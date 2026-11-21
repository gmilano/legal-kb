---
industry: legal
region: Global
updated: 2026-11-21
---

# 🧩 Patrones de composición — Legal Services

> Recetas para construir soluciones combinando repos + agentes + AI.
> Última actualización: 2026-11-20
> Cada receta nombra repos **verificados el 2026-11-20 por API de GitHub + lectura del LICENSE**.
>
> ⚠️ **Corrección aplicada a TODAS las recetas:** las versiones anteriores apuntaban a
> `microsoft/presidio` y `JSv4/OpenContracts`. **Ambos slugs están obsoletos** (renombrados a
> `data-privacy-stack/presidio` y `Open-Source-Legal/OpenContracts`). Un `git clone` del slug viejo
> todavía funciona por redirección, pero un pin de dependencia, un submódulo o un mirror interno
> apuntados ahí **quedan atados a un nombre que el upstream ya no usa**. Corregidos abajo.

## Patrón base

```
[Ingesta documental]      Docling (MIT) / Unstructured (Apache-2.0) / Tika (Apache-2.0)
          ↓
[De-identificación PII]   Presidio (MIT)      ← obligatorio antes de egreso a LLM externo
          ↓  (+ Databunker (MIT) si además hay que CUSTODIAR la PII, no sólo redactarla)
          ↓
[Extracción tipada]       ContextGem (Apache-2.0)  ← con cita al párrafo de origen
          ↓
[Verificación de cita]    contra la FUENTE OFICIAL ← korean-law-mcp / CaseCite como referencia
          ↓
[Agentes especializados]  claude-for-legal (Apache-2.0) como base; lavern como patrón de gates
          ↓
[Entrega en formato del abogado]  DOCX tracked changes / API con citas / firma
```

Tres reglas que no se negocian:
1. **Presidio va antes del primer egreso** — es lo que hace el despliegue legal bajo GDPR/LGPD.
2. **Toda afirmación vuelve con su cita** — es lo que lo hace usable.
3. 🆕 **La cita se verifica contra la fuente, no sólo contra el documento** — es lo que lo hace
   defendible donde la firma del abogado certifica la autenticidad de lo citado (Indiana TR 11).

---

