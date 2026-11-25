---
industry: legal
region: Global
updated: 2026-11-25
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
#    LATAM -> leis-mcp + br-eli-mcp (BR, legislacion) / jurismcp (BR, jurisprudencia) / mcp-dof (MX)
#    [CORREGIDO EN EL PASE 7: esta linea decia que no existia ninguno. Lo desmintio el PASE 6,
#     en este mismo fichero, y la afirmacion sobrevivio DENTRO del bloque de codigo. Ver G-L16.]
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

## 🆕 P26 — Correr un benchmark legal **filtrado por licencia** (la receta que convierte `LegalBench` en utilizable)

**Problema que resuelve.** `LegalBench` no tiene licencia a nivel de repositorio: la tiene **por
tarea**, y **30 de sus 162 tareas son NonCommercial** más 2 sin concesión. Correrlo entero para
sustentar un entregable de cliente usa datos NC con fines comerciales. Correrlo **filtrado** es
legítimo, y el propio repo trae el utilitario para hacerlo (`UsingLegalBench.ipynb`).

```bash
#!/usr/bin/env bash
# P26 — censo de licencias por tarea + lista de exclusion. ~162 GET a raw, 0 autenticacion.
# Generaliza a CUALQUIER repo de datos cuyo README diga "follow the license of the dataset creator".
set -euo pipefail
SLUG=${1:-HazyResearch/legalbench}
DIR=${2:-tasks}
WORK=$(mktemp -d); trap 'rm -rf "$WORK"' EXIT

# (1) Enumerar los items SIN descargar los datos (clone sin blobs: arbol solamente).
git clone -q --depth 1 --filter=blob:none --no-checkout "https://github.com/$SLUG" "$WORK/r"
git -C "$WORK/r" ls-tree --name-only HEAD "$DIR/" | sed "s|$DIR/||" > "$WORK/items.txt"
echo "items: $(wc -l < "$WORK/items.txt")"

# (2) Leer la linea de licencia de cada item (en paralelo; es lo unico que cuesta red).
mkdir -p "$WORK/md"
xargs -P 10 -I{} sh -c \
  "curl -s -m 20 'https://raw.githubusercontent.com/$SLUG/HEAD/$DIR/{}/README.md' -o '$WORK/md/{}.md'" \
  < "$WORK/items.txt"

# (3) Censo + lista de exclusion. NC y "sin linea de licencia" se excluyen por igual:
#     el segundo no es un descuido, es AUSENCIA DE CONCESION.
: > "$WORK/exclude.txt"
for f in "$WORK"/md/*.md; do
  item=$(basename "$f" .md)
  lic=$(grep -m1 -oiE '\*\*License\*\*:.*' "$f" | sed 's/.*\*\*[Ll]icense\*\*: *//; s/\[//g; s/\].*//; s/ *$//')
  [ -z "$lic" ] && { echo "$item"$'\t'"(SIN LINEA DE LICENCIA)" >> "$WORK/exclude.txt"; continue; }
  case "$lic" in *NC*|*NonCommercial*|*noncommercial*) echo "$item"$'\t'"$lic" >> "$WORK/exclude.txt";; esac
  printf '%s\n' "$lic"
done | sort | uniq -c | sort -rn

echo; echo "=== EXCLUIR ($(wc -l < "$WORK/exclude.txt") items) ==="; cat "$WORK/exclude.txt"
```

**Salida medida sobre `HazyResearch/legalbench` el 2026-11-22:**

```
124 CC BY 4.0        ->  usable con atribucion
  4 MIT              ->  usable
  2 CC BY-SA 4.0     ->  usable, pero share-alike sobre el derivado
 16 CC BY-NC-SA 4.0  ->  EXCLUIR (familia learned_hands_*)
  9 CC BY-NC         ->  EXCLUIR (familia opp115_*)
  4 CC BY-NC 4.0     ->  EXCLUIR (textualism_tool_* , canada_tax_court_outcomes, consumer_contracts_qa)
  1 CC BY-NC 3.0     ->  EXCLUIR (privacy_policy_entailment)
  2 sin linea        ->  EXCLUIR (abercrombie, rule_qa)
=== 130 de 162 utilizables en un entregable comercial ===
```

**Cómo se cablea con lo que esta KB ya tiene** — evaluación de tres fuentes, declarando cuál se usó:

1. **`harvey-labs`** (MIT, 2.010 tareas, 24 áreas + contratación): banco principal. Instalar
   `lab-core` desde el wheel del release y apuntar `LAB_ROOT` al checkout de tareas.
   ⚠️ Para puntuar `.docx` hace falta la CLI **`pandoc` (GPL-2.0)**: si se empaqueta en una imagen
   de contenedor, **esa imagen redistribuye GPL-2.0**. Evaluar texto / `.xlsx` / `.pptx` no la carga.
2. **`legalbench`**, subconjunto de 130 tareas de este script: contraste académico independiente.
3. **`thunlp/CAIL`** (MIT): contraste en chino, para engagements de APAC.

Y el resultado se reporta **siempre** con la frase que lo hace defendible: *«medido sobre
`harvey-labs` v1.4.0 (benchmark de un participante del mercado) y sobre el subconjunto permisivo de
130/162 tareas de LegalBench»*. Un número de benchmark sin su procedencia **no es un dato, es una
afirmación de marketing** — incluida la nuestra.

## 🆕 P27 — G-L16: barrer las **afirmaciones obsoletas dentro de bloques de código**

**El defecto, encontrado hoy en este mismo fichero.** El `P21` del pase 6 llevaba, en el comentario
de su bloque de código:

```
#    LATAM: no existe todavia ningun MCP de fuentes oficiales -> ver P12 (ese es el hueco real)
```

**El pase 6 desmintió esa frase en el mismo pase y en los mismos ficheros** — incorporó cuatro MCP
de fuentes oficiales de Brasil y México. La afirmación sobrevivió **porque estaba dentro de un
bloque de código**, y todos los controles de esta familia de KBs (censo de licencias, de URLs, de
nombres, de estructura de tabla `P22`) **leen filas y prosa, nunca comentarios de código**.

Es la misma clase de fallo que `G-L11` — el defecto no estaba en el dato, estaba **en dónde vivía**:

| Control | Qué mira | Ciego a |
|---|---|---|
| Censo de licencias / URLs | celdas de tabla | prosa y código |
| `P22` estructura de tabla | separadores y columnas | contenido |
| `G-L7` | slugs **con** URL | slugs citados sin URL |
| 🆕 **`P27`** | **comentarios dentro de ``` ```** | — |

```bash
#!/usr/bin/env bash
# P27 — afirmaciones de AUSENCIA dentro de bloques de codigo. 0 llamadas de red.
# Correr en las 12 industrias antes de cada commit, junto con P22.
awk '
  /^[[:space:]]*```/ { inblk = !inblk; next }
  inblk && tolower($0) ~ /no existe|inexistente|no hay ning|todavia ning|aun no|hueco real|falta un/ {
    printf "%s:%d: %s\n", FILENAME, FNR, $0
  }
' */*.md
```

> ⚠️ **Este patrón se marca a sí mismo, y es correcto que lo haga.** La cita textual del defecto
> (tres párrafos más arriba) y el propio regex del script contienen las cadenas que el barrido
> busca, así que `P27` saldrá siempre con **dos positivos en `compose/patterns.md` que son la
> evidencia y la herramienta, no el defecto**. Es exactamente lo que le pasó al pase 5 al
> documentar el bug del `|` dentro de una celda: *describir el fallo lo reproduce.* **No los
> borres**: sin la cita no queda prueba de qué se corrigió.

**Resultado en esta KB el 2026-11-22:** 7 líneas marcadas, **6 falsos positivos** (son cadenas que
el propio script *imprime*: `RECHAZAR ... ningun termino`, `NO EXISTE (o es privado)`,
`NINGUNO <-- BANDERA ROJA`) y **1 defecto real**, corregido. Tasa de falsos positivos alta y coste
cero: se revisa a ojo en diez segundos.

> **La regla generalizable, que es la que hay que copiar a las doce industrias:** *un pase que
> refuta una afirmación debe buscarla **donde no la busca ningún control**: comentarios de código,
> texto dentro de bloques, notas al pie y encabezados.* Refutar un hueco en la tabla y dejarlo
> afirmado en una receta no lo cierra — **deja dos respuestas contradictorias en la misma KB, y la
> que el siguiente lector copie y pegue será la del bloque de código.**

---

## 🆕 P28 — **Puerta de pre-factura**: que no salga del despacho una línea que el cliente vaya a recortar

**Problema que resuelve, con el número delante:** el cobro cayó del 93% al 92% en 2026 mientras la
utilización subía de 39% a 42% (Clio, 26-oct-2026). Lo que se recorta se recorta por cuatro motivos
deterministas: narrativa vaga, *block billing*, aritmética que no cuadra y códigos UTBMS inválidos.

**Piezas, todas MIT y verificadas byte a byte el 2026-11-22:**

| Pieza | Repo | Papel |
|---|---|---|
| Linter de pre-factura | [kirillsakhin/billing-lint](https://github.com/kirillsakhin/billing-lint) (MIT 1.070 B) | Reglas deterministas sobre CSV/XLSX/LEDES: narrativa, duplicados, restos de plantilla, UTBMS |
| Validador de formato | [unhingedpanda/billcheck](https://github.com/unhingedpanda/billcheck) (MIT 1.080 B) | LEDES 1998B: 24 campos, ceros a la izquierda, escala decimal, aritmética exacta |
| Libro de horas | [kimai/kimai](https://github.com/kimai/kimai) (**AGPL-3.0** ⚠️ interno) | Origen de los datos: timesheets, tarifas por proyecto/actividad/usuario |
| Taxonomía de materia | [sali-legal/LMSS](https://github.com/sali-legal/LMSS) (MIT 1.073 B) | IRI estable de área/tipo de asunto para agregar por materia y cruzar con el cliente |

**Cableado, en este orden y no en otro:**

```text
Kimai (export de timesheet)
   └─> billing-lint   : reglas deterministas  -> hallazgos BLOQUEANTES y hallazgos de JUICIO
         └─> billcheck: construye el LEDES 1998B y revalida aritmética y formato
               └─> cola de revisión humana: sólo los de JUICIO
                     └─> fichero .LED firmado + informe JSON adjunto al expediente
