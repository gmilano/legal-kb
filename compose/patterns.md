---
industry: legal
region: Global
updated: 2026-11-04
---

# 🧩 Patrones de composición — Legal Services

> Recetas para construir soluciones combinando repos + agentes + AI.
> Última actualización: 2026-11-04
> Cada receta nombra repos **verificados vivos el 2026-11-04 con licencia leída del fichero**.

## Patrón base

```
[Ingesta documental]      Docling (MIT) / Unstructured (Apache-2.0) / Tika (Apache-2.0)
          ↓
[De-identificación PII]   Presidio (MIT)      ← obligatorio antes de egreso a LLM externo
          ↓
[Extracción tipada]       ContextGem (Apache-2.0)  ← con cita al párrafo de origen
          ↓
[Agentes especializados]  lavern (Apache-2.0) como patrón de human gates
          ↓
[Entrega en formato del abogado]  DOCX tracked changes / API con citas
```

La regla que no se negocia: **Presidio va antes del primer egreso**, y **toda afirmación vuelve
con su cita**. Lo primero hace el despliegue legal bajo GDPR/LGPD; lo segundo lo hace usable.

---

## P1 — Pipeline de revisión de contratos con redline auditable
**Regiones:** North America, EMEA · **Esfuerzo:** 6–8 semanas a MVP productivo

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [docling](https://github.com/docling-project/docling) | MIT | PDF/DOCX escaneado → estructura con números de página |
| 2 | [presidio](https://github.com/microsoft/presidio) | MIT | redacta PII antes de llamar al LLM |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | *aspects* (indemnización, limitación de responsabilidad, rescisión, pago) → *concepts* tipados + cita |
| 4 | [contract-review-agent](https://github.com/lowtidebuild/contract-review-agent) | Apache-2.0 | DOCX redline interno + limpio externo + informe |
| 5 | [OpenContracts](https://github.com/JSv4/OpenContracts) | MIT | repositorio, anotación y analítica de cartera |

**Cableado:** Docling y ContextGem encajan sin adaptador — ContextGem **usa Docling como backend
de lectura**, así que el paso 1→3 es configuración, no integración. Presidio se interpone como
middleware en la llamada al LLM (reemplazo de entidades reversible con mapa de tokens guardado
fuera del prompt). ContextGem emite JSON tipado con referencias de párrafo; el paso 4 lo consume
para posicionar los tracked changes.
**Por qué gana:** devuelve el artefacto que el abogado ya negocia (DOCX con tracked changes) en
lugar de un chat, y cada hallazgo es auditable hasta su párrafo.

---

## P2 — Asistente legal defendible bajo EU AI Act
**Región:** EMEA · **Esfuerzo:** 10–12 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | Ollama o vLLM (self-hosted, EU) | MIT / Apache-2.0 | inferencia sin egreso transfronterizo |
| 2 | [presidio](https://github.com/microsoft/presidio) | MIT | de-identificación documentada |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | *decision models* que devuelven **probabilidad por respuesta** en preguntas cerradas |
| 4 | Patrón de [lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | human gates obligatorios + verificación multi-paso |
| 5 | Registro de auditoría propio | — | traza por decisión: entrada, cita, confianza, aprobador |

**Cableado:** el paso 3 es la clave de compliance — como ContextGem devuelve probabilidades en
preguntas cerradas, se puede fijar un **umbral por tipo de cláusula** y enrutar todo lo que caiga
por debajo al gate humano del paso 4, dejando registro de por qué escaló. Eso convierte
"supervisión humana" de promesa en mecanismo con evidencia.
**Anclas normativas:** aplicación del Reglamento desde el **2-ago-2026**; transparencia desde el
**2-ago-2026** con transición al **2-dic-2026** para marcado de contenido ya en mercado; la
Comisión indica que **los agentes no son categoría aparte**, luego **Art. 50** aplica a agentes
que interactúan con personas → el UI debe declarar que es AI y marcar el contenido generado.
⚠️ El calendario de alto riesgo (ago-2026 vs. ago-2028) está en conflicto entre fuentes: diseñar
para el supuesto estricto y no afirmar la fecha al cliente.

---

## P3 — Acceso a la justicia a escala (es/pt)
**Región:** LATAM · **Esfuerzo:** 8–10 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [docassemble](https://github.com/jhpyle/docassemble) | MIT | entrevista guiada con lógica condicional (Python/YAML) |
| 2 | [docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | MIT | formulario judicial en papel → web app paso a paso |
| 3 | [presidio](https://github.com/microsoft/presidio) | MIT | PII de ciudadanos fuera del LLM |
| 4 | LLM local (Ollama) | MIT | sin coste por token ni egreso de datos |

**Cableado:** AssemblyLine es un paquete **sobre** docassemble, así que 1→2 es instalación, no
integración. El LLM no redacta el documento legal: rellena y explica la entrevista, y el documento
sale de la plantilla determinista de docassemble. Esa separación es la que hace el patrón
defendible — el output legal es plantilla auditada, no generación.
**Encaje LGPD:** la LGPD da derecho a **revisión de decisiones automatizadas** y la **ANPD ya
suspendió** funciones de plataformas que entrenaban con datos personales sin base legal. Con
plantilla determinista + LLM local + Presidio, el derecho de revisión es trivial de satisfacer.
**Compradores:** defensorías públicas, poder judicial, clínicas jurídicas universitarias.

---

## P4 — Backend de investigación jurisprudencial
**Regiones:** Global (sensible a licencia) · **Esfuerzo:** 4–6 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1a | [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | **MIT** | plataforma de datos legales + API REST + Elasticsearch |
| 1b | [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | **AGPL-3.0** ⚠️ | archivo de datos judiciales EE. UU. |
| 2 | [docling](https://github.com/docling-project/docling) | MIT | normaliza sentencias a estructura |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | extrae holding, ratio, jurisdicción, fecha |
| 4 | [Blackstone](https://github.com/ICLRandD/Blackstone) | Apache-2.0 | NER legal (rama `master`; *early prototype*) |

**Decisión de licencia, explícita:** si el entregable es un SaaS cerrado, **elegir 1a (OLDP, MIT)**.
CourtListener es **AGPL-3.0** (35.140 B leídos): al exponerse por red obliga a ofrecer el fuente
de la obra derivada. Para investigación interna o producto abierto, 1b aporta mucho más corpus
de EE. UU. Esta es la bifurcación que hay que resolver **antes** de escribir código, no después.

---

## P5 — Razonamiento legal por jurisdicción en APAC (derecho chino)
**Región:** APAC · **Esfuerzo:** 8–10 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [DISC-LawLLM](https://github.com/FudanDISC/DISC-LawLLM) | Apache-2.0 | LLM legal chino (Fudan DISC) |
| 2 | [fuzi.mingcha](https://github.com/irlab-sdu/fuzi.mingcha) | Apache-2.0 | LLM judicial chino (Shandong + Inspur + CUPL), base ChatGLM |
| 3 | [presidio](https://github.com/microsoft/presidio) | MIT | PII |
| 4 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | capa de extracción agnóstica del modelo |
| 5 | Paquete de evidencias | — | model cards + trazas + logs de gates |

**Cableado:** ContextGem queda por encima del modelo, de modo que 1 y 2 son intercambiables
detrás de la misma interfaz de extracción; se puede evaluar cuál responde mejor por tipo de
materia sin rehacer el pipeline.
**Por qué el paso 5 es el producto:** en **Singapur no hay ley de AI**, pero bancos y agencias
**exigen evidencia de AI Verify a sus proveedores**, y la autoridad monetaria publicó guías de
riesgo de AI para entidades financieras el **7-oct-2026**. En **Corea** el AI Basic Act rige desde
ene-2026. El paquete de evidencias reutilizable es lo que se vende, por encima del modelo.

---

## P6 — Banco de evaluación de extracción de cláusulas
**Regiones:** Global (interno) · **Esfuerzo:** 3–4 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [CUAD](https://github.com/TheAtticusProject/cuad) | ⚠️ **sin fichero LICENSE** | 510 contratos anotados por expertos, 41 categorías de cláusula |
| 2 | [lex-glue](https://github.com/coastalcph/lex-glue) | ⚠️ **sin fichero LICENSE** | benchmark de comprensión legal |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | sistema bajo prueba |
| 4 | [Blackstone](https://github.com/ICLRandD/Blackstone) | Apache-2.0 | línea base de NER |

⚠️ **Aviso de licencia:** CUAD y lex-glue están **vivos** pero **no tienen fichero LICENSE**
(probado contra `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `COPYING`, `LICENCE` en su rama por
defecto). Sirven para **evaluación interna**; no redistribuir dataset ni derivados en un
entregable de cliente sin aclarar términos con Atticus Project / los autores.
**Para qué sirve igualmente:** da una cifra defendible de precisión/recall por tipo de cláusula
antes de prometer exactitud a un cliente — justamente el dato que falta en el 43–54% de despachos
sin gobernanza.

---

## Nota sobre este fichero
La versión anterior contenía una sola receta titulada "Receta 1" con todos sus campos en guiones.
Sustituida por 6 patrones con repos nombrados, licencias leídas y el cableado explícito.