## P1 — Pipeline de revisión de contratos con redline auditable
**Regiones:** North America, EMEA · **Esfuerzo:** 6–8 semanas a MVP productivo

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [docling](https://github.com/docling-project/docling) | MIT | PDF/DOCX escaneado → estructura con números de página |
| 2 | [presidio](https://github.com/data-privacy-stack/presidio) | MIT | redacta PII antes de llamar al LLM |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | *aspects* (indemnización, limitación de responsabilidad, rescisión, pago) → *concepts* tipados + cita |
| 4 | [contract-review-agent](https://github.com/lowtidebuild/contract-review-agent) | Apache-2.0 | DOCX redline interno + limpio externo + informe |
| 5 | [OpenContracts](https://github.com/Open-Source-Legal/OpenContracts) | MIT | repositorio, anotación y analítica de cartera |

**Cableado:** Docling y ContextGem encajan sin adaptador — ContextGem **usa Docling como backend
de lectura**, así que el paso 1→3 es configuración, no integración. Presidio se interpone como
middleware en la llamada al LLM (reemplazo de entidades reversible con mapa de tokens guardado
fuera del prompt). ContextGem emite JSON tipado con referencias de párrafo; el paso 4 lo consume
para posicionar los tracked changes.
**Por qué gana:** devuelve el artefacto que el abogado ya negocia (DOCX con tracked changes) en
lugar de un chat, y cada hallazgo es auditable hasta su párrafo.
⚠️ **Riesgo de dependencia nuevo:** `contract-review-agent` resuelve en `raw` pero **no aparece en
el índice de búsqueda de GitHub**, la misma firma que un renombrado, y su README no permite
determinar el slug canónico. **Vendorizar el repo en el primer sprint** en vez de depender del
slug. Alternativa si eso no es aceptable: la etapa de redline de **CaseCite** (Apache-2.0).

---

## P2 — Asistente legal defendible bajo EU AI Act
**Región:** EMEA · **Esfuerzo:** 10–12 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | Ollama o vLLM (self-hosted, EU) | MIT / Apache-2.0 | inferencia sin egreso transfronterizo |
| 2 | [presidio](https://github.com/data-privacy-stack/presidio) | MIT | de-identificación documentada |
| 3 | [databunker](https://github.com/securitybunker/databunker) | MIT | custodia cifrada de la PII que **no** se puede redactar (partes, firmantes) |
| 4 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | extracción con trazabilidad al párrafo |
| 5 | patrón de [lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | human gates obligatorios + log de aprobación |
| 6 | [claude-fuer-deutsches-recht](https://github.com/Klotzkette/claude-fuer-deutsches-recht) | Apache-2.0 | si el engagement es alemán: flujos y **Testakten** ya hechos |

**Cableado:** el log de gates del paso 5 es el artefacto de compliance, no un subproducto — se
diseña con esquema estable desde el día 1 (quién aprobó, qué vio, qué cambió, cuándo), porque es
lo que se entrega a una auditoría.
🔴 **Encuadre obligatorio por calendario, y cambia la propuesta:** el plazo de **marcado de
contenido sintético ya en el mercado es el 2-dic-2026**, es decir **12 días desde este pase**.
Proponer «un sprint de 3-5 semanas para cumplir el marcado» **es vender un incumplimiento.** Lo
que cabe: (A) inventario de exposición en **días**, (B) marcado del subconjunto crítico,
(C) plan fechado post-plazo **con el gap documentado** — que es lo que un regulador valora por
encima de un cumplimiento fingido.
**Lo que sí tiene 10-12 semanas de margen:** las obligaciones de alto riesgo, retrasadas por el
Digital Omnibus a **2-dic-2027 (Anexo III)** y **2-ago-2028 (Anexo I)**.
🆕 **Añadir siempre el Art. 4 (alfabetización en AI):** el Reglamento exige comprensión adecuada
por parte del personal que usa AI. Con **54% de despachos sin formación**, un programa de AI
literacy con registro de asistencia y evaluación **es evidencia de cumplimiento**, y se vende
junto al despliegue, no después.

---

## P3 — Acceso a la justicia a escala (es/pt)
**Región:** LATAM · **Esfuerzo:** 8–10 semanas por tipo de trámite

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [docassemble](https://github.com/jhpyle/docassemble) | MIT | entrevista guiada condicional (rama `master`) |
| 2 | [docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | MIT | formulario judicial en papel → web app paso a paso |
| 3 | [presidio](https://github.com/data-privacy-stack/presidio) | MIT | PII del ciudadano antes de cualquier egreso |
| 4 | [legal-templates](https://github.com/General-Legal/legal-templates) | **CC0-1.0** | 🆕 base de plantillas **en dominio público**: redistribuible en un entregable cerrado sin cadena de licencias |
| 5 | LLM sólo en **explicación**, nunca en el texto final | — | el documento sale de plantilla determinista |

**Cableado:** el paso 5 es la decisión arquitectónica central y es deliberadamente conservadora:
**el LLM explica y guía, la plantilla genera.** El texto que se presenta ante un tribunal nunca es
salida de modelo.
**Por qué gana, y es el argumento regulatorio más fuerte de esta KB:** bajo LGPD (derecho a
revisión de decisiones automatizadas), bajo el **reglamento peruano de la Ley 31814 — que exige
supervisión humana para alto riesgo** — y ante cualquier regulador, **un documento que proviene de
plantilla determinista no es una decisión automatizada**. El riesgo se elimina por diseño, no se
mitiga.
**Contexto de riesgo que refuerza la venta:** la **ANPD brasileña es agencia de pleno derecho
desde feb-2026** y ya había suspendido funciones de plataformas que entrenaban con datos
personales sin base legal. Es riesgo demostrado, no teórico.

---

## P4 — Backend de investigación jurisprudencial
**Regiones:** North America, EMEA · **Esfuerzo:** 6–8 semanas

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [oldp](https://github.com/openlegaldata/oldp) | **MIT** | plataforma de corpus: ingesta, API REST, búsqueda Elasticsearch |
| 2 | [awesome-legal-data](https://github.com/openlegaldata/awesome-legal-data) | ⚠️ NONE | 🆕 mapa de fuentes de datos legales por país (consultar, no redistribuir) |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | extracción de holdings y ratio decidendi con cita |
| 4 | [casecite](https://github.com/thomasunise/casecite) | Apache-2.0 | 🆕 capa de research lista: retrieval híbrido + **cada afirmación verificada contra su pasaje** |

⚠️ **La decisión de licencia de esta receta, y es la que define el entregable.** **CourtListener
(AGPL-3.0)** tiene el mejor corpus de EE. UU., pero su copyleft **de red** significa que si el
cliente expone el servicio, debe liberar el derivado. **OLDP es MIT** y es la única
corpus-platform permisiva que existe.
⇒ **Entregable cerrado: OLDP.** ⇒ **Investigación interna o entregable abierto: CourtListener.**
Decidirlo **antes** del primer sprint, no después: es una decisión de arquitectura, no de licencia.
Nota: CaseCite consulta CourtListener **como fuente externa por API**, lo que **no** contagia AGPL
al código del cliente — consumir un servicio no es distribuir una obra derivada.

---

## P5 — Razonamiento legal por jurisdicción en APAC
**Región:** APAC · **Esfuerzo:** 4–6 semanas (Corea) / 10–14 semanas (China)

**🆕 Esta receta cambia de componente principal respecto al pase anterior.** La versión previa se
construía sobre los tres LLM legales chinos. Medido hoy: **DISC-LawLLM 18 meses sin commits,
fuzi.mingcha 16, lawyer-llama 27.** Siguen siendo buenos *modelos* y buen *corpus*; **no son
proyectos vivos**, y no se le promete a un cliente que se construye sobre algo que nadie mantiene.

**Ruta recomendada hoy — Corea, y es la mejor de la región:**

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) | MIT | **42 APIs oficiales del 법제처** en 10 herramientas MCP: leyes, jurisprudencia, reglamentos, normativa autonómica, tratados, interpretaciones |
| 2 | el mismo repo | MIT | **contraste de las citas del LLM contra el texto oficial** — verificación, no promesa |
| 3 | [korean-privacy-terms](https://github.com/kimlawtech/korean-privacy-terms) | Apache-2.0 | terminología de privacidad coreana normalizada |
| 4 | [korean-tax-mcp](https://github.com/UpstageAI/korean-tax-mcp) | MIT | si el alcance incluye fiscal: resoluciones de la NTS y tribunales |
| 5 | patrón de [lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | human gates |

**Por qué Corea primero:** es la única jurisdicción APAC donde **la fuente oficial es accesible por
API y ya está envuelta** (2.904★, commit de hoy). El esfuerzo baja de «construir un corpus» a
«cablear un MCP». Y la ventana regulatoria acompaña: la **AI Basic Act está en vigor desde el
22-ene-2026, pero el MSIT indica que 2026 funciona de hecho como periodo piloto con enforcement
limitado** ⇒ es el momento de construir la evidencia, antes de que muerda.
**Otras jurisdicciones con pieza disponible:** `mhfed/vn-law-check` (Vietnam, MIT — y **Vietnam
tiene ley integral de AI en vigor desde el 1-mar-2026**), `aa0101181514/tw-legal-rag` (Taiwán),
`kevanwee/sg-legal-corpus` (Singapur, MIT), `lawglance` (India, Apache-2.0).
⚠️ **China:** usar DISC-LawLLM / fuzi.mingcha / lawyer-llama como **modelos y corpus congelados**,
fijando el commit y asumiendo el mantenimiento. No como upstream vivo.

---

## P6 — Banco de evaluación de extracción de cláusulas
**Región:** Global · **Esfuerzo:** 3–4 semanas

⚠️ **Esta receta pierde su dataset principal y hay que decirlo.** Se construía sobre **CUAD**
(`TheAtticusProject/cuad`). **Ese repo ya no existe** — `repo:` da 422 y `raw` da 404 en `main`,
`master` y `HEAD`. CUAD sigue siendo válido como **concepto** de benchmark (y
`evolsb/claude-legal-skill` implementa detección de riesgo basada en él), pero **el puntero de
GitHub está muerto** y no se puede clonar.

**Sustitución verificada hoy:**

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [legal-templates](https://github.com/General-Legal/legal-templates) | **CC0-1.0** | corpus de plantillas en dominio público como base de casos |
| 2 | [template-archive](https://github.com/accordproject/template-archive) | Apache-2.0 | plantillas del Accord Project con lógica ejecutable: **la lógica da el ground truth** |
| 3 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | sujeto a evaluar: extracción tipada con cita |
| 4 | [lex-glue](https://github.com/coastalcph/lex-glue) | ⚠️ **NONE** | benchmark académico — **sólo evaluación interna**, no redistribuir |

**Cableado:** el paso 2 es el truco de la receta. Una plantilla del Accord Project **lleva su
propia lógica contractual**, así que se puede generar un contrato instanciado **sabiendo de
antemano el valor correcto de cada campo**. Eso da ground truth sin anotación manual, que es el
coste que normalmente hunde este tipo de proyecto.
⚠️ `lex-glue` existe (276★) pero **no tiene fichero de licencia** (confirmado hoy): válido para
medir internamente, **no** para incluir en un entregable.

---

## 🆕 P7 — Adaptación por jurisdicción: la plaza vacía de LATAM

> ⚠️ **CORRECCIÓN (pase 2 del 2026-11-20).** La premisa de «plaza vacía» era **parcialmente
> falsa**: `ThomasMoreAI/legal-skills-open` (Apache-2.0) ya tiene **Brasil 15 plugins**, Argentina
> 2, México 2, Colombia 1, Perú 1, Rep. Dominicana 1. **Este patrón sigue siendo válido pero ya no
> parte de cero: parte de contribuir profundidad a una estructura existente.** Y el hueco que
> **sí** está vacío se trabaja en **P12** (ningún MCP de fuentes legales oficiales LATAM).

**Región:** LATAM · **Esfuerzo:** 3–5 semanas (plugins) + 4–8 semanas (MCP de fuentes oficiales)

**Esta es la receta más acotada de esta KB, porque no inventa el patrón: lo copia.** Existe una
plantilla probada **y replicada dos veces**, con licencia que lo permite expresamente.

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Apache-2.0 | **base**: arquitectura de plugins, patrones de diseño, cold-start interviews, perfiles de práctica |
| 2 | [claude-para-abogados](https://github.com/betobetico/claude-para-abogados) | Apache-2.0 | **plantilla de adaptación**: ya hizo el trabajo para España/UE (20 módulos, 100 skills, 17 agentes) y **atribuye explícitamente el diseño a Anthropic** — el modelo de atribución a imitar |
| 3 | [claude-fuer-deutsches-recht](https://github.com/Klotzkette/claude-fuer-deutsches-recht) | Apache-2.0 | **segunda prueba de que el patrón se replica**, y de dónde copiar la idea de *Testakten* (expedientes ficticios para ensayar sin datos reales) |
| 4 | [korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) | MIT | **plantilla de la capa de fuentes**: cómo envolver las APIs legales oficiales de un país y verificar citas contra ellas |
| 5 | [presidio](https://github.com/data-privacy-stack/presidio) | MIT | PII, con LGPD en mente desde el diseño |

**El hueco, medido y no heredado:** se buscó hoy con vocabulario es/pt (4 búsquedas) y **no existe
ni adaptación de plugins ni MCP de jurisdicción para Brasil o México**. Todo lo hallado de origen
LATAM está entre 0 y 3★.
⚠️ **Y el error que hay que no cometer:** `claude-para-abogados` está en castellano pero es
**derecho de España — EMEA**. Su contenido mercantil, laboral y procesal es español y europeo.
Para un engagement brasileño o mexicano **sirve como plantilla de estructura, no como contenido.**

**Secuencia recomendada:**
1. Fork de `claude-for-legal`, fijando commit. Apache-2.0 permite la obra derivada; **mantener el
   NOTICE y atribuir como hace `claude-para-abogados`.**
2. Elegir **un** área de alto volumen primero (laboral en Brasil, o contratos mercantiles en
   México). No portar 20 módulos en el primer sprint.
3. La capa de fuentes es el cuello de botella real: **en Brasil y México no hay un `법제처` con 42
   APIs limpias.** Inventariar qué está disponible (DOU, LexML, Diario Oficial de la Federación)
   **antes** de prometer verificación de cita contra fuente oficial. **Éste es el riesgo técnico
   principal de la receta y hay que decirlo en la propuesta, no descubrirlo en la semana 6.**
4. Verificar **las dos licencias** del corpus que se incorpore (software ≠ corpus; ver P9).

**Límite honesto:** las 49★ de la adaptación española y las 1.866★ de la alemana **miden interés,
no producción**. Son colecciones de plugins y prompts, no runtimes con usuarios medidos. Esta
receta es una apuesta de posicionamiento temprano en una plaza vacía — **no** una categoría con
demanda probada.

---

## 🆕 P8 — Citation integrity como producto
**Región:** North America (principal), Global · **Esfuerzo:** 4–6 semanas

**Por qué ahora:** con alucinación reportada del **17–33%** en research legal y con la regla de
**Indiana (Trial Rule 11, en vigor 1-ago-2026)** —**la firma del abogado certifica que la autoridad
citada es auténtica, y cubre expresamente los escritos asistidos por AI**— la verificación de cita
pasa de mejora técnica a **transferencia de riesgo personal al socio firmante**. La política
interina del **New York UCS** empuja en la misma dirección.

| Paso | Componente | Licencia | Función |
|------|-----------|----------|---------|
| 1 | [casecite](https://github.com/thomasunise/casecite) | Apache-2.0 | **cada afirmación comprobada contra el pasaje que cita**; deep research con step log de lo buscado |
| 2 | [contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | trazabilidad al párrafo como propiedad del framework, sin chunking por retrieval |
| 3 | [courtlistener](https://github.com/freelawproject/courtlistener) | ⚠️ AGPL-3.0 | fuente de autoridad de EE. UU. — **consumida por API**, no forkeada (ver P4) |
| 4 | patrón de [korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) | MIT | el patrón a copiar: **contrastar contra la fuente oficial**, no sólo contra el corpus local |
| 5 | patrón de [lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | gate humano obligatorio antes de que una cita salga en un escrito |

**Cableado, y es lo que distingue esta receta de un RAG normal:** hay **dos verificaciones
distintas** y las dos hacen falta. (a) *¿El pasaje dice lo que el modelo afirma?* — eso es el
paso 1-2, contra el documento. (b) *¿La autoridad citada existe y está vigente?* — eso es el
paso 3-4, contra la fuente. **Un RAG normal sólo hace (a)**, y una cita a un caso inventado pasa
(a) sin problema si el modelo también inventó el pasaje.
**El entregable que se vende no es el chat: es el log.** Un informe por escrito que, para cada
autoridad citada, registra: la cita, la fuente consultada, la fecha de consulta, el pasaje
verificado y quién lo aprobó. Eso es lo que el socio firmante necesita si le preguntan.
**Por qué es vendible ahora:** se vende al **riesgo de sanción**, no al ahorro de horas. Es un
presupuesto distinto, con otro comprador (el general counsel o el comité de riesgo) y mucho menos
sensible al precio.

---

## 🆕 P9 — Auditoría de licencia para un entregable legal (mecánica, sin dependencias)
**Región:** Global · **Esfuerzo:** 1–2 días por cartera de repos

Receta de proceso, no de producto. Es lo que este pase usó para encontrar 2 renombrados, 1 repo
muerto, 1 AGPL escondida y 2 grants partidos. **Cuesta minutos y se puede correr en cualquier KB.**

**Canal 1 — índice de la plataforma (existencia + metadatos):**
```
gh api -X GET search/repositories -f q='repo:<owner>/<name>' \
  --jq '.items[]|[.full_name,(.license.spdx_id//"NONE"),(.stargazers_count|tostring),
                  (.archived|tostring),.pushed_at,.default_branch]|@tsv'
```
**Canal 2 — el fichero real (la licencia):**
```
curl -sL "https://raw.githubusercontent.com/<owner>/<name>/HEAD/LICENSE" -o L.txt -w '%{http_code} %{size_download}'
# probar también LICENSE.md, LICENSE.txt, LICENCE, COPYING
```
**Siempre `/HEAD/`, nunca una rama fija:** OpenSign está en `staging`, docassemble, databunker,
lexnlp, awesome-legal-data y awesome-legal-nlp en `master`.

**Las seis cosas que detecta, cada una con un caso real de esta KB:**

| Síntoma | Qué significa | Caso real |
|---------|---------------|-----------|
| `repo:` da **422** + `raw` da **200** | **renombrado** (GitHub sirve por redirección) | `microsoft/presidio` → `data-privacy-stack/presidio` |
| `repo:` da **422** + `raw` da **404** | **repo muerto** | `TheAtticusProject/cuad` |
| API dice **`NOASSERTION`** | licencia **compuesta o no reconocida**, *no* ausencia | `OpenSign` = AGPL-3.0 con 16 menciones a Affero |
| Bytes **por encima** de la banda de la familia | preámbulo antepuesto o licencia compuesta | `courtlistener`: 35.140 B = AGPL 34.523 + 617 B de copyright |
| Bytes **muy por debajo** de la banda | **fichero puntero** — seguir el puntero | `lexifina/global-law`: 935 B de CC0 en forma corta |
| Licencia limpia **pero el corpus excluido** | **grant partido código/corpus** | `vn-law-check`: MIT + «cannot license the underlying legal texts» |

**Bandas canónicas:** MIT/Expat 1.050–1.150 · CC0 ~7.048 · Apache-2.0 ~11.358 · MPL-2.0 ~16.700 ·
CC-BY-4.0 ~18.650 · LGPL-2.1 ~26.400 · AGPL-3.0 ~34.523 · GPL-3.0 ~35.149.

**Control negativo obligatorio:** correr la auditoría también sobre un repo que se sabe limpio. Si
no produce «limpio», el instrumento está roto. (Y el falso positivo simétrico a tener presente: un
LICENSE correcto envuelto en un bloque de código Markdown hace que el detector de GitHub devuelva
`NOASSERTION` sobre una licencia perfectamente válida.)

**Clasificación POR CONSECUENCIA, que es lo que el cliente pregunta — no por nombre de licencia:**
1. **Permisiva limpia** → úsala (MIT, Apache-2.0, BSD, CC0).
2. **Permisiva con tarea asignada** → úsala y cumple (Apache-2.0 exige conservar NOTICE).
3. **Copyleft de red** → **bloqueante para SaaS cerrado** (AGPL: courtlistener, lexnlp, mike,
   OpenSign).
4. **Grant partido código/corpus** → **verifica la mitad que importa**: en legal, el corpus.
5. **Sin licencia (`NONE`)** → sin permiso de redistribución. Evaluación interna sólo
   (lex-glue, Vaquill-AI/awesome-legaltech, awesome-legal-data).
6. **Procedencia sin establecer** → no recomendar hasta resolver (LawLink: tres copias idénticas
   bajo cuentas distintas).

⚠️ **Límite honesto, y hay que escribirlo en el entregable:** esto es una auditoría de
**procedencia declarada**. **No** es una opinión legal, **no** es un escaneo de código copiado, y
**no** responde la pregunta de los pesos del modelo.

---

## 🆕 P10 — Verificación de cita ejecutable (la obligación que converge en las tres regiones)

**Para quién:** despacho o legal dept. en EE. UU. (Indiana Trial Rule 11, 1-ago-2026), UE
(Art. 50) o LATAM (Colombia AC739-2026: 15 salarios mínimos de multa). **El comprador es el
abogado que firma.**

**Piezas (todas verificadas, todas permisivas):**

| Capa | Repo | Licencia |
|---|---|---|
| Fuente + resolución de citas | [jonashertner/opencaselaw](https://github.com/jonashertner/opencaselaw) | MIT + **CC0** datos |
| Fuente alternativa por jurisdicción | [chrisryugj/korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) · [lawchat-oss/mcp-taiwan-legal-db](https://github.com/lawchat-oss/mcp-taiwan-legal-db) · [JamesANZ/us-legal-mcp](https://github.com/JamesANZ/us-legal-mcp) · [ayunis-core/ayunis-legal-mcp](https://github.com/ayunis-core/ayunis-legal-mcp) | MIT |
| Afirmación ↔ pasaje | [thomasunise/casecite](https://github.com/thomasunise/casecite) | Apache-2.0 |
| Extracción con trazabilidad | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 |
| Redacción de PII antes del LLM | [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT |

**Cableado — el paso 3 es el que no existía antes de este pase:**

1. **Extraer** del borrador toda cadena con forma de cita (regex por jurisdicción: `BGE \d+ \w+ \d+`,
   `\d+ U.S. \d+`, número de radicado, etc.).
2. **Redactar PII** con Presidio antes de que el borrador toque cualquier modelo externo.
3. **Resolver cada cita contra la fuente oficial** — ejecutable, no prometido:
   ```bash
   # por cada referencia: si la sentencia existe y cuál es
   ocl citations resolve 'BGE 136 III 513' '4A_747/2012' 'BGE 999 III 1'
   ```
   Las que no resuelven son **citas inexistentes**: ese es el hallazgo que evita la sanción.
4. **Para las que sí resuelven**, contrastar con CaseCite que **la proposición del borrador
   coincide con el pasaje citado** — una cita real que no dice lo que se le atribuye falla la
   misma regla procesal.
5. **Emitir un log firmable** por cita: `{cita, resuelta: sí/no, id_fuente, pasaje, hash, timestamp}`.

> ⚠️ **Límite que hay que decirle al cliente, y decirlo es parte del producto.** El propio
> `opencaselaw` lo documenta: **una comprobación de cita establece que la sentencia existe, no que
> sea autoridad aplicable al caso.** El paso 4 cubre la correspondencia textual; **la pertinencia
> jurídica sigue siendo del abogado.** Vender esto como «AI que valida tu argumentación» es
> exactamente la sobrepromesa que produce la sanción que el producto dice evitar.

**Por qué gana:** es el único requisito que comparten las tres rutas regulatorias (regla procesal
en EE. UU., reglamento en la UE, jurisprudencia en LATAM). Se vende al **riesgo de sanción
nominado**, no al ahorro de horas.

## 🆕 P11 — E-discovery como punto de entrada (el flujo donde la alucinación no llega al cliente)

**Para quién:** litigation support, investigaciones internas, respuesta a requerimientos.
**Por qué primero:** el entregable es *un conjunto de documentos responsivos*. Un fallo es **recall
medible y corregible**, no una afirmación falsa firmada. Es el engagement legal más fácil de
defender ante un socio escéptico.

| Paso | Repo | Licencia |
|---|---|---|
| Ingesta forense (PST, ZIP, imágenes), dedup, metadatos, culling, producción | [shmsoft/FreeEed](https://github.com/shmsoft/FreeEed) | Apache-2.0 |
| Parsing estructural de lo que FreeEed extrae | [docling-project/docling](https://github.com/docling-project/docling) | MIT |
| Barrido de PII antes de cualquier modelo externo | [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT |
| Custodia de PII identificada | [securitybunker/databunker](https://github.com/securitybunker/databunker) | MIT |
| Clasificación responsivo/privilegiado con trazabilidad al párrafo | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 |

**Cableado:** FreeEed hace la ingesta y el culling determinista (dedup por hash, filtros de fecha y
custodio) → Docling normaliza a estructura con número de página → Presidio marca PII y Databunker
la custodia tokenizada → **ContextGem clasifica con el párrafo de soporte atado a cada decisión** →
revisión humana sólo sobre el subconjunto dudoso.

**La métrica que hace vendible el piloto:** el culling determinista de FreeEed se mide contra el
corpus completo (**% de volumen eliminado sin revisión humana**) y es verificable sin discutir sobre
la calidad del modelo. **Todo el pipeline es MIT/Apache-2.0: entregable cerrado sin cadena de
licencias.**

## 🆕 P12 — La capa de fuentes legales oficiales de LATAM: **qué adoptar, qué endurecer y qué construir** · ♻️ **REESCRITO EN EL PASE 6 (2026-11-21)**

> 🔴 **Este patrón estaba construido sobre una premisa falsa.** Decía: *«existen MCP de fuentes
> oficiales para EE. UU., Alemania, Suiza, Italia, Taiwán, Corea y China. Para Brasil, México,
> Argentina, Chile, Colombia y Perú: ninguno»*, y proponía 4–8 semanas para construir **el
> primero**. Existen cuatro, con licencia leída byte a byte, y uno de ellos es **exactamente** el
> ejemplo que el patrón ponía como cosa a construir (el DOF mexicano). El fallo fue de
> **independencia de canal**, no de rigor: ver `agents/top.md` → **G-L12**. El patrón se conserva
> con el mismo número porque la *arquitectura* era correcta; lo que cambia es **el punto de
> partida**, que ya no es un folio en blanco.

### Estado real de la capa (medido 2026-11-21)

| País | Legislación | Jurisprudencia | Boletín oficial | Estado |
|------|-------------|----------------|-----------------|--------|
| 🇧🇷 Brasil | `leis-mcp` (MIT, 1,21 M normas, avisos de revogação) · `br-eli-mcp` (Apache-2.0, `normas.leg.br` a nivel de artículo) | `jurismcp` (MIT: STJ, STF, TST, TJES, LexML, **BNP/CNJ**, TNU, TRF4) · `br-eli-mcp` (STJ, TST, TCU, CARF, DataJud/CNJ) | `br-eli-mcp` (publicación en **DOU** vía Congresso) | 🟢 **Cubierto — adoptar y endurecer** |
| 🇲🇽 México | — | — | `mcp-dof` (MIT, API oficial **SIDOF**) | 🟡 **Medio — falta SCJN/jurisprudencia** |
| 🇦🇷 🇨🇱 🇨🇴 🇵🇪 | — | — | — | 🔴 **Vacío — aquí sí se construye** |

### Lo que hay que hacer, en orden, y ya no es «empezar»

1. **ADOPTAR (días, no semanas).** Para Brasil, los tres servidores se montan en paralelo: no
   compiten, se complementan. `leis-mcp` da texto de norma **con aviso de revogação**,
   `br-eli-mcp` da articulado + fiscal (CARF) + control externo (TCU) **sobre API, sin scraping**,
   y `jurismcp` da jurisprudencia. Licencias MIT/Apache-2.0 en los tres ⇒ **sin fricción entre
   ellos ni con `legal-skills-open/br/` (Apache-2.0)**.
2. **ENDURECER — y esto es lo facturable.** Las tres debilidades están declaradas por los propios
   repos y son exactamente lo que un despacho no puede arreglar solo:
   - `jurismcp` usa **navegador headless y scraping HTML** para STF, TST, TNU y TRF4 ⇒ se rompe con
     cada rediseño de portal. Migrar a API donde exista, y donde no, **contrato de prueba que falle
     ruidosamente** en vez de devolver vacío (un `resolver_cita` que calla es peor que uno que
     falla).
   - `leis-mcp` advierte de **errores de conversión/OCR** y de que su búsqueda sin norma concreta
     **sólo cubre lo cacheado** ⇒ hace falta la marca de procedencia OCR del patrón `P21`
     (`kancelaria-lex`) y una política de caché explícita.
   - `mcp-dof` depende de una **API oficial no documentada** mapeada por sondeo ⇒ monitor de
     contrato y pruebas de regresión contra endpoints reales.
3. **SEPARAR FUENTE OFICIAL DE AGREGADOR, por contrato.** `jurismcp` ya lo hace (marca
   Jurisprudencias.ai como agregador de terceros y lo deja **opt-in**) y `mcp-dir/jusbrasil-mcp`
   (MIT) es el caso contrario: agregador bien posicionado en buscadores que **parece** la capa
   oficial. ⇒ Toda herramienta MCP devuelve un campo `fonte: oficial | agregador` y el *gate* de
   citación **rechaza** lo que no sea `oficial`.
4. **CONSTRUIR sólo donde falta: AR, CL, CO, PE** — copiando `mcp-dof`, que ya resolvió el patrón
   duro «boletín oficial LATAM con API no documentada». **Perú primero**, porque es donde los
   *human gates* son **reglamentarios** (Ley 31814 + reglamento vigente 22-ene-2026, deberes por
   fases sectoriales desde sep-2026) y por tanto el entregable tiene criterio de aceptación
   escrito. **Argentina con cuidado:** la obligación allí es **subnacional** (Santa Fe Decreto
   2726/2025, Prov. Buenos Aires Resolución 4/2025), así que el perímetro es provincial.
5. **CONTRIBUIR de vuelta** la profundidad de `br/`, `mx/`, `ar/` en `legal-skills-open`: Colombia,
   Perú y Rep. Dominicana están a **1 plugin** frente a los 44 de EE. UU. y Alemania.

**Y lo que ya no hace falta prometer:** el inventario de accesibilidad por fuente oficial (que el
patrón anterior ponía como primer sprint) **está hecho para Brasil y México** — lo hicieron estos
cuatro repos, y las fuentes que usan son públicas y sin clave. Queda por hacer para AR/CL/CO/PE.

**Plantilla a copiar, dos implementaciones de referencia:**

| Referencia | Qué demuestra |
|---|---|
| [`opencaselaw`](https://github.com/jonashertner/opencaselaw) (MIT+CC0) | 26 jurisdicciones subnacionales, **3 idiomas**, grafo de citas, MCP + REST + CLI + Parquet. **El caso análogo a un país federal multilingüe.** |
| [`chrisryugj/korean-law-mcp`](https://github.com/chrisryugj/korean-law-mcp) (MIT) | **42 APIs oficiales** envueltas en 10 tools, con contraste de la cita del LLM contra el texto original. |

**Cableado para Brasil (el de mayor cobertura de flujos, 15 plugins ya escritos):**

1. **Fuentes:** DJe / diarios de justicia de los tribunales, LexML Brasil, Planalto para legislación
   federal. Un conector por fuente, igual que las 42 APIs de `korean-law-mcp`.
2. **Herramientas MCP mínimas**, copiando la superficie de `opencaselaw`: `buscar_jurisprudencia`,
   `obtener_sentencia`, `resolver_cita`, `buscar_legislacao`, `obter_artigo`.
3. **`resolver_cita` es la pieza no negociable** — es lo que convierte el servidor en defensa
   frente a **AC739-2026** y a la LGPD. Sin ella es un buscador más.
4. **Plug de los flujos que ya existen:** los 15 plugins de `legal-skills-open/br/` consumen el
   servidor como fuente. Apache-2.0 en ambos lados, sin fricción de licencia.
5. **Contribuir de vuelta** la profundidad de `br/`, `mx/`, `ar/`: el repo acepta contribuciones por
   jurisdicción, y Colombia/Perú/Rep. Dominicana están a **1 plugin** frente a los 44 de EE. UU. y
   Alemania.

⚠️ **Antes de prometerlo (actualizado en el pase 6):** para **Brasil y México** la accesibilidad
está demostrada por implementación — los cuatro repos consumen fuentes públicas sin clave. Para
**AR/CL/CO/PE** sigue valiendo la advertencia original: el primer sprint es **inventario de
accesibilidad y términos de uso por fuente**, no código. Y una advertencia nueva, que es la lección
del pase: **antes de declarar que algo no existe, búsquese fuera del índice de GitHub y en el
idioma del país** (`legislação`, `jurisprudência`, `Diario Oficial`), no sólo en inglés.

## 🆕 P13 — Gate de licencia por *tag* (amplía P9, y P9 por sí solo ya no basta)

**Qué cambió:** P9 verifica la licencia de `HEAD`. **Insuficiente** — `tw-legal-rag` es MIT hasta
v1.2.2 y **Elastic License 2.0** desde v2.0.0. Un `pip install` sin pin trae la versión propietaria.

```bash
#!/usr/bin/env bash
# Verifica la licencia EN EL TAG QUE SE VA A FIJAR, no en HEAD.
# Uso: ./lic-gate.sh owner/repo v1.2.2
repo="$1"; ref="${2:-HEAD}"
for f in LICENSE LICENSE.md LICENSE.txt LICENCE COPYING LICENSE-CODE; do
  url="https://raw.githubusercontent.com/$repo/$ref/$f"
  code=$(curl -sL -o /tmp/lic -w '%{http_code}' "$url")
  [ "$code" = 200 ] || continue
  echo "== $repo@$ref  $f  $(wc -c </tmp/lic) B"
  # NO fiarse de los primeros bytes: ELv2 empieza mencionando MIT.
  grep -oiE 'Elastic License|Business Source|NonCommercial|NoDerivatives|GNU AFFERO|GNU GENERAL PUBLIC|Apache License|MIT License|CC0' /tmp/lic | sort -u
  grep -niE 'versions? (up to|prior)|continues? to apply|relicens' /tmp/lic | head -3
  exit 0
done
echo "== $repo@$ref  SIN FICHERO DE LICENCIA"
```

**Tres reglas que salen de los hallazgos de hoy, no de teoría:**

1. **No clasificar por los primeros bytes.** El LICENSE de `tw-legal-rag` **empieza mencionando
   MIT** y es ELv2. Un `head -1` lo aprueba.
2. **Buscar la cláusula de frontera temporal** (`versions up to…`, `continues to apply`): es la que
   dice que la licencia vieja sobrevive en tags viejos — y es la que permite fijar v1.2.2 y seguir
   en MIT **legítimamente**.
3. **Comparar el tamaño con el canónico.** MIT ≈ 1.069 B, Apache-2.0 ≈ 11.3 KB, AGPL-3.0 ≈ 35 KB,
   CC-BY-NC-ND ≈ 19 KB. **Un «MIT» de 4.044 B no es MIT**, y el tamaño lo delata antes que el texto.
   Fue así como salieron los dos hallazgos de licencia de este pase.

## 🆕 P14 — Revisión de contratos dentro de Word, permisiva de punta a punta

**El problema de adopción, que esta KB ya tenía identificado:** el abogado no cambia de
herramienta. El redline tiene que llegar a Word. Hasta hoy la opción con tracked changes reales
era `doc-haus` (**GPL-3.0**) o `contract-review-agent` (procedencia sin confirmar) — **ninguna apta
para producto cerrado.**

| Capa | Repo | Licencia |
|---|---|---|
| UI dentro de Word (task pane, playbooks, redacción) | [Vaquill-AI/ms-word-addin](https://github.com/Vaquill-AI/ms-word-addin) | Apache-2.0 |
| Extracción de cláusulas con trazabilidad al párrafo | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 |
| Repositorio contractual y analítica de cláusulas | [Open-Source-Legal/OpenContracts](https://github.com/Open-Source-Legal/OpenContracts) | MIT |
| PII fuera antes del modelo | [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT |
| Firma al cierre | [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | ⚠️ AGPL-3.0 |

**Cableado:** el add-in de Vaquill es la superficie (el abogado nunca sale de Word) → Presidio
redacta antes de salir → ContextGem extrae cláusulas **con el párrafo de soporte** → OpenContracts
guarda el contrato y la analítica de cláusulas para la revisión tabular de la cartera → OpenSign
cierra la firma.

⚠️ **El eslabón AGPL:** sólo OpenSign. Desplegado como **servicio separado** que se invoca por API
(no enlazado al producto) el riesgo es acotado; **enlazado, contamina.** Alternativa: integrar el
proveedor de firma que ya use el cliente y dejar OpenSign fuera del entregable.

**Por qué importa:** es el **primer camino de punta a punta de esta KB en el que todo lo que se
redistribuye es MIT/Apache-2.0** y el entregable aterriza donde el abogado ya trabaja.

## 🆕 P15 — Gate de PERTINENCIA: el control que ninguna verificación de licencia ni de estrellas sustituye

**Problema que resuelve.** Un repo puede existir, tener licencia MIT impecable y 394.928★ **y no
pertenecer a la industria**. Caso real del pase 3: un medio describió `openclaw/openclaw` como
*«proyecto open source de AI legal»*. Las tres comprobaciones de esta KB (existencia, licencia,
estrellas) **pasan limpias**; su propia descripción es *«The AI that really does things. Any OS.
Any Platform. The lobster way. 🦞»* — **cero términos jurídicos**. Habría entrado como la fila más
prominente y más errónea de la KB. **La verificación de existencia no detecta errores de
pertinencia: son canales distintos y hacen falta los dos.**

```bash
#!/usr/bin/env bash
# relevance-gate.sh — ¿este repo habla de MI industria, en SUS propias palabras?
# Uso: ./relevance-gate.sh owner/repo "legal|law|contract|court|jurisprud|compliance"
# NO -e: grep sin match y curl con SIGPIPE son RESULTADOS, no fallos del script.
set -uo pipefail
SLUG="$1"; TERMS="$2"

DESC=$(gh api -X GET search/repositories -f q="repo:$SLUG" \
         --jq '.items[0] | "\(.description // "") \(.topics|join(" "))"' 2>/dev/null || true)
README=$(curl -sL --max-time 25 "https://raw.githubusercontent.com/$SLUG/HEAD/README.md" || true)

# (1) \b: palabra completa. Sin esto, "openclaw" contiene "law" y pasa el gate.
# (2) El NOMBRE del repo se excluye a proposito: es donde viven esas colisiones.
hits() { printf '%s' "$1" | grep -ioE "\\b(${TERMS})\\b" | tr 'A-Z' 'a-z' | sort -u | tr '\n' ' '; }
DHITS=$(hits "$DESC"); RHITS=$(hits "${README:0:4000}")
NDESC=$(printf '%s' "$DHITS" | wc -w)

# (3) >=2 terminos distintos en description/topics: una sola mencion suele ser incidental
#     ("Legal free LLM APIs" en un repo de coding).
if [ "$NDESC" -ge 2 ]; then
  echo "OK       $SLUG — $NDESC terminos en description/topics: $DHITS"; exit 0
elif [ "$NDESC" -eq 1 ] || [ -n "$RHITS" ]; then
  echo "REVISAR  $SLUG — senal debil (desc:[$DHITS] readme:[$RHITS]) -> leer antes de admitir"
  echo "         description propia: ${DESC:-<vacia>}"; exit 2
else
  echo "RECHAZAR $SLUG — ningun termino de la industria como palabra completa"
  echo "         description propia: ${DESC:-<vacia>}"; exit 1
fi
```

**Salida medida hoy (el gate se probó, no se propuso):**

```
RECHAZAR docling-project/docling   — ningun termino como palabra completa   (correcto: es infra horizontal)
REVISAR  openclaw/openclaw         — desc:[] readme:[contract]              (correcto: no se admite solo)
REVISAR  mvalentsev/awesome-free-ai-coding — desc:[legal]                   (correcto: "Legal free LLM APIs")
OK       thomasunise/casecite      — 3 terminos: caselaw law legal
OK       stella/stella             — 2 terminos: law legal
```

**Las tres decisiones de diseño, y cada una salió de un fallo real al probarlo:**

1. 🔴 **`\b` (palabra completa) es obligatorio: sin él, el gate aprueba justo el caso que lo
   motiva.** La primera versión de este script **aceptó `openclaw`** — porque la cadena
   `openc·law` **contiene «law»**. Un gate de pertinencia que valida por subcadena se rompe con
   los nombres de proyecto, que es precisamente donde viven las colisiones. Por eso el script
   **excluye el nombre del repo** y sólo mira `description` y `topics`.
2. **Se exigen ≥2 términos distintos en `description`/`topics`.** Con uno solo, `grep` acierta y
   el sentido falla: `awesome-free-ai-coding` dice *«**Legal** free LLM APIs»* — término correcto,
   industria equivocada. Dos términos distintos es la frontera que separó limpiamente los 6 casos
   probados.
3. **Tres salidas, no dos** (`OK` / `REVISAR` / `RECHAZAR`, exit 0/2/1). El gate **no decide**:
   descarta lo evidente y **pone la `description` del propio repo delante de quien decide**. Con
   la descripción de openclaw a la vista (*«The AI that really does things… The lobster way 🦞»*)
   el rechazo cuesta dos segundos; sin ella, 394.928★ invitan a buscarle un hueco.

⚠️ **Modos de falso negativo conocidos — por eso este gate filtra ALTAS, nunca poda filas vivas:**
- **Palabras compuestas.** `betagouv/mon-entreprise` sale `REVISAR` con un solo término porque su
  topic es **`legaltech`**, y `\blegal\b` no casa dentro de `legaltech`. ⇒ La cobertura del gate
  **es exactamente la calidad de la lista de términos**; incluir las formas compuestas
  (`legaltech`, `legal-ai`, `caselaw`).
- **Infraestructura horizontal admitida a propósito.** `docling` sale `RECHAZAR` y **está bien
  que salga así**: entró en la KB como capa de parsing, no como activo legal. Aplicar el gate a
  **una fila que se presenta como activo del vertical**, no a la infraestructura transversal.
- **Repos sin descripción.** `Paparusi/legal-ai-agent` (MIT, 214★) no declara descripción: el gate
  no puede pronunciarse y la fila entra como **candidato a auditar**, nunca como recomendación.

4. **Registrar el rechazo con su motivo** (como se hizo con `openclaw` en `agents/trending.md`),
   porque si no, el siguiente pase lo «descubre» otra vez por las estrellas.

---

## 🆕 P16 — Resolver procedencia: renombrado, copia o espejo (identidad de HEAD)

**Problema que resuelve.** Tres preguntas que ni la API de búsqueda ni `raw` responden por
separado: *¿este slug sigue siendo el canónico?*, *¿estos dos repos parecidos son el mismo?*,
*¿cuál de las N copias es el original?* En el pase 3 este patrón corrigió un slug muerto que el
pase 2 había dado por bueno y **desbloqueó** un activo que una cautela excesiva había congelado.

```bash
#!/usr/bin/env bash
# provenance.sh — identidad de HEAD + titular del copyright
# Uso: ./provenance.sh owner/repo-a owner/repo-b [owner/repo-c ...]
set -uo pipefail
for SLUG in "$@"; do
  SHA=$(GIT_TERMINAL_PROMPT=0 timeout 60 git ls-remote "https://github.com/$SLUG" HEAD 2>/dev/null | cut -f1)
  if [ -z "$SHA" ]; then printf '%-40s NO EXISTE (o es privado)\n' "$SLUG"; continue; fi
  API=$(gh api -X GET search/repositories -f q="repo:$SLUG" \
          --jq '"\(.items[0].stargazers_count)* \(.items[0].license.spdx_id) push=\(.items[0].pushed_at[0:10])"' 2>/dev/null)
  # gh escribe el cuerpo del error en STDOUT: sin esto, un 422 vuelca 300 B de JSON en la columna.
  case "$API" in ''|*'Validation Failed'*) API="no-buscable(422)";; esac
  L=""
  for F in LICENSE LICENSE.md LICENSE.txt LICENCE COPYING; do
    L=$(curl -sfL --max-time 20 "https://raw.githubusercontent.com/$SLUG/HEAD/$F" || true)
    [ -n "$L" ] && break
  done
  # OJO: $(...) se come el \n final, asi que estos bytes son 1 menos que `wc -c < fichero`.
  # OJO: en Apache-2.0 la primera linea "Copyright" es BOILERPLATE, no el titular:
  #      el titular va en NOTICE. Este campo solo identifica autor en MIT/BSD/ISC.
  printf '%-40s %s  %-30s %6sB  %s\n' "$SLUG" "${SHA:0:10}" "$API" \
    "$(printf '%s' "$L" | wc -c)" "$(printf '%s' "$L" | grep -i -m1 -o 'Copyright.*' | head -c 40)"
done
```

**Cómo se lee la salida:**

| Observación | Conclusión |
|---|---|
| Dos slugs, **mismo SHA** | **Es el mismo repositorio**: renombrado o espejo. Prueba criptográfica, no parecido. |
| Dos slugs, **SHA distinto**, misma frase de README | **Copia/fork divergente.** Si el original es Apache-2.0/MIT, hay **obligación de atribución** que el derivado puede no estar declarando. |
| Slug viejo **422 en API + 200 en `raw` + SHA = al del nuevo** | **Renombrado.** No es «repo no indexado» — ese diagnóstico costó al pase 2 un slug muerto con liveness falsa. |
| `git ls-remote` **vacío** + `raw` 404 | **No existe.** (`gh api repos/<slug>` **no** vale: da 403 para todo repo no adjunto, incluso existiendo.) |
| N slugs, mismo SHA, **mismo titular de copyright** | **Un codebase espejado por un autor.** Riesgo de licencia ≈ 0; el riesgo real es **de cadena de suministro** (¿quién controla el próximo commit?) ⇒ **fijar tag/SHA y mirrorizar**, no descartar. |

> 📌 **Por qué importa calibrar la cautela en las dos direcciones.** El pase 2 produjo los dos
> errores simétricos: una advertencia **insuficiente** («activo») que dejó pasar un repo dormido
> con slug muerto, y una advertencia **excesiva** («autoría sin determinar») que congeló el único
> *practice management* permisivo de la KB. **Las dos se resuelven con este mismo script de dos
> llamadas.** Una cautela mal calibrada no es gratis: cuesta credibilidad en un sentido y
> oportunidad en el otro.

---

## 🆕 P17 — Arquitectura defendible en Brasil: el límite es el ejercicio de la profesión, no el AI Act

**Problema que resuelve.** En Brasil **no hay ley general de AI**, así que el riesgo no llega por
donde casi toda propuesta lo anticipa. Llega por el **estatuto de la abogacía**: el Consejo Federal
de la **OAB** autorizó en **ago-2026** demandar a empresas de AI que realicen **actos reservados a
la abogacía**, y la **OAB-SP presentó acción civil pública contra «Enter» (Talisman AI) el
7-oct-2026**. ⇒ El requisito no es «cumplir una norma de AI»: es **poder demostrar que un abogado
identificado ejerce el juicio profesional y firma**.

**Receta — tres obligaciones de ingeniería, con los repos de esta KB:**

1. **Gate humano no evitable antes de cualquier entrega** —
   [`AnttiHero/lavern`](https://github.com/AnttiHero/lavern) (Apache-2.0, 326★): los hallazgos
   críticos **no se entregan sin aprobación humana**. Es la pieza que materializa «asiste, no
   sustituye» en código y no en marketing. Configurar el gate como **bloqueante por tipo de
   documento**, no como aviso descartable.
2. **Registro de atribución por entregable** — quién revisó, cuándo, qué citas se resolvieron y
   contra qué fuente. Usar la verificación ejecutable de **P10** y persistir **el resultado**
   (cita → fuente → veredicto → revisor → timestamp). **La prueba es el log, no la política.**
3. **Documento final desde plantilla determinista, no desde generación libre** —
   [`jhpyle/docassemble`](https://github.com/jhpyle/docassemble) (MIT, 1.015★). El documento sale
   de una plantilla auditable; la AI prepara insumos y el abogado decide. Es el patrón que un
   regulador sabe inspeccionar. Para el cálculo normativo, el modelo a imitar es
   [`betagouv/mon-entreprise`](https://github.com/betagouv/mon-entreprise) (MIT): **reglas
   ejecutables**, mantenidas por el propio Estado.

**Capa de datos (no portable entre países, y esto es lo que más se subestima):** el derecho
procesal **varía sustancialmente** entre Brasil, México y Colombia, así que el corpus y el flujo se
construyen **por jurisdicción**. Cobertura real medida en `legal-skills-open` (Apache-2.0 **sobre
el contenido**): **BR 15 plugins, AR 2, MX 2, CO 1, PE 1, DO 1** — asimetría de 15× dentro del
mismo bucket «LATAM». Plantilla para construir la pieza que falta: **P12**.

🔴 **Contraindicación explícita, y es la parte que hay que decirle al cliente:** un producto de AI
legal **dirigido al cliente final** en Brasil no es un riesgo teórico — **es la conducta que la OAB
está demandando ahora mismo**. El producto se dirige **al abogado o al tribunal**, nunca al
justiciable sin abogado en medio.

⚠️ **Y en México, un punto contractual que no es técnico:** la **Suprema Corte resolvió que el
contenido generado por AI no tiene derecho de autor** (la autoría se limita a personas humanas).
Un entregable generado por AI **puede no ser protegible**: estructurar y documentar la aportación
humana para que el resultado sí lo sea, y decirlo en la propuesta.

---

## Nota sobre este fichero

Las nueve recetas nombran **repos verificados el 2026-11-20 por doble canal** (API de búsqueda de
GitHub + lectura del fichero de licencia). Ninguna receta nombra un componente sin licencia leída.

**Cambios de este pase:** P1–P6 corrigen los **dos slugs obsoletos** (`microsoft/presidio`,
`JSv4/OpenContracts`) que arrastraban todas las recetas; **P5 cambia de componente principal**
porque los tres LLM chinos sobre los que se construía están dormidos 16–27 meses; **P6 pierde CUAD**
(el repo ya no existe) y se sustituye por un ground truth generado desde plantillas del Accord
Project; **P2 se reencuadra por calendario** porque el plazo de marcado del EU AI Act está a 12
días; y se añaden **P7** (la plaza vacía de jurisdicción en LATAM), **P8** (citation integrity como
producto) y **P9** (la auditoría de licencia mecánica que produjo las correcciones de este pase).


## 🆕 P18 — Censo de clúster de nombre: contar ANTES de escribir «el» repo

**Problema que resuelve.** P16 contesta *¿estos N slugs son el mismo repo?* pero **no** contesta
*¿cuántos repos se llaman así?*, y esa es la pregunta que decide si el nombre identifica algo. En
este pase el censo devolvió **113 repositorios llamados `LawLink`** — el pase 3 había razonado sobre
**tres**, sacados de una sola búsqueda web, y publicó «procedencia resuelta».

```bash
#!/usr/bin/env bash
# name-census.sh — ¿cuántos repos comparten este nombre, y cuál es el único con señal?
# Uso: ./name-census.sh LawLink
set -uo pipefail
NAME="$1"
TOTAL=$(gh api -X GET search/repositories -f q="$NAME in:name" --jq '.total_count' 2>/dev/null)
echo "=== '$NAME' in:name  ->  total_count = ${TOTAL:-ERROR}"
# Regla: >1 obliga a llevar siempre el owner. >20 es un comunal: el nombre no identifica nada.
gh api -X GET search/repositories -f q="$NAME in:name" -f per_page=30 \
  --jq '.items[] | [.full_name, (.stargazers_count|tostring)+"*",
                    (.license.spdx_id // "NONE"), .pushed_at[0:10]] | @tsv' 2>/dev/null |
while IFS=$'\t' read -r SLUG STARS LIC PUSHED; do
  # El filtro que importa: licencia Y estrellas Y actividad. Los tres a la vez.
  FLAG="   "
  [ "$LIC" != "NONE" ] && [ "${STARS%\*}" -ge 10 ] && [ "$PUSHED" \> "2026-05-01" ] && FLAG=">>>"
  printf '%s %-42s %-8s %-12s %s\n' "$FLAG" "$SLUG" "$STARS" "$LIC" "$PUSHED"
done
```

**Lectura del resultado.** `>>>` marca candidatos con las tres señales. En `LawLink` **sólo
`lawflow-boop/LawLink` queda marcado** de 30 inspeccionados; la única otra con licencia
(`NovaLynk/LawLink`, MIT) está muerta desde 2023-12-01 y el resto son 0–1★ sin licencia.

**Cómo se combina con los patrones que ya existen — el orden importa y es este:**

| Orden | Patrón | Pregunta que cierra |
|------:|--------|---------------------|
| 1 | **P18** (este) | ¿cuántos repos se llaman así? ⇒ ¿puedo decir «el» X? |
| 2 | **P15** gate de pertinencia | ¿habla de mi industria en *sus* palabras? |
| 3 | **P16** identidad de HEAD | ¿estos slugs concretos son el mismo árbol? |
| 4 | **P9/P13** gate de licencia | ¿puedo distribuirlo, en el tag que voy a fijar? |

**Ejecutar P18 primero no es cosmético:** P16 sobre un conjunto incompleto **produce una conclusión
verdadera sobre los slugs que recibió y falsa sobre el proyecto**, y se publica con la misma
confianza. Fue lo que pasó: el cuarto slug (`appleoppa/LawLink`, HEAD `535a3531…`) **es una
bifurcación divergente real** y refuta la frase «ni una bifurcación divergente» del pase 3.

### 🔴 Y el control que refuta la lectura ingenua de este patrón (medido en el mismo pase)

Antes de dar por bueno «muchos repos con el nombre ⇒ nombre inútil», se corrió P18 sobre un
**flagship** de esta KB:

```
docassemble in:name  →  total_count = 1444      (!!)
LawLink    in:name   →  total_count =  113
```

**1.444 > 113, y `docassemble` es el estándar de facto de access-to-justice.** Si `total_count`
alto significara «nombre que no identifica nada», este patrón acabaría descalificando al mejor
activo del fichero. **Hay que mirar la FORMA del resultado, no el número.** Medida:

| | `LawLink` (113) | `docassemble` (1.444) |
|---|---|---|
| Quién tiene el nombre **desnudo** | **muchos**, todos ~0★ | **uno**: `jhpyle/docassemble`, **1.015★** |
| Cómo se llaman los demás | **`LawLink` otra vez**, idéntico | **`docassemble-<extensión>`**: `-AssemblyLine`, `-ALWeaver`, `-docusign`, `-MAEvictionDefense`… |
| Qué es | **comunal de nombre**: reimplementaciones independientes de un nombre genérico | **ecosistema de paquetes**: un proyecto más sus extensiones |
| Qué dice el `total_count` | el nombre **no identifica nada** | el nombre identifica **muchísimo** |

> 🔧 **DISCRIMINADOR MECÁNICO, Y ES EL VERDADERO CONTENIDO DE P18.** `total_count` alto tiene **dos
> significados opuestos** y se distinguen sin leer código:
> 1. **¿Hay un repo que tenga el nombre DESNUDO con estrellas dominantes?** Sí ⇒ ecosistema. No ⇒ comunal.
> 2. **¿Los demás repiten el nombre EXACTO, o lo extienden con separador (`-`, `_`)?** Repiten ⇒ comunal. Extienden ⇒ ecosistema.
>
> **Un `total_count` alto con forma de ecosistema es una señal de SALUD** —mide el tamaño de la
> comunidad de extensiones— **y debería subir la confianza en el activo, no bajarla.** Es el único
> patrón de este fichero donde la misma medición, según su forma, apoya conclusiones contrarias.

> ⚠️ **Caveat asimétrico, para no sobrecorregir.** Un `total_count` alto **no** desacredita al
> candidato: `lawflow-boop/LawLink` sigue siendo MIT, con 110★ y commits de noviembre. Lo que
> desacredita es **haber escrito «el» sin haber contado.** Y al revés, `total_count=1` es una
> señal fuerte y gratuita de nombre propio defendible.

---

## 🆕 P19 — Expediente de clasificación y registro CNJ 615/2025 (Brasil, y el plazo ya venció)

**Problema que resuelve.** Un tribunal o un órgano público brasileño que ya usa AI está **fuera de
plazo**: la **Resolução CNJ nº 615/2025** dio **12 meses de adaptación que terminaron en marzo de
2026** con obligación de **registrar los sistemas en uso**. Esto no es un *gap* anticipado como el
Anexo III europeo de dic-2027: es un **pasivo vencido**, y el entregable es un expediente, no una
hoja de ruta. Complementa **P17** (que cubre el despacho privado, donde el límite es el ejercicio
de la profesión) y **P2** (asistente defendible bajo EU AI Act).

**Composición, toda con piezas que ya están en esta KB:**

1. **Inventario de sistemas** — un sistema por ficha: finalidad, datos de entrada, salida y **si la
   salida influye en una determinación jurídica o sólo asiste a revisión humana**. Esa frontera es
   literalmente la misma que separa el Anexo III europeo, así que **la ficha se escribe una vez y
   sirve para las dos jurisdicciones** (ver la tabla de relojes en `intel/market.md` → LATAM).
2. **Clasificación alto/bajo riesgo** según la Resolución, y **descarte explícito** de todo uso que
   **impida la supervisión humana** — que la Resolución **prohíbe en absoluto**, no regula.
3. **Supervisión humana como mecanismo, no como declaración** — `AnttiHero/lavern` (Apache-2.0):
   *human gates* obligatorios, los hallazgos críticos no se entregan sin aprobación. Es la pieza que
   convierte «hay supervisión humana» en un artefacto auditable: **un log de aprobaciones**.
4. **Verificación de cita ejecutable** — `jonashertner/opencaselaw` (MIT + CC0) como **plantilla** de
   `resolve` de citas, y el MCP de la fuente oficial de la jurisdicción. Toda afirmación del sistema
   que cite jurisprudencia tiene que poder contrastarse contra el texto. Ver **P10**.
5. **Anonimización antes de cualquier llamada externa** — `data-privacy-stack/presidio` (MIT).
6. **Trazabilidad de la extracción** — `shcherbak-ai/contextgem` (Apache-2.0): devuelve el párrafo
   de origen, que es lo que hace revisable la ficha del punto 1.
7. **Gate de licencia sobre todo el árbol entregado** — **P9** y, si se fijan tags, **P13**. Un
   expediente de cumplimiento entregado con una dependencia AGPL mal declarada es un hallazgo.

**Por qué este patrón se vende solo y por qué conviene secuenciarlo primero.** El trabajo 1–3 es
reutilizable **hacia arriba**: sirve para el Anexo III europeo de dic-2027. Lo hecho para un cliente
de North America **no** sirve para Brasil (allí no hay obligación vinculante que obligue a producir
nada: 43% de los despachos ni siquiera tiene política de AI). ⇒ **La asimetría favorece empezar por
Brasil**, que es lo contrario de como se suele secuenciar un rollout regional.

**Dónde está el riesgo de este patrón, dicho antes de que lo diga el cliente.** La Resolución aplica
al **Poder Judicial**, no al despacho privado; y **178 iniciativas de AI** ya censadas por el CNJ en
2024 son **mayoritariamente predictivas o analíticas**, no generativas — así que el inventario del
punto 1 va a encontrar sistemas **anteriores** a la ola de LLMs, que son los que peor documentados
están y los que más probablemente caigan en «influye en una determinación».

---

## 🆕 P20 — Despacho permisivo de punta a punta (la receta que **no se podía escribir** hasta este pase)

**Por qué es nueva:** esta KB declaraba abierto el hueco de *practice management* permisivo, así
que todas las recetas anteriores empezaban en el documento. Con `Kourti` (MIT) verificado, la
receta puede empezar en **el expediente y el plazo**, que es donde empieza el despacho.

| Paso | Pieza | Licencia | Qué aporta |
|---|---|---|---|
| 1 | [boyeesu/Kourti](https://github.com/boyeesu/Kourti) | **MIT** | Columna vertebral: **matters, documentos, clientes, plazos**. React + Node + PostgreSQL, `docker compose up --build`. |
| 2 | [docling-project/docling](https://github.com/docling-project/docling) | MIT | Ingesta y parsing (el cuello de botella real, ver `repos/foundations.md`). |
| 3 | [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT | **De-identificar PII antes de cualquier egreso** a un LLM externo. Sin esto no hay despliegue defendible bajo GDPR/LGPD. |
| 4 | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | Extracción tipada (*aspects/concepts*) **con trazabilidad al párrafo de origen**. |
| 5 | [thomasunise/casecite](https://github.com/thomasunise/casecite) | Apache-2.0 | Cada afirmación contrastada contra el pasaje que cita + *tabular review*. |
| 6 | [Vaquill-AI/ms-word-addin](https://github.com/Vaquill-AI/ms-word-addin) | Apache-2.0 | El canal que decide la adopción: **Word**, con redline y playbooks. |
| 7 | [meta-models/legal-agent-workshop](https://github.com/meta-models/legal-agent-workshop) | **MIT** | Patrón de la **capa de verificación fuera del control del agente** + firma del abogado. Se copia la arquitectura, no el caso. |

**Cableado concreto.** `Kourti` es el sistema de registro y **dueño del `matter_id`**. Todo lo demás
cuelga de ese id:

```
Kourti (matter_id, cliente, plazo)
  └─ docling  ──► texto + estructura        [por documento del matter]
       └─ presidio ──► texto de-identificado   [ANTES de salir del perímetro]
            └─ contextgem ──► conceptos tipados + offset de origen
                 └─ casecite ──► cada claim atado a su pasaje
                      └─ verificación (patrón legal-agent-workshop):
                           corre FUERA del agente; si un claim no resuelve ──► no se entrega
                                └─ Word add-in ──► redline al abogado ──► firma  ──► Kourti
```

⚠️ **Las tres advertencias que hay que decirle al cliente, no esconder:**
1. **`Kourti` tiene 1★.** Se forkea, se fija el commit y **se asume mantenimiento**. Es base de
   partida, no proveedor.
2. **No trae trust accounting ni control de conflictos de interés** — las dos cosas que un colegio
   de abogados mira primero. Hay que construirlas o integrarlas (el único candidato con trust
   accounting, **Kosmos**, es AGPL-3.0).
3. **Auditar antes de proponer.** Este pase verificó licencia, existencia y alcance; **no** auditó
   seguridad ni calidad de código.

## 🆕 P21 — Soberanía del dato **impuesta por la red**, no prometida en el README (patrón `kancelaria-lex`)

**El problema:** «on-premise» y «local-first» son afirmaciones de marketing que un auditor no puede
verificar. Bajo EU AI Act / GDPR / LGPD lo que hay que poder demostrar es que **no existe ruta** de
salida, no que nadie la use.

**La implementación de referencia, permisiva y legible:**
[AI4CharityPL/kancelaria-lex](https://github.com/AI4CharityPL/kancelaria-lex) (**MIT**, 1.069 B).

| Control | Cómo lo hace | Por qué es auditable |
|---|---|---|
| **Sin egreso** | **cuatro segmentos Docker, tres con `internal: true`** | `internal: true` elimina la ruta al gateway **a nivel de red**. Se verifica leyendo el compose, no confiando en el código. |
| **Cita verificada por construcción** | el código **reconstruye el texto desde el documento fuente** y compara **carácter a carácter** | una cita fabricada **no puede** pasar el verificador. Declara **0 inconsistencias en todas las corridas**, >80% de precisión (vs **17–34%** de fabricación en comerciales). |
| **Procedencia del OCR** | Tesseract local, **marcador permanente**, cada cita derivada muestra `z OCR` | distingue *«apunta a un carácter del expediente»* de *«apunta a un carácter de **la lectura de un escaneo**»*. **Ninguna otra pieza de esta KB hace esta distinción.** |
| **Identidad** | perfiles locales con contraseña y **TOTP** opcional | control de acceso sin IdP externo. |

**Receta de reutilización** (el patrón es replicable a cualquier jurisdicción; sólo el corpus es
polaco):

```bash
# 1. El control que hace defendible todo lo demás: verificar que NO hay ruta de salida.
#    Si un servicio que toca texto de cliente no esta en un segmento internal, el diseño miente.
docker compose config | python3 -c "
import sys,yaml
c=yaml.safe_load(sys.stdin)
nets=c.get('networks',{}) or {}
internal={n for n,v in nets.items() if (v or {}).get('internal')}
print('segmentos internal:', sorted(internal) or 'NINGUNO  <-- BANDERA ROJA')
for svc,v in (c.get('services') or {}).items():
    sn=set((v.get('networks') or {})) or {'<default>'}
    fuera=sn-internal
    print(f'{svc:28s} redes={sorted(sn)}  {\"EGRESO POSIBLE <--\" if fuera else \"sin egreso\"}')
"
# 2. Sustituir el corpus jurisdiccional, conservando el verificador:
#    PL -> korean-law-mcp (KR) / opencaselaw (CH) / ayunis-legal-mcp (DE) / mcp-legal-it (IT)
#    LATAM: no existe todavia ningun MCP de fuentes oficiales -> ver P12 (ese es el hueco real)
```

⇒ **Esto es lo que convierte el argumento de soberanía EMEA en una demostración de 10 minutos**
delante de un DPO, en vez de una diapositiva.

## 🆕 P22 — Barrido de **estructura** de tabla (G-L11): el control que ningún pase tenía, y es gratis

**El fallo que detecta:** una línea en blanco dentro de una tabla Markdown la **parte en dos**. Las
filas de abajo quedan **sin cabecera**, así que el compilador o las pierde o **convierte la primera
fila en nombres de columna** — el fallo «cabecera como dato» que el brief prohíbe explícitamente.

**Por qué los controles existentes no lo ven:** todos (licencia, pertinencia P15, censo de nombre
P18, checksum 932-G1) validan **filas**. Ninguno valida **la tabla que las contiene**. En este pase
el defecto estaba en las 7 filas que el pase 4 **auditó una por una y declaró correctas** — y lo
eran: *el defecto estaba en el carácter que las separaba de su cabecera.*

```bash
# table-structure.sh — 0 llamadas de red. Correr en las 12 industrias antes de cada commit.
python3 - <<'PY'
import re,glob,sys
bad=0; tot=0
for f in sorted(glob.glob('*/*.md')):
    L=open(f,encoding='utf-8').read().split('\n'); i=0
    while i<len(L):
        if L[i].lstrip().startswith('|'):
            s=i; blk=[]
            while i<len(L) and L[i].lstrip().startswith('|'): blk.append(L[i]); i+=1
            tot+=1
            sep=len(blk)>1 and re.match(r'^\|[\s:|-]+\|?\s*$',blk[1].strip())
            cols=[len(re.split(r'(?<!\\)\|',b.strip().strip('|'))) for b in blk]
            data=[c for c,b in zip(cols,blk) if not re.match(r'^\|[\s:|-]+\|?\s*$',b.strip())]
            if not sep:
                print(f'{f}:{s+1}  SIN FILA SEPARADORA -> tabla sin cabecera ({len(blk)} filas huerfanas)'); bad+=1
            elif len(set(data))>1:
                print(f'{f}:{s+1}  COLUMNAS INCONSISTENTES: {sorted(set(data))}'); bad+=1
        else: i+=1
print(f'--- {tot} bloques de tabla, {bad} defectos ---')
sys.exit(1 if bad else 0)
PY
```

**Resultado en esta KB tras la reparación: 86 bloques, separadora en todos, 0 mismatches.**
⚠️ **Y una trampa que este script encontró en su propia documentación:** una barra vertical dentro
de *inline code* (`` `|` ``) **parte la celda igual** en GFM. En una celda de tabla hay que
escaparla como `\|`.

## 🆕 P23 — Descubrimiento **sin falso negativo**: dejar de usar filtros de precisión como filtros de cobertura

**El fallo que corrige (G-L10):** el pase 4 declaró *««Kourti Legal» no existe»* sobre un repo que
existe, es MIT y tiene 524 refs. Vio **1★** y concluyó inexistencia. El gate de pertinencia **P15**
de esta KB **también** lo rechaza, porque el repo no tiene `description` ni `topics`.

🔑 **La distinción que hay que internalizar:**

| Filtro | Para qué **sirve** | Para qué **no sirve** |
|---|---|---|
| Estrellas, `description`, `topics`, ranking de búsqueda | **PRECISIÓN**: descartar ruido de una lista ya obtenida | **COBERTURA**: decidir qué mirar, o concluir que algo no existe |
| `git ls-remote` (refs), bytes de LICENSE, lectura del README | **EXISTENCIA y NATURALEZA** del artefacto | medir tracción o madurez |

```bash
# discover.sh — buscar por FUNCION, no por popularidad. Uso: ./discover.sh "practice management" "matters|deadlines|trust accounting"
set -u
FUNC="$1"; TERMS="$2"
# (1) Candidatos SIN umbral de estrellas y SIN sort=stars (el ranking es el sesgo).
gh api -X GET search/repositories -f q="$FUNC" -f per_page=100 \
  --jq '.items[] | [.full_name, (.stargazers_count|tostring), ((.license.spdx_id)//"NONE")] | @tsv' > /tmp/cand.tsv
# (2) Y el canal que esta KB no usaba: directorios de terceros. Dan nombres, no verdades.
echo "MANUAL: buscar '$FUNC open source self-hosted' en agregadores; extraer NOMBRES, verificar aqui."
# (3) Verificar cada candidato por EXISTENCIA, no por senal social.
while IFS=$'\t' read -r slug stars lic; do
  refs=$(git ls-remote "https://github.com/$slug" 2>/dev/null | wc -l)
  [ "$refs" -eq 0 ] && continue                       # no existe de verdad
  rm -f /tmp/L; code=$(curl -sL -o /tmp/L -w '%{http_code}' --max-time 20 \
      "https://raw.githubusercontent.com/$slug/HEAD/LICENSE")
  bytes=$([ "$code" = 200 ] && wc -c < /tmp/L || echo 0)
  readme=$(curl -sL --max-time 20 "https://raw.githubusercontent.com/$slug/HEAD/README.md" || true)
  # pertinencia por el README (NO por description/topics: ahi viven los falsos negativos)
  hits=$(printf '%s' "$readme" | grep -ioE "$TERMS" | sort -u | wc -l)
  printf '%-45s %5s★ lic=%-12s bytes=%-6s refs=%-5s terminos=%s\n' "$slug" "$stars" "$lic" "$bytes" "$refs" "$hits"
done < /tmp/cand.tsv
```

⇒ **Y la regla de redacción que se deriva:** un hueco sólo puede declararse como *«no existe X
permisivo»* si se buscó por función fuera de GitHub. En otro caso se escribe **«no existe X
permisivo con señal social»**, que es lo que realmente se midió. En el pase 5 se reescribieron en
ese sentido **los dos huecos de `verticals/solutions.md`** (practice management, cerrado; firma
electrónica, confirmado abierto sobre los tres mayores). **Los huecos declarados en `agents/top.md`,
`repos/foundations.md` e `intel/trends.md` siguen redactados en la forma fuerte y están pendientes
de rerevisión con P23** — en particular el de **MCP de fuentes oficiales LATAM**, que es el más
citado de esta KB y nunca se buscó fuera de GitHub.

---

## 🆕 P24 — **Sonda de canal**: el control que va *antes* de todos los demás (gratis, 6 llamadas)

**El problema que resuelve.** Esta KB prescribió en el pase 3 `git ls-remote` como oráculo de
existencia y de renombrado «para toda la rotación», y en el pase 5 `gh api search/repositories`
como fuente de ★/SPDX/`pushed_at`. **Hoy los dos están muertos** (0 refs para todo; HTTP 422), y un
canal muerto **no devuelve un error legible: devuelve «no existe» para todo**. Un pase que herede
los canales del anterior sin sondearlos convierte un fallo de infraestructura en una tabla de
hallazgos. Es el mismo error que G-L12, un nivel más abajo: allí el canal estaba *sesgado*, aquí
está *roto*.

**La regla:** todo canal se sonda con un **par conocido-bueno / conocido-malo** antes de usarse. El
conocido-malo es un slug **inventado** (no un repo archivado: un repo archivado existe).

```bash
#!/usr/bin/env bash
# P24 — sonda de canal. GOOD debe existir; BAD debe ser inventado.
GOOD="suffolkLITLab/docassemble-AssemblyLine"
BAD="gmilano/definitely-not-a-real-repo-xyz"

probe_raw(){ for f in README.md LICENSE .gitignore; do
    c=$(curl -s -o /dev/null -w '%{http_code}' --max-time 15 \
        "https://raw.githubusercontent.com/$1/HEAD/$f")
    [ "$c" = 200 ] && { echo 200; return; }; done; echo 404; }

echo "raw        good=$(probe_raw "$GOOD")  bad=$(probe_raw "$BAD")"
echo "ls-remote  good=$(git ls-remote "https://github.com/$GOOD" 2>/dev/null | wc -l)" \
     "bad=$(git ls-remote "https://github.com/$BAD" 2>/dev/null | wc -l)"
echo "search     good=$(gh api -X GET search/repositories -f q="repo:$GOOD" \
        --jq '.total_count' 2>/dev/null || echo ERR)"
echo "curl -sI   good=$(curl -sI -o /dev/null -w '%{http_code}' "https://github.com/$GOOD")" \
     "bad=$(curl -sI -o /dev/null -w '%{http_code}' "https://github.com/$BAD")"
```

**Lectura del resultado — y sólo hay tres casos:**

| Patrón | Diagnóstico | Qué hacer |
|--------|-------------|-----------|
| `good` ≠ `bad` | 🟢 El canal **discrimina** | Usable como oráculo |
| `good` = `bad` = negativo | 🔴 **Canal ciego** (403/0 refs para todo) | **Inusable.** No escribir «no existe» con él |
| `good` = `bad` = positivo | 🔴 Canal **permisivo** (todo 200) | Inusable: confirmaría repos inventados |

**Resultado medido el 2026-11-21 en esta sesión** (la tabla cambia entre sesiones, que es el punto):
`raw` 200/404 🟢 · `ls-remote` 0/0 🔴 · `search/repositories` 422 🔴 · `curl -sI` 403/403 🔴 ·
**WebFetch sobre `github.com/<slug>` 🟢** (da ★ + licencia + README: es el sustituto de
`search/repositories` cuando éste cae).

**Consecuencias que hay que escribir en el fichero, no sólo saber:**

1. `raw.githubusercontent.com` es un oráculo **positivo**: 200 prueba existencia, **404 no prueba
   inexistencia** (puede faltar ese fichero). Para negar, hacen falta varios nombres **y** un
   segundo canal.
2. **`raw` sigue los redirects de renombrado** ⇒ con `ls-remote` caído, **no hay oráculo de
   renombrado**. Entonces se escribe *«83/83 vivas, renombrados no comprobados»*, no *«83/83
   verificadas»*. La diferencia es la *promoción de suplente* que costó un líder de categoría
   entero en la KB de gaming.
3. Sin `search/repositories` **no hay `pushed_at`** ⇒ la columna de último commit va `n/d ⚠️`.
   **Nunca una fecha inferida.**

## 🆕 P25 — Matriz de descubrimiento **trilingüe por categoría** (la que habría evitado G-L12)

**El problema.** «Buscar también en español» no basta, y esta KB es la prueba: buscó *flujos* en
portugués (`agente jurídico`, `assistente`) y encontró cuatro repos LATAM reales; buscó *fuentes*
sólo en inglés (`legal MCP`, `official sources`) y declaró un cero que era falso por cuatro. **El
sesgo de idioma no es regional, es por categoría de activo.**

**La matriz.** Eje vertical = **categoría de activo**; eje horizontal = **idioma**. Se ejecuta
completa, y **cada celda vacía se escribe como cero medido, con su consulta**:

| Categoría | EN | ES | **PT** |
|-----------|----|----|--------|
| Fuentes oficiales / boletín | `official gazette MCP` | `Diario Oficial MCP`, `boletín oficial API` | `Diário Oficial MCP`, `DOU API` |
| Legislación | `statute corpus` | `legislación MCP`, `normas API` | **`legislação MCP`**, `normas.leg.br` |
| Jurisprudencia | `case law MCP` | `jurisprudencia MCP`, `sentencias API` | **`jurisprudência MCP`**, `acórdãos` |
| Flujos / agentes | `legal agent` | `agente jurídico`, `asistente legal` | `agente jurídico`, `assistente jurídico` |
| Práctica / expediente | `practice management` | `gestión de expedientes` | `gestão de processos` |

**Y la regla de canal que la acompaña (G-L12):** un enunciado de **cobertura** («no existe X»)
exige al menos un canal **fuera** del sistema que indexa X — búsqueda web, directorio de MCP,
agregador, registro de paquetes. Un enunciado de **propiedad** («X es Apache-2.0») no lo exige:
ahí el fichero de licencia es la verdad. **Esta KB aplicaba el protocolo de propiedad a enunciados
de cobertura, y lo llamaba «doble canal».**

**Dónde aplicarlo ya, en las 12 industrias:** toda frase de la forma *«no existe ningún X
permisivo para LATAM»* está pendiente de re-test. Canal externo mínimo y gratuito que funcionó
hoy: **una búsqueda web con el sustantivo en portugués**, más el directorio
[`daniel-filius/awesome-mcp-brasil`](https://github.com/daniel-filius/awesome-mcp-brasil) (CC0,
8 secciones, 13 entradas jurídico/legislativo), que es ahora un canal de descubrimiento de esta KB
y no sólo una fila.