```

**Las tres decisiones que hacen que funcione:**

1. **Determinista antes que modelo, y está medido, no supuesto.** `billing-lint` documenta que la
   revisión por LLM en lote es inconsistente: *el mismo defecto se marca en la entrada 3 y pasa
   callado en la 47, y dos ejecuciones se contradicen; 400 entradas en un prompt lo empeora*.
2. **Correr en CI sobre el export de pre-factura**, no en el momento de emitir. Un ajuste descubierto
   por el equipo de facturación del cliente **cuesta dinero y confianza**; el mismo defecto detectado
   el día 3 del ciclo no cuesta nada.
3. **`billcheck` no sube nada a ningún sitio.** Cero dependencias de runtime; su validador web liga a
   `127.0.0.1`, rechaza métodos de escritura y Host inesperado, no tiene endpoint de subida, ni
   analítica, ni cookies, y su política de contenido **bloquea las conexiones salientes del
   navegador**. Es la misma garantía *por construcción* del patrón `P21`, aplicada a la factura —
   que contiene la narrativa de lo que se hizo en cada asunto, es decir, **material privilegiado**.

**Qué hay que construir, dicho sin adornos:** la tabla de tarifas por abogado y materia, el mapeo
asunto→IRI de LMSS, y las *outside counsel guidelines* del cliente si se quiere anticipar sus cortes
(eso es `P29`). Nada de esto viene en ninguna de las piezas.

---

## 🆕 P29 — **Revisión de factura contra las guías del cliente** (el lado corporativo, que es donde está la cartera de Globant)

**Reencuadre de comprador, y es el que cambia a quién se le vende:** esta KB lleva ocho pases
escrita para el **despacho**. La factura tiene dos lados, y el otro —el **departamento legal
corporativo** que la recibe y la revisa contra sus *outside counsel guidelines*— es donde ya están
los clientes de Globant. Es la vía de entrada más caliente de todo este plano **y no requiere vender
nada a un despacho.**

**Referencia de diseño:** [manojrevenkar12-web/legal-invoice-review-agents](https://github.com/manojrevenkar12-web/legal-invoice-review-agents).
⚠️ **SIN LICENCIA — 5/5 rutas devuelven 404. Se lee, no se forkea.** Lo que aporta es su regla de
arquitectura, que es la mejor formulación del principio que esta KB venía escribiendo en prosa:

> **«Models read, rules decide.»** *Los modelos leen, las reglas deciden.*

**La arquitectura, en cuatro capas:**

1. **El modelo convierte la prosa de la guía en reglas tipadas** — y **cada regla carga una cita
   literal** del documento que se comprueba mecánicamente, más un extractor de patrones que
   contrasta los valores. **Legal operations aprueba el conjunto de reglas antes de que se use.**
2. **Un motor determinista aplica todo lo que es aritmética**: tarifas, incrementos, topes diarios,
   roles, gastos, topes de investigación, asistentes a reuniones. **El dinero que ajusta es
   reproducible al céntimo.**
3. **NLP clásico criba cada línea** —clasificadores calibrados, NER contra el listado de personal del
   despacho, modelos de materia y de horas—. **Sólo las líneas donde cabe un juicio llegan al
   modelo**, que está obligado a **citar la entrada**; un verificador **descarta toda decisión cuya
   cita o cláusula no se compruebe**.
4. **Los hallazgos de juicio son propuestas** (*block billing*, narrativa vaga, trabajo administrativo,
   reuniones internas). Una persona acepta o rechaza. **Nada de lo que dijo un modelo se aplica sin
   ese paso** — y el despacho puede **apelar** y recibir una respuesta que le cita su propia apelación.

**Piezas permisivas con las que se construye:** `billcheck` (MIT) para leer el LEDES 1998B entrante ·
`sali-legal/LMSS` (MIT) como eje de materia para agregar el gasto y que **cruce con la taxonomía del
despacho** · `billing-lint` (MIT) como banco de reglas deterministas de partida · Kill Bill
(Apache-2.0) si hace falta llevar el ajuste a un flujo de pago.

⚠️ **Lo que hay que decir en la propuesta, porque las fuentes son de parte:** los ahorros publicados
(5–10%, algún proveedor dice 15–25%) **son cifras de marketing sin fuente trazable**; una de las más
repetidas —«la revisión manual se pierde hasta el 62% de las infracciones»— **no tiene fuente
localizable**. Se mide contra la línea base del propio cliente, y no se cita ninguna de ellas.
Límite real y conocido: la revisión por línea **no ve el contexto** —estrategia del asunto,
complejidad, si el trabajo debía haberse hecho siquiera—, y eso sigue siendo humano.

---

## 🆕 P30 — **Libro de cumplimiento de honorarios en la era AI** (ABA 512 / Regla 1.5), y sirve dos veces

**Obligación que cubre, y no es futura:** sólo se factura el tiempo efectivamente empleado — el
prompt y la verificación **sí**, el tiempo ahorrado **no**; una tarifa plana puede volverse
irrazonable bajo la **Regla 1.5** si la AI comprime el trabajo; el tiempo de **aprender** una
herramienta general no se repercute; el **coste de la herramienta** exige acuerdo previo. ABA Formal
Opinion 512, y en la misma línea California, Texas Op. 705, North Carolina 2024 FEO 1 y D.C. Op. 388.

**Base:** [itsoumya-d/aderant-legal-billing](https://github.com/itsoumya-d/aderant-legal-billing)
(MIT 1.071 B) — WIP por expediente, tarifarios, **libros de cuenta de cliente que no pueden quedar en
descubierto**, excepciones de compliance y export LEDES, con las fórmulas publicadas en el README
(`timeValue = round(minutes / 60 * effectiveRate)`), que es lo que lo hace auditable.

**Los cuatro controles que se añaden encima, uno por obligación:**

| Control | Qué hace | Regla que cubre |
|---|---|---|
| **Campo de herramienta por entrada de tiempo** | Cada entrada declara si intervino AI, cuál y en qué paso (redacción / revisión / verificación) | Base probatoria de todo lo demás |
| **Marcador de tarifa plana en riesgo** | Si el esfuerzo real de un asunto a tarifa plana cae por debajo del umbral que la tarifa suponía, se marca para revisión de razonabilidad | Regla 1.5 |
| **Bloqueo de tiempo de aprendizaje** | Las entradas contra herramientas de uso general marcadas como «aprendizaje» no pueden facturarse salvo petición expresa del cliente, registrada | ABA 512 |
| **Puerta de repercusión de coste** | El coste de herramienta no se añade a la factura si no existe acuerdo escrito previo en el expediente | ABA 512 |

> 🔑 **Y el motivo por el que esto se construye una vez y se cobra en dos regímenes:** el campo de
> herramienta por entrada de tiempo **es** el rastro de auditoría que el **EU AI Act** exige
> documentar — en una región donde **el 56% de los departamentos legales usa herramientas genéricas
> y sólo el 14% tiene AI legal especializada**, es decir, donde cuatro de cada cinco **no pueden
> documentar nada**. Misma pieza: Regla 1.5 en EE. UU., expediente documental en la UE, y en LATAM la
> cobertura de una responsabilidad **ya vigente** por vía colegial. **Una construcción, tres
> argumentos de venta.**

⚠️ **Límite declarado:** `aderant-legal-billing` tiene **0★, un solo autor y 16 días de vida**. Se
adopta como **base de referencia leída**, no como dependencia mantenida. Lo que se promete a un
cliente es el código que se ha leído.

---

## 🆕 P31 — **Consultar por el nombre de un estándar** (la receta que habría evitado `G-L17`)

**Fallo que corrige:** añadir la palabra del sector al nombre de un estándar sectorial **es un
filtro, no una aclaración** — y filtra precisamente los mejores activos, porque un repo que
implementa el estándar **no necesita nombrar el sector**.

**Medición que lo demuestra, tres llamadas, 2026-11-22:**

| Consulta | `total_count` | ¿Contiene el mejor activo (`billcheck`, MIT)? |
|---|---|---|
| `LEDES` | 109.739 | ❌ sepultado bajo la familia `led` (`WLED`, `FastLED`) |
| **`LEDES invoice`** | **26** | ✅ **sí**, y con él otros cuatro |
| `LEDES legal billing` | 6 | ❌ **no** — la consulta que prescribe el brief |

**Receta, cuatro pasos:**

```bash
# 1. El estándar solo: mide el ruido de tokenización, no se usa para descubrir
gh api -X GET search/repositories -f q='LEDES' | python3 -c 'import json,sys;print(json.load(sys.stdin)["total_count"])'

