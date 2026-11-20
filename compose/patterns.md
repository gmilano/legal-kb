---
industry: legal
region: Global
updated: 2026-11-20
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

## 🆕 P12 — El primer MCP de fuentes legales oficiales de LATAM (el hueco real, con plantilla probada)

**El hueco, verificado por doble canal:** existen MCP de fuentes oficiales para EE. UU., Alemania,
Suiza, Italia, Taiwán (×2), Corea y China. **Para Brasil, México, Argentina, Chile, Colombia y
Perú: ninguno.** Y lo que **sí** existe para LATAM son *flujos*:
`ThomasMoreAI/legal-skills-open` (Apache-2.0) con `br/` 15 plugins, `ar/` 2, `mx/` 2, `co/` 1,
`pe/` 1, `do/` 1. **Hay con qué razonar y no hay contra qué verificar.**

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

⚠️ **Antes de prometerlo:** la disponibilidad y los términos de uso de cada fuente oficial LATAM
**no se verificaron en este pase** — sólo se verificó que **no existe el servidor**. El primer
sprint es un **inventario de accesibilidad y licencia por fuente**, no código.

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