# 2. Estándar + SUSTANTIVO DEL ARTEFACTO  <-- el canal útil
gh api -X GET search/repositories -f q='LEDES invoice' -f sort=stars -f per_page=30

# 3. Estándar + palabra del sector: SOLO para medir cuánto filtra (control, no descubrimiento)
gh api -X GET search/repositories -f q='LEDES legal billing'

# 4. Todo hallazgo de (2) se verifica por funcion, NO por estrellas: leer README y LICENSE
curl -s https://raw.githubusercontent.com/<slug>/HEAD/README.md | head -40
curl -s https://raw.githubusercontent.com/<slug>/HEAD/LICENSE | wc -c
```

**Tabla de aplicación a la rotación — el sustantivo que hay que usar en cada industria:**

| Industria | Estándar | Sustantivo del artefacto (el que **sí** funciona) |
|---|---|---|
| legal | LEDES · UTBMS · SALI LMSS | `invoice` · `task code` · `taxonomy` |
| healthcare | HL7 · FHIR · DICOM | `record` · `resource` · `image` |
| financial | ISO 20022 · SWIFT MT · FIX | `payment` · `message` · `order` |
| retail | EDIFACT · EANCOM · GS1 | `order` · `catalog` · `barcode` |
| energy | IEC 61850 · CIM · OpenADR | `substation` · `grid model` · `demand response` |
| travel | OpenTravel · NDC · IATA | `booking` · `offer` · `itinerary` |

> **El síntoma de que se ha caído en la trampa** es siempre el mismo: **un `total_count` de un solo
> dígito que parece confirmar que la categoría no existe.** Antes de escribir «no existe X
> permisivo», hay que repetir la consulta **sin la palabra del sector**.

---

## 🆕 P32 — **Producción documental defendible** (Norteamérica): el flujo que el juez ya aceptó

**Para quién:** litigio o investigación interna en EE. UU./Canadá. **Por qué ahora:**
`Schulte v. LinkedIn` (jul-2026) aceptó AI generativa para las determinaciones **finales** de
pertinencia, y dejó abiertas las tres cuestiones que este patrón cubre: **prueba del sistema,
prompts y salida escrita**. Todo lo que sigue es **MIT o Apache-2.0**: entregable cerrado viable.

```
1. CONSERVAR  → legal-hold-manager (MIT)      custodios, emisión y seguimiento de la orden
2. INGESTAR   → apache/tika (Apache-2.0)      ~1.000 formatos, incl. legacy y correo
                 + docling (MIT)              estructura y número de página
3. REVISAR    → modelo + judgment-compiler (MIT)
                 el abogado fija la regla de pertinencia -> la AI la ejecuta sin desviarse
4. REDACTAR   → Marisol (MIT)                 redacción + estampado de texto
5. NUMERAR    → Marisol (MIT)                 numeración Bates = identificador citable por página
6. PRODUCIR   → loadfile-tool (MIT)           export/validación Concordance DAT · OPT · LFP · DII
7. CERTIFICAR → pyHanko (MIT)                 firma del PDF de producción (integridad + autoría)
8. REGISTRAR  → bitácora de prompts, versión de modelo, regla aplicada y quién firmó
```

**El paso 8 no es burocracia: es el entregable.** Las tres preguntas que la resolución dejó abiertas
se responden con un registro, no con un modelo mejor. **Y los pasos 1 y 8 son los que ningún
competidor que venda «AI para e-discovery» está entregando.**

⚠️ **Dos salvedades medidas, no supuestas.** (1) `Marisol` está **dormante desde 2023-08-28**: se
forkea y se asume mantenimiento, o se reimplementa su API —son tres operaciones sobre PDF—. (2)
`loadfile-tool` tiene **0★ y 8 meses**: es un cimiento correcto, no una dependencia probada; el paso
6 exige banco de pruebas propio con producciones reales antes de prometerlo a un cliente.

## 🆕 P33 — **Conformidad de firma eIDAS de punta a punta** (EMEA), con la autoridad del regulador dentro

**Para quién:** cualquier flujo legal en la UE cuyo entregable sea **un documento firmado** — que son
casi todos. **La clave de licencia:** `esig/dss` es **LGPL-2.1**, copyleft **débil**; se **enlaza**
como biblioteca desde un producto cerrado y sólo deben liberarse las modificaciones **a DSS mismo**.
Esa distinción es la diferencia entre viable e inviable, y es la razón de que este patrón exista.

```
PRODUCIR LA FIRMA        → pyHanko (MIT, 807*)         perfiles PAdES (B-B, B-T, B-LT, B-LTA)
VALIDAR CONTRA LA UE     → esig/dss (LGPL-2.1)         listas de confianza UE; PAdES/XAdES/CAdES/ASiC
                                                        *** implementación OFICIAL de la Comisión Europea
                                                            (eu.europa.ec.joinup.sd-dss en Maven Central)
TRADUCIR EL INFORME      → eidas-validator (MIT)        del informe técnico a lenguaje de abogado
PATRÓN DE PORTAL         → autogram-portal (EUPL-1.2)   referencia: ya en producción en un Estado miembro
ANONIMIZAR ANTES         → document-anonymizer (MIT, alemán) · greek-pii-redaction (MIT, griego)
```

**Cómo se arma, y el orden importa:** `pyHanko` firma en el proceso del cliente; **DSS valida en un
servicio aparte** (es Java y es LGPL — aislarlo mantiene limpia la frontera de licencia del producto
Python/JS); `eidas-validator` convierte el veredicto en una frase que el abogado puede firmar.

> 🔑 **El argumento de venta, y no lo tiene ningún competidor propietario:** *«la validez de su firma
> no la afirmamos nosotros: la valida la implementación de referencia de la propia Comisión
> Europea.»* En contratación pública europea, **LGPL y EUPL dejan de ser un problema de licencia y
> pasan a ser una ventaja de adjudicación** — y la Instrucción 2/2026 del CGPJ español, que obliga al
> juez a usar sólo sistemas **facilitados por la administración**, señala exactamente ese mercado.

⚠️ **Riesgo de calendario, explícito:** la EUDI Wallet se anuncia para final de 2026 **pendiente de
actos de ejecución** de la Comisión, y las fuentes consultadas **discrepan** sobre ese plazo (una de
nov-2025 lo daba por vencido a final de 2025). Se diseña contra **PAdES**, que ya es estable, **no
contra la Wallet**, que no lo es.

## 🆕 P34 — **Gobernanza sobre adopción ya consumada** (APAC): el 94% que nadie controla

**Para quién:** despachos y departamentos legales en APAC, donde **94%** ya usa AI y la gobernanza
«no es universal». **No se vende capacidad: se vende evidencia de control.**

```
1. REGLA EXPLÍCITA     → judgment-compiler (MIT)   el abogado compila su criterio en playbook validado
                                                     => cumple el 1er principio del MinLaw de Singapur:
                                                        el profesional responde de TODO su producto
2. EJECUCIÓN ACOTADA   → el modelo aplica el playbook; no improvisa criterio
3. VERIFICACIÓN FUERA  → el control corre FUERA del agente (patrón legal-agent-workshop)
4. CITA COMPROBADA     → reconstrucción desde el documento fuente y comparación carácter a carácter
                           (patrón kancelaria-lex) + marcador permanente de procedencia OCR
5. JURISDICCIÓN        → legal-ai-skills (India/EE.UU./RU/Singapur) · legal-agent-skills (China, MIT)
6. EXPEDIENTE DE AUDITORÍA → qué regla, qué versión, qué fuente, quién firmó
```

**Variante India, y es un encaje literal:** los tribunales indios **ya** usan AI para **transcripción
en sala y traducción de sentencias**. Sobre ese mismo artefacto —el acta— operan los tres activos MIT
de deposición que este pase incorporó: `depo-summarizer` (**LLM local**, el acta no sale),
`DepoIndex` (índice por tema y testigo) y `deposition-contradiction-analysis` (contradicciones con
cita a línea). **Es el único caso de este pase en que un activo hallado con vocabulario procesal
estadounidense sirve directamente a un flujo público asiático** — y conviene no olvidar por qué se
encontró: porque se buscó `deposition`, palabra que esta KB no había consultado nunca.

## 🆕 P35 — **El censo de planos**: el control que este pase debió existir antes y hay que copiar a las doce industrias

Tres pases consecutivos encontraron activos **no buscando mejor, sino buscando otras palabras**: el
pase 6 en portugués, el pase 8 en el plano de la factura, el pase 9 en el de la prueba. El patrón es
siempre el mismo y por tanto es **automatizable**. Cuesta **cero llamadas de red**.

```bash
#!/bin/bash
# censo-de-planos.sh — ejecutar AL EMPEZAR cada pase, antes de cualquier búsqueda.
# Mide el VOCABULARIO DE LA PROPIA KB, no el ecosistema.
# Un 0 no significa "no existe": significa "NUNCA SE PREGUNTO".
for t in bates "load file" "legal hold" custodian "privilege log" deposition transcript \
         PAdES eIDAS notar apostille "chain of custody" docket PACER efiling \
         LEDES UTBMS IOLTA "trust account" conflicts calendaring "legal spend" \
         "entity management" UBO "beneficial owner" "registry filing" immigration ; do
  n=$(grep -rio "$t" --include='*.md' . | wc -l)
  [ "$n" -eq 0 ] && echo "PLANO NO CONSULTADO: $t"
done
```

**Y la lista de términos no se inventa: se extrae de los paréntesis de salvedad de la propia KB**
(regla del pase 8 — *una limitación anotada en un paréntesis es una consulta pendiente, no una nota
al pie*), más los **nombres de los artefactos** que el sector intercambia: formatos, identificadores,
registros y plazos.

> 🔑 **Y el criterio de interpretación, que es lo que convierte el censo en método (`G-L18`):** una
> vez obtenido el `total_count` de un término no consultado, hay **tres** diagnósticos y **tres**
> arreglos distintos:
>
> | `total_count` | Diagnóstico | Arreglo |
> |---|---|---|
> | **Un dígito** | sobre-restricción: se añadió un calificador redundante | **quitar** el calificador — `{estándar}` + `{artefacto}`, nunca + `{sector}` |
> | **Centenares, todo irrelevante** | **homónimo** en un dominio más ruidoso | **añadir** un sustantivo **del mismo plano** |
> | **Centenares y ningún calificador lo recupera** | término **inalcanzable** por el índice | buscar **por función, fuera de GitHub** |
>
> Casos medidos: `LEDES`→LED (109.739), `bates`→apellido (150), `PAdES`→«signature pad» (676),
> `privilege log`→escalada de privilegios (**902, irrecuperable**).

## 🆕 P36 — Gate de **nivel de encabezado de región** (amplía `G-L11`, que validaba filas y tablas pero no la jerarquía)

`G-L11` valida la **estructura de tabla**. Este pase encontró —y **también cometió**— un defecto que
`G-L11` no ve: un `###` al nivel de las regiones crea un ***bucket* de región fantasma**, que es
exactamente lo que el brief prohíbe («`region` es vocabulario CERRADO»). Dos casos en un pase: uno
heredado del pase 4 («PASE 4 — Brasil» como quinta región) y **dos introducidos por mí al escribir**.

```bash
#!/bin/bash
# region-gate.sh — ejecutar ANTES y DESPUES de editar intel/market.md
n=$(sed -n '/^## Opportunities by region/,/^## Hueco de producto transversal/p' intel/market.md \
    | grep -c '^### ')
echo "subsecciones de region: $n (debe ser 4)"
sed -n '/^## Opportunities by region/,/^## Hueco de producto transversal/p' intel/market.md \
  | grep '^### ' | grep -vE '^### (North America|EMEA|APAC|LATAM)$' \
  && { echo "FALLO: encabezado de region fuera del vocabulario cerrado"; exit 1; }
exit 0
```

> 🔑 **La regla general, y vale más que el script:** **todo control estructural se ejecuta DOS veces
> — antes de editar y después de editar.** El acto de escribir reintroduce el defecto que el control
> acababa de encontrar. Ya había ocurrido en el pase 6 (documentar el bug de la barra vertical en una
> celda **reprodujo** el bug) y volvió a ocurrir hoy. Un control que sólo corre al principio
> **audita el pasado y certifica mal el presente.**

---

## 🆕 P37 — Rastreo de **cambio normativo multiestatal** sobre infraestructura cívica (North America)

**El dolor, y está medido en esta KB desde el pase 6:** los *trackers* de legislación de AI de
EE. UU. **no se reconcilian entre sí** (29 estados con legislación y 1.561 proyectos en la sesión
2026, según rastreadores que dan cifras distintas). El comprador —legal ops corporativo, el mismo
del `P29`— no necesita otro resumen: necesita **saber qué cambió esta semana en los 50 estados y qué
obligación suya toca**.

**La infraestructura existe, es abierta y tuvo commits hoy.** Nadie la ha conectado a un registro de
obligaciones.

### Las piezas, con su licencia y el papel exacto

| Pieza | Licencia | Papel | Por qué esa y no otra |
|---|---|---|---|
| [`openstates/openstates-scrapers`](https://github.com/openstates/openstates-scrapers) | **GPL-3.0** | Ingesta: 50 estados + DC + PR, normalizados | 929★, **522 forks**, commit de hoy. No hay alternativa permisiva con esta cobertura |
| [`openstates/people`](https://github.com/openstates/people) | **CC0-1.0** | Legisladores, cargos, comisiones | **CC0 = dominio público.** Se copia al modelo propio sin condición alguna |
| [`unitedstates/congress`](https://github.com/unitedstates/congress) | **CC0-1.0** | Capa federal | Ídem. 228 forks |
| [`portable-genai/obligation-register-kit`](https://github.com/portable-genai/obligation-register-kit) | **Apache-2.0** | Fuente → **obligaciones atómicas** → políticas/controles/evidencia, en registro **versionado append-only** | Es la primitiva correcta y es permisiva. 0★: se adopta como librería, se audita antes |
| [`CatalaLang/catala`](https://github.com/CatalaLang/catala) | **Apache-2.0** | *(opcional)* Codificar la obligación cuando es calculable | Única base permisiva de ley-como-código |

### El cableado, y el orden importa

```
openstates-scrapers  ──►  bulk JSON  ──►  [FRONTERA DE PROCESO]  ──►  normalizador propio
   (GPL-3.0, servicio                                                  (tu licencia)
    separado, sin enlazar)                                                   │
                                                                             ▼
openstates/people + unitedstates/congress (CC0) ──────────────►  modelo de datos propio
                                                                             │
                                                                             ▼
                                            obligation-register-kit (Apache-2.0)
                                            · 1 obligación atómica = 1 fila versionada
                                            · cada fila lleva CITA LITERAL + URL de la fuente
                                                                             │
                              ┌──────────────────────────────────────────────┤
                              ▼                                              ▼
                   REGLAS DETERMINISTAS                            MODELO (sólo donde hay juicio)
                   · ¿cambió el texto? (diff)                      · clasificar la materia
                   · ¿cambió el estado del proyecto?               · proponer a qué control mapea
                   · ¿venció un plazo?                             · DEBE citar la fila
                              └──────────────────────────────┬───────────────┘
                                                             ▼
                                              VERIFICADOR: descarta toda salida
                                              cuya cita no se compruebe contra el bulk
                                                             ▼
                                              COLA HUMANA (legal ops aprueba el mapeo)
                                                             ▼
                                              registro append-only + alerta por obligación
```

### 🔴 La decisión de arquitectura que hay que tomar el primer día: **la frontera GPL**

`openstates-scrapers` es **GPL-3.0** y es la única pieza con esa cobertura. La forma de usarla sin
contaminar el entregable **no es un truco de licencia, es una frontera de proceso**: se despliega
**como servicio separado, sin modificar y sin enlazar**, y se consume **su salida de datos**. Los
datos que produce **no son obra derivada del scraper** — y además las dos piezas de datos
(`people`, `congress`) ya son **CC0**. ⇒ **Lo que se entrega al cliente es el normalizador, el
registro de obligaciones y la capa agéntica; lo GPL se despliega, no se vende.** Si el cliente
exige no tener GPL ni en despliegue, la alternativa es pagar la cobertura a un proveedor de datos:
**es una decisión de coste, no de ingeniería**, y conviene ponerla por escrito en la propuesta.

> ⚠️ **Y el control que esta KB aprendió en el pase 8 y aquí vuelve a aplicar:** la revisión por LLM
> **en lote es inconsistente** (el mismo defecto se marca en la entrada 3 y pasa en la 47). Por eso
> el diff textual, el cambio de estado y el vencimiento de plazo son **reglas deterministas** y el
> modelo sólo ve lo que requiere juicio. **Reglas primero, modelo después.**

---

## 🆕 P38 — **Legislación como código** para un país LATAM: las dos arquitecturas, y la licencia decide

**El hueco, medido y resistente al vocabulario** (a diferencia del de activos, que era un artefacto —
ver `G-L22`): **no existe ningún modelo de legislación como código de ningún país latinoamericano.**
Hay Francia, EE. UU., Nueva Zelanda y Senegal. Seis consultas, incluida una en español, devuelven
**0**. La causa es institucional, no técnica: en Francia es un *commun numérique* con apoyo estatal.

### Dos caminos, y **no** son equivalentes

| | **Camino A — contribuir al común** | **Camino B — producto propio** |
|---|---|---|
| Base | [`openfisca/country-template`](https://github.com/openfisca/country-template) + [`openfisca-core`](https://github.com/openfisca/openfisca-core) | [`CatalaLang/catala`](https://github.com/CatalaLang/catala) |
| Licencia | 🔴 **AGPL-3.0** — copyleft de **red** | **Apache-2.0** — empotrable sin condiciones |
| Qué se obtiene | `openfisca-mx` / `openfisca-br` público, ecosistema y referencias (PolicyEngine tiene **224 forks**) | Especificación ejecutable **anotada contra el texto legal**, con *default logic* para la excepción |
| Qué NO se obtiene | **Activo propietario**: exponerlo como servicio arrastra la obligación de fuente | Ecosistema: hay que construir el motor y las pruebas |
| Cuándo elegirlo | Cliente **público**, o posicionamiento regional (ver abajo) | Cliente **privado** que necesita el cálculo dentro de su producto |

### Por qué el camino A **no** es una concesión

Lo medido en `verticals/solutions.md` aplica aquí entero: **en este plano el comprador natural es
público, y para un comprador público el copyleft es argumento de venta** —garantiza que el Estado no
queda capturado por el proveedor—. Un `openfisca-mx` publicado es **la carta de presentación más
barata que existe** para entrar en un ministerio de hacienda o una agencia tributaria de la región,
y el margen está en la implantación, la calidad del modelo y la capa agéntica. **El reflejo de
«evitar AGPL» viene del producto SaaS y aquí se aplica al revés.**

### Receta del camino A, en orden

1. **Elegir un cuerpo normativo acotado y calculable** — no «el código fiscal»: un beneficio, una
   retención, un tramo. Debe tener fórmula y casos reales publicados.
2. `openfisca/country-template` como esqueleto; **un commit por artículo**, con el `urn:lex` o la
   referencia oficial en el mensaje del commit. Eso hace el modelo auditable por un jurista que no
   lee Python.
3. **La fuente del texto, por país** (todas verificadas en este pase): México
   [`dof-rag`](https://github.com/CodeandoGuadalajara/dof-rag) (**MIT**) · Brasil
   [`lexml-parser-projeto-lei`](https://github.com/lexml/lexml-parser-projeto-lei) (GPL-2.0,
   **oficial del Senado**) y [`dou-collector`](https://github.com/LibreCodeCoop/dou-collector)
   (**MIT**, ⚠️ dormante) · Chile [`lex-chile-mcp`](https://github.com/alvarosdev/lex-chile-mcp)
   (**MIT**) · Argentina [`InfoLeg-MCP`](https://github.com/ejaircastillo/InfoLeg-MCP) y
   [`notarum`](https://github.com/diegoparras/notarum) (**MIT** ambos).
4. **El papel del modelo es asistir la anotación, no escribir la regla.** Propone la fórmula a
   partir del artículo; **el jurista la acepta o la rechaza**; el modelo genera además los casos de
   prueba, que el jurista revisa. La regla publicada **siempre lleva firma humana**.
5. **Validación cruzada obligatoria:** cada regla contra casos reales ya resueltos por la
   administración. Una regla sin caso de prueba **no se publica**.

⚠️ **Y la salvedad que convierte esto en un proyecto y no en un demo:** `BetterRules/openfisca-aotearoa`
(45★, 23 forks, la referencia mundial) está **dormante desde 2025-03-13**. **Un modelo de país no se
mantiene solo**, y sin compromiso institucional de mantenimiento el entregable envejece hasta ser
engañoso — una regla derogada que sigue calculando es peor que no tener la regla.

---

## 🆕 P39 — **Cita normativa verificable por construcción** (EMEA): el identificador hace el trabajo del verificador

Esta KB lleva nueve pases tratando la verificación de cita como un **control posterior**: generar y
luego comprobar. En la UE eso es innecesario, porque **la fuente devuelve un identificador
persistente con cada respuesta** y el identificador es comprobable sin el modelo.

### Piezas, todas verificadas en este pase

| Pieza | Licencia | Papel |
|---|---|---|
| [`elconcept/mcp-eu-sparql`](https://github.com/elconcept/mcp-eu-sparql) | **MIT (1.082 B)** | MCP sobre el SPARQL de la Oficina de Publicaciones; **devuelve CELEX y ECLI en cada cita**. 57k+ sentencias del TJUE |
| [`cyanheads/eur-lex-mcp-server`](https://github.com/cyanheads/eur-lex-mcp-server) | **Apache-2.0** | MCP de EUR-Lex + travesía del grafo **CELLAR** + resolución de conceptos **EuroVoc**. **Sin API key**; endpoint sobreescribible |
| [`tseidl/eurlex-builder`](https://github.com/tseidl/eurlex-builder) | **MIT** | CLI: construye el *dataset* y lo enriquece con **ELI**, fechas de adopción y descriptores EuroVoc |
| [`maastrichtlawtech/cellar-extractor`](https://github.com/maastrichtlawtech/cellar-extractor) | **Apache-2.0** | Metadatos de jurisprudencia en bloque, para la línea base y la evaluación |

**Las cuatro son permisivas y el endpoint es gratuito y sin clave** (`publications.europa.eu/webapi/rdf/sparql`).

### El cableado

```
pregunta ──► MCP (mcp-eu-sparql | eur-lex-mcp-server)
                 │  devuelve: texto + CELEX + ECLI + ELI
                 ▼
         el modelo redacta, y CADA afirmación arrastra su CELEX/ECLI
                 ▼
         VERIFICADOR DETERMINISTA (sin modelo, sin red salvo al endpoint oficial):
           1. ¿el CELEX/ECLI resuelve en CELLAR?        → si no: se descarta la afirmación
           2. ¿el pasaje citado aparece en ese documento? → si no: se descarta
           3. ¿la versión es la vigente a la fecha?       → si no: se marca «histórica»
                 ▼
         sólo lo que pasa los tres controles llega al jurista
```

> 🔑 **La diferencia con `P10`, y es la razón de ser de este patrón:** `P10` verifica una cita
> **después** de que el modelo la escribe, y por eso tiene que resolver el problema difícil de
> *localizar* la fuente. Aquí la fuente **viene con su identificador desde el origen**, así que el
> verificador sólo **resuelve un identificador** — una operación determinista, barata y sin
> ambigüedad. ⇒ **Donde exista un identificador persistente oficial, el patrón correcto es
> arrastrarlo, no reconstruirlo.** Equivalentes a usar: `urn:lex` (Brasil, vía LexML, ya en la KB),
> **ECLI** (jurisprudencia europea), **ELI** (legislación europea y nacional), **CELEX** (UE).
> Donde **no** exista identificador persistente, `P10` sigue siendo el patrón — y esa es la
> situación de la mayoría de LATAM y APAC.

### Y para qué se vende en EMEA

El pase 8 midió la demanda: **61 % de adopción *in-house* europea** (la más alta del mundo), **56 %
usando herramientas genéricas** y **sólo 14 % con AI legal especializada implantada** — es decir,
cuatro de cada cinco usuarios **no pueden documentar nada**, justo donde el AI Act exige documentar.
Este patrón produce **el rastro documental** (identificador por afirmación, verificación
determinista registrada, descartes contados) con **cuatro dependencias permisivas y coste de fuente
cero**.

---

## 🆕 P40 — Ingesta de un **cuerpo normativo completo** a Akoma Ntoso (la base de P37–P39)

Los tres patrones anteriores asumen que el texto ya está estructurado. Cuando no lo está —el caso
normal fuera de la UE y EE. UU.— esto es lo que hay, con la advertencia de licencia por delante.

| Pieza | Licencia | Papel | Advertencia |
|---|---|---|---|
| [`TBI-AI-Incubator/codify`](https://github.com/TBI-AI-Incubator/codify) | **Apache-2.0** | PDF/texto/XML → Akoma Ntoso: adquisición, transcripción, **estructuración por anclas**, recuperación, comparación | Creado 2026-09-18, 15★. **Lo más nuevo y lo único permisivo de extremo a extremo.** Requiere Python ≥3.12 |
| [`laws-africa/bluebell`](https://github.com/laws-africa/bluebell) | 🔴 GPL-3.0 | Parser AN3: garantiza salida **estructuralmente válida** con cualquier entrada | Copyleft fuerte ⇒ **frontera de proceso**, igual que en `P37` |
| [`laws-africa/cobalt`](https://github.com/laws-africa/cobalt) | 🔴 LGPL-3.0 (*stub* 633 B) | **Validación** contra el esquema AN 3.0 | LGPL es enlazable, **pero el texto de la licencia no está en el repo** ⇒ resolver con el mantenedor antes de enlazar |
| [`laws-africa/slaw`](https://github.com/laws-africa/slaw) | **MIT** | Parser AN3 en Ruby | ⚠️ **ARCHIVADO** 2022-06-28. **El único permisivo del stack**: referencia de API y base de fork |
| [`oasis-open/legaldocml-akomantoso`](https://github.com/oasis-open/legaldocml-akomantoso) | **CC-BY-2.0** | **El esquema XSD normativo** | **Es un documento, no código**: se implementa contra él, no se enlaza |
| [`SenatoDellaRepubblica/AkomaNtosoBulkData`](https://github.com/SenatoDellaRepubblica/AkomaNtosoBulkData) | CC-BY-4.0 | **Corpus oficial de referencia** para probar el pipeline | Senado italiano, repo de 2016 con commit de hoy. **La mejor verdad-terreno gratuita que existe** |

### El orden, y el control que lo hace defendible

1. **Validar antes de confiar:** todo lo que salga del pipeline pasa por validación de esquema
   (`cobalt`, o un validador propio contra el XSD de OASIS). Un AN inválido que *parece* válido
   envenena los tres patrones anteriores.
2. **Probar contra el corpus italiano primero.** Es AN oficial, masivo y gratuito: si el pipeline no
   reproduce la estructura de un acto del Senado italiano, no está listo para el cuerpo del cliente.
3. **La estructura es juicio jurídico, no formato.** Qué es artículo, parágrafo, inciso o anexo
   **lo decide la tradición jurídica del país** (ver `editor-articulacao`, de la Asamblea de Minas
   Gerais, para la brasileña). El modelo propone la jerarquía; **un jurista local la aprueba** antes
   de que se consolide.
4. **Cada nodo lleva su identificador persistente** desde el primer día (`urn:lex`, ELI, o el que
   use la jurisdicción). Añadirlo después obliga a reprocesar todo, y es lo que hace posible `P39`.

> ⚠️ **El activo que NO se usa aquí, y el motivo:** [`hendrillara/akoma`](https://github.com/hendrillara/akoma)
> (legislación federal brasileña por artículo) aparece en los buscadores descrito como **MIT**. Su
> `LICENSE` son **6.732 B** titulados **«Akoma Noncommercial and Commercial Licence 1.0»** —
> licencia bespoke con frontera comercial. **No entra en ningún entregable.** Es el caso `G-L20`.

## 🆕 P41 — **Acta oral soberana**: el audio de la audiencia no sale de la institución, y sale `página:línea`

**Problema que resuelve.** El Estado autorizó grabar y no financió transcribir (North America), la
judicatura ya transcribe pero manda el audio a una nube ajena (Chile) o no (Argentina), y el
artefacto que el litigio consume —**texto paginado y citable**— no lo emite ninguna pieza del stack.

**Arquitectura, reutilizando la regla del pase 8 «el modelo lee, las reglas deciden»:**

1. **Captura e ingesta.** [hwdsl2/scribecrate](https://github.com/hwdsl2/scribecrate) (MIT, 2.304 B)
   como servidor: **offline por diseño**, modelos en caché, Docker CPU o CUDA. En sala sin red,
   [ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp) (MIT) o
   [k2-fsa/sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) (Apache-2.0) embarcados.
2. **ASR.** [SYSTRAN/faster-whisper](https://github.com/SYSTRAN/faster-whisper) (MIT) para lote;
   [QuentinFuxa/WhisperLiveKit](https://github.com/QuentinFuxa/WhisperLiveKit) (Apache-2.0) si se
   quiere texto en vivo en estrados. ⛔ **No `moonshine` si el idioma es español** (ver `P44`).
3. **Atribución de locutor.** [pyannote/pyannote-audio](https://github.com/pyannote/pyannote-audio)
   (MIT, pesos CC-BY-4.0) o [BUTSpeechFIT/DiariZen](https://github.com/BUTSpeechFIT/DiariZen) (MIT)
   si los pesos con registro previo son un problema de aprovisionamiento. En una audiencia multiparte
   **quién habla es el dato jurídico**, no un adorno.
4. **Anclaje temporal.** [m-bain/whisperX](https://github.com/m-bain/whisperX) (BSD-2) o
   [MahmoudAshraf97/ctc-forced-aligner](https://github.com/MahmoudAshraf97/ctc-forced-aligner)
   (BSD-2) para `timestamp` por palabra ⇒ **toda línea del acta apunta al segundo exacto del audio**.
   ⛔ **No `whisper-timestamped`: es AGPL-3.0.**
5. **🟢 Paginador determinista — ESTO ES EL CÓDIGO A ESCRIBIR, no hay repo.** 25 líneas por página,
   numeración consecutiva, índice `página:línea`, plantilla del foro. **Determinista y reproducible
   al carácter; sin modelo dentro.** Es la pieza que convierte el stack en entregable (`T-P11-6`).
6. **Anonimización, si el foro la exige.**
   [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) (MIT) sobre el
   **texto**, nunca sobre la voz: la síntesis de voz **mete el sistema en el Art. 50 del Reglamento
   UE de AI** (ver `P43`).
7. **Gate de certificación humana.** El informe de `P42` adjunto, y **una persona certifica**. No es
   opcional ni es prudencia: es la condición expresa del *white paper* del Tribunal Supremo de India
   y la práctica declarada en India, y es lo que hace aceptable el récord.

**Entregables:** el acta paginada, el `JSON` con `timestamp` por palabra y locutor, el informe de
exactitud, y el audio original con su hash. **Coste de licencia del stack: cero.**

---

## 🆕 P42 — **Informe de exactitud del acta**: el entregable que nadie vende y que decide la compra

**Por qué existe.** `T-P11-2`: ningún proveedor publica su WER sobre audio judicial. Un tribunal no
compra «buena transcripción», compra **récord defendible**. Si la exactitud no está medida, la
objeción en sala es libre.

**Receta, todo permisivo y verificado:**

1. **Referencia humana** sobre una muestra estratificada: por **idioma, acento, rol procesal**
   (juez, letrado, testigo, intérprete) y **condición acústica** (micrófono de estrados vs. sala vs.
   videoconferencia). La estratificación es el método; sin ella el número agregado engaña.
2. **WER palabra a palabra** con [revdotcom/fstalign](https://github.com/revdotcom/fstalign)
   (Apache-2.0) — alineación por transductores finitos, de una empresa de transcripción.
   Segunda opinión con [jitsi/jiwer](https://github.com/jitsi/jiwer) (Apache-2.0).
3. **DER por locutor** con [pyannote/pyannote-metrics](https://github.com/pyannote/pyannote-metrics)
   (MIT) y contraste independiente con [nryant/dscore](https://github.com/nryant/dscore) (BSD-2).
   **Separar WER de DER es obligatorio:** un acta con 2% de WER y locutores intercambiados es
   **inservible** y el WER no lo ve.
4. **Gate con umbral y cola humana selectiva.** Por debajo del umbral, el segmento va a revisión
   humana; por encima, pasa. **La persona revisa segmentos, no el acta entera** — es lo que hace
   viable el volumen.
5. **Línea base del cliente, nunca cifra de folleto.** Mismo criterio que el pase 8 impuso a los
   ahorros de facturación: se mide contra **el tiempo y el coste actuales del propio tribunal o
   despacho**.

> **Error que esta receta previene, documentado en esta KB.** `billing-lint` (pase 8) midió que
> **la revisión por LLM en lote es inconsistente**: «el mismo defecto se marca en la entrada 3 y pasa
> callado en la 47». En transcripción el efecto es el mismo y peor: **el error que pasa en el minuto
> 47 entra en el récord oficial.** Reglas y métricas deterministas primero; el modelo sólo donde cabe
> un juicio.

---

## 🆕 P43 — **Expediente de clasificación de riesgo** (EMEA): el mismo software, dos clases según quién lo despliega

⚠️ **Fuente:** `eur-lex.europa.eu` no resuelve desde esta sesión. Basado en el *AI Act Service Desk*
de la Comisión y fuentes secundarias de práctica. **Verificar literalidad en el Diario Oficial antes
de entregar.**

**El árbol de decisión, y es el entregable:**

1. **¿Quién despliega?**
   - **Un tribunal** ⇒ zona **no resuelta**. El Anexo III.8(a) cubre asistir a la autoridad judicial
     a *investigar e interpretar hechos y Derecho*; la transcripción **no es eso**. El Considerando 61
     excluye **actividades administrativas accesorias**, y la lista del *Service Desk*
     (anonimización/pseudonimización de resoluciones y documentos, comunicación interna, verificación
     de tasas) **no menciona la transcripción**. ⇒ **Se documenta la posición, no se asume.**
   - **Un despacho o una parte** ⇒ **fuera del ámbito de 8(a)**: no actúa por cuenta de una autoridad
     judicial. **Vía de entrada comercial sin carga de conformidad de alto riesgo**, y es la misma
     inversión de comprador que `P29` encontró en la factura.
2. **¿Genera contenido sintético?** La transcripción **consume audio real y emite texto: NO**.
   El marcado legible por máquina del **Art. 50(2) vence el 2026-12-02** y **este diseño queda
   fuera**. ⛔ **Entra en ámbito si se añade** lectura por voz sintética (TTS) o **anonimización de la
   voz del testigo por síntesis**. ⇒ **Decisión de arquitectura con consecuencia regulatoria: el
   anonimizado se hace sobre el texto (`P41` paso 6), no sobre la voz.**
3. **¿Es penal?** Entonces entra la **Directiva 2010/64/UE** (derecho a interpretación y traducción):
   interpretación «sin demora» y **deber de confidencialidad**. ⚠️ Está escrita para intérpretes
   **humanos**, así que aplicarla a un sistema es **inferencia, no regla**. Operativamente fija el
   estándar contra el que se comparará el sistema, y es **la razón técnica por la que el audio penal
   europeo se procesa en local**.
4. **Apoyo doctrinal concurrente, de otra jurisdicción:** la **Academia Judicial de Colombia**
   (abril 2026) clasifica la transcripción como **apoyo administrativo, el más bajo de tres niveles de
   intensidad decisoria**. **No vinculante en la UE**, pero es doctrina concurrente e independiente
   para el mismo encuadre, y en un expediente de clasificación eso **se cita**.

**Entregable:** el dossier de clasificación, el registro de decisiones de arquitectura que lo
sostienen (local, sin TTS, anonimización sobre texto) y el informe de `P42` como evidencia de
diligencia. **Alto riesgo diferido a 2027/2028** ⇒ **ventana para dejar el expediente hecho antes de
que obligue.**

---

## 🆕 P44 — **Auditoría de licencia por idioma** (la receta que `T-P11-1` obliga a escribir, y aplica a las doce industrias)

**El fallo que previene, medido hoy.** `moonshine-ai/moonshine`: 11.598★, el buscador y los
comparadores lo presentan como MIT, su `LICENSE` son **14.180 B** y empieza por un **reparto**. El
código es MIT, los modelos *streaming* y todos los de inglés son MIT, y **español (Base), árabe,
japonés, coreano, mandarín, ucraniano y vietnamita** quedan bajo licencia **no comercial por encima
de USD 1 M de facturación anual**. ⇒ **Permisivo en Norteamérica, no utilizable en LATAM, España,
Japón o Corea.**

**Procedimiento, cinco sondas:**

1. **La unidad de auditoría es el artefacto que se carga en producción**, no el repositorio: el
   fichero de pesos, para el idioma concreto del despliegue.
2. **Leer el `LICENSE` entero, no la cabecera.** Un fichero muy por encima de la banda
   (MIT 1.052–1.183 B; Apache-2.0 ~10.1–11.5 kB; AGPL 34.523 B) **es un reparto o un compuesto**.
   14.180 B no es ninguna licencia conocida ⇒ leer.
3. **Buscar el eje de la excepción**, que puede no ser técnico: por **idioma**, por **facturación**,
   por **directorio** (el *carve-out* de `Extras` en `bullet3`, KB de gaming), por **marca**
   (`InvoicePlane`, pase 8) o por **tercero obligatorio** (la EULA de `cuRobo` en `IsaacLab`).
4. **Separar concesión de código y concesión de pesos.** `pyannote-audio`: código **MIT**, pesos
   `community-1` **CC-BY-4.0**. Son **dos lecturas**, y en la capa de modelos es la norma.
5. **Registrar el sustituto antes de necesitarlo.** Para español sin restricción, verificado:
   `whisper` (MIT), `faster-whisper` (MIT), `sherpa-onnx` (Apache-2.0), `vosk-api` (Apache-2.0).

> **Copiar a las once KBs restantes.** Donde haya pesos por idioma o por región —voz, traducción,
> OCR, TTS— **la licencia puede variar con el mercado del engagement**. Una auditoría hecha en
> Norteamérica **no vale** para la propuesta de LATAM, y es el tipo de defecto que no aparece hasta
> la due diligence del cliente.

## 🆕 P45 — Puerta de **renovaciones y anualidades**: el único plano de esta KB donde el fallo es irreversible

**Problema.** Una anualidad o una renovación de marca olvidada **abandona el derecho de forma
definitiva** en la mayoría de jurisdicciones: no hay restitución ni recurso, y el activo que caduca
es normalmente el más caro de la cartera. El censo de este pase midió la herramienta abierta
disponible para eso: `patent annuity renewal deadline` ⇒ **1 repo, sin licencia**.

**Lo que NO se hace.** Forkear [`jjdejong/phpip`](https://github.com/jjdejong/phpip) (GPL-3.0). Trae
el calendario de renovaciones resuelto y es la opción que *parece* ahorrar seis meses; arrastra
GPL-3.0 al entregable comercial. Se despliega tal cual como sistema de registro del cliente y **se
lee como especificación funcional**: su modelo de datos de plazos es el mejor documento de requisitos
que existe en abierto.

**Receta, con la regla `MODELS READ, RULES DECIDE` del `P29`:**

1. **Estado oficial, de la oficina, nunca de un agregador:**
   [`patent-dev/uspto-odp`](https://github.com/patent-dev/uspto-odp) (MIT) ·
   [`patent-dev/epo-ops`](https://github.com/patent-dev/epo-ops) (MIT) ·
   [`patent-dev/dpma-connect-plus`](https://github.com/patent-dev/dpma-connect-plus) (MIT) ·
   [`chrisryugj/korean-patent-mcp`](https://github.com/chrisryugj/korean-patent-mcp) (MIT) ·
   [`milaniseb12-png/inpi-marcas-mcp-server`](https://github.com/milaniseb12-png/inpi-marcas-mcp-server) (MIT).
2. **Backfill histórico** con [`patent-dev/epo-bdds`](https://github.com/patent-dev/epo-bdds) y
   [`patent-dev/bulk-file-loader`](https://github.com/patent-dev/bulk-file-loader) (MIT los dos).
   Nunca raspando Espacenet: los seis raspadores que existen son de 0–1★ y sin licencia.
3. **Tabla de significados** —el paso que se salta todo el mundo—:
   [`patent-dev/kind-codes`](https://github.com/patent-dev/kind-codes) (MIT) traduce el código *kind*
   del documento a su posición en el ciclo de vida, que es lo que determina **qué plazo corre**.
4. **Escalera de plazos determinista.** Aritmética de fechas en código versionado, con prueba de
   regresión por jurisdicción y reproducible al día. **Cero modelo en este paso.**
5. **El modelo, solo en la última milla:** redactar el aviso legible para el cliente y convertir la
   prosa de un dictamen de oficina en tareas con fecha — cada una **citando el párrafo** del que
   sale, y un verificador que descarta la tarea cuya cita no se comprueba.
6. **Doble control de caducidad:** el sistema avisa, y además **reconcilia contra el estado publicado
   por la oficina** tras la fecha. El fallo que mata no es «no avisé», es «avisé y nadie lo hizo».

**Por qué se vende.** Es el único entregable de esta KB cuyo valor no se mide en horas ahorradas sino
en **un activo que no se pierde**. Y la contraparte compradora no es el despacho: es el departamento
de PI corporativo, que es donde ya está la cartera de Globant (mismo reencuadre de comprador que el
`P29`).

## 🆕 P46 — Búsqueda de estado de la técnica **con informe de exactitud**, no con promesa

**Problema.** Nadie publica su exactitud. El pase 11 lo midió en transcripción (`T-P11-2`: «nadie
vende exactitud certificada») y aquí se repite: el único banco agéntico de estado de la técnica que
existe, [`AIforIP/PatEx-Gym`](https://github.com/AIforIP/PatEx-Gym) (13★), **no tiene licencia**.

**Receta:**

1. **Recuperación:** [`pqaidevteam/pqai`](https://github.com/pqaidevteam/pqai) (MIT) como núcleo
   semántico. ⚠️ Sus siete microservicios llevan dormidos desde 2022–2023: **se forkea la flota
   completa y se asume mantenimiento**, no se declara dependencia.
2. **Fuentes:** [`ip-tools/python-epo-ops-client`](https://github.com/ip-tools/python-epo-ops-client)
   (Apache-2.0, vivo) para EPO OPS;
   [`PatentsView/PatentsView-API`](https://github.com/PatentsView/PatentsView-API) (BSD-2) y
   [`ropensci/patentsview`](https://github.com/ropensci/patentsview) (MIT) para bibliografía y
   cesionarios US.
3. **Estructura:**
   [`volfpeter/uspto-patent-citation-graph`](https://github.com/volfpeter/uspto-patent-citation-graph)
   (MIT) — la citación es la señal de relevancia que el examinador ya usa.
4. **El entregable que falta:** `recall@k` sobre las citas que el examinador **efectivamente** opuso
   en expedientes ya resueltos. Es un banco de pruebas que se construye con datos públicos del propio
   USPTO, y **`PatEx-Gym` se lee como referencia de diseño, no se forkea** (sin licencia).
5. `AIforIP/PatEx-Gym` y `smcronin/ai-language-patent-applications` (MIT, paquete de réplica) se citan
   como literatura, no como dependencias.

**Regla:** no se promete «encontramos más estado de la técnica». Se entrega **la medida contra la
línea base del cliente**, igual que en `P29` con los ahorros de facturación.

## 🆕 P47 — Cartera multi-oficina **solo con fuentes oficiales** (nueve registros, todos permisivos)

Ocho oficinas y nueve clientes MIT/Apache verificados hoy. Es el patrón «MCP de fuentes oficiales»
(`intel/trends.md` nº 13) aplicado a PI, y la plaza vacía ya no es LATAM entera:

| Registro | Cliente permisivo | Licencia | Hueco |
|---|---|---|---|
| USPTO (patentes y expediente) | `patent-dev/uspto-odp`, `smcronin/uspto-cli`, `DunlapCoddingPC/pyUSPTO` | MIT | — |
| EPO / Espacenet | `patent-dev/epo-ops`, `ip-tools/python-epo-ops-client`, `navisbio/OPS-patent-search-mcp` | MIT / Apache-2.0 | — |
| DPMA (Alemania) | `patent-dev/dpma-connect-plus` | MIT | 2★, un solo mantenedor |
| EUIPO (marcas UE) | `anseljh/euipo-tm-client` | MIT | **1★.** Toda la capa de marca EMEA cuelga de un repo |
| KIPRIS (Corea) | `chrisryugj/korean-patent-mcp`, `ChloePark85/kipris-cli` | MIT / **MIT-0** | — |
| JPO (Japón) | `kitepon/IP-MCP` | MIT | 0★; `JPO patent japan api` devuelve **total 1** |
| INPI (Brasil) | `milaniseb12-png/inpi-marcas-mcp-server`, `mcp-dir/inpi_patentes-mcp` | MIT | 0★ y 0 forks los dos |
| ONAPI (R. Dominicana) | `CarlsRemy/onapi-utils` | MIT | 0★. Único activo del Caribe |
| CNIPA (China) | `faruheaisha/cnipa-patent-kit`, `roy-tian/cn-patent-ipc` | MIT | 2★ y 0★ |
| **IMPI (México)** | **ninguno** | — | **Hueco medido: `IMPI mexico marcas` ⇒ 2 resultados, 0★, sin licencia** |
| **CGPDTM (India)** | **ninguno permisivo encontrado** | — | Hueco medido |

**Regla de arquitectura:** un adaptador por oficina detrás de una interfaz común, y el **estado
canónico siempre el de la oficina**. Las 3 ó 4 oficinas que faltan se construyen con el mismo patrón
—es el trabajo más pequeño y mejor acotado de todo este plano— y son **entregables reutilizables en
todos los engagements de la región**.

## 🆕 P48 — `ST.96` como contrato de integración: es una **construcción**, y el alcance está medido

**Honestidad primero:** no existe implementación abierta de ST.96. `wipo xml schema patent trademark`
⇒ `total_count` **0**; `ST96` ⇒ 9 repos, todos de prácticas universitarias. Esto **no es un patrón de
composición: es un proyecto**, y el valor de haberlo medido es que el alcance deja de ser una
incógnita.

**Lo que hay para empezar:**

- Los **esquemas oficiales de WIPO, ST.96 v9.0**, aprobados por el *XML4IP Task Force* el
  **2025-04-01**, publicados en ZIP (normal y *flattened*), con seis familias de componentes:
  comunes, patente, marca, diseño, indicación geográfica y copyright.
- **ST.26** (listados de secuencias, obligatorio en PCT) tiene **una** implementación permisiva de la
  que partir: [`angela-125/ST26_sequence-xml-generator`](https://github.com/angela-125/ST26_sequence-xml-generator) (MIT).
- Las implementaciones de oficina (el USPTO publica esquemas propios **basados** en componentes
  ST.96) sirven de referencia de cómo se restringe el estándar en la práctica.

**Alcance recomendado:** **no** se implementa ST.96 completo. Se tipa el **subconjunto** de las
familias que el cliente realmente presenta, con validación contra el XSD oficial y una prueba por
cada campo que su oficina exija. Y se consulta por el **sustantivo del artefacto**, nunca por el
nombre del estándar — ver `T-P12-1`: `ST.96` devuelve 2.683 resultados de pantallas OLED.

## 🆕 P49 — La capa de **redacción** ya está resuelta, es MIT, y es de APAC

El hallazgo que más acorta un engagement: mientras Occidente debate si se puede redactar con AI,
APAC publicó las plantillas bajo MIT y con tracción real (65–216★ en repos de semanas o meses).

**Composición, con enrutador por jurisdicción:**

1. **Memoria y reivindicaciones:**
   [`RobThePCGuy/Claude-Patent-Creator`](https://github.com/RobThePCGuy/Claude-Patent-Creator)
   (MIT, 216★, 35 forks) como base general.
2. **Por jurisdicción:** [`lsj4232/KR_PATENT_SKILL`](https://github.com/lsj4232/KR_PATENT_SKILL)
   (MIT, 67★) para Corea · [`handsomeZR-netizen/cn-patent-drafter`](https://github.com/handsomeZR-netizen/cn-patent-drafter)
   (MIT, 65★) para China · [`ThomasMoreAI/legal-skills-open`](https://github.com/ThomasMoreAI/legal-skills-open)
   (Apache-2.0, 143★, 39 jurisdicciones) como marco de *skills*.
3. **Dibujos:** [`PisenAILab/china-patent-figure-skill`](https://github.com/PisenAILab/china-patent-figure-skill)
   (MIT, 100★) — conformidad formal de figuras CNIPA, la causa de objeción más tonta y más frecuente.
4. **Dos puertas obligatorias antes de que salga nada:**
   - **Inventoría:** solo personas naturales (USPTO 2025-11-28; igual en LATAM y en la línea DABUS).
     El expediente registra **qué aportó la persona y qué la herramienta, por reivindicación y con
     fecha** — el mismo rastro que piden la ABA 512 y el EU AI Act (ver `intel/trends.md` H).
   - **Responsabilidad de contenido:** la EPO lo dice expresamente en las Guidelines 2026 (Sección 5
     del Prólogo) — la parte responde del contenido **se haya usado AI o no**. La revisión humana no
     es una buena práctica: es el régimen de responsabilidad.
5. **Clasificación CPC/IPC:** `roy-tian/cn-patent-ipc` (MIT) y `NICTA/t3as-pat-clas` (GPL-3.0, solo
   lectura). ⚠️ Capa pobre: `CPC IPC patent classification` ⇒ **total 4**.
