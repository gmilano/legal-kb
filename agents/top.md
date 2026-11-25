---
industry: legal
region: Global
updated: 2026-11-25
---

# 🎯 Agentes AI — Legal Services

> Agentes y herramientas AI open source para la industria legal. Foco: MIT / Apache 2.0 / BSD.
> Última actualización: 2026-11-20

## Método de verificación (2026-11-20) — y una corrección al método anterior

Cada fila se verificó por **dos canales independientes**:

1. **API de búsqueda de GitHub** — `gh api -X GET search/repositories -f q='repo:<owner>/<name>'`.
   Devuelve en una sola llamada: existencia, SPDX, estrellas, `archived`, `pushed_at` y rama por
   defecto.
2. **Lectura byte a byte del LICENSE** desde `raw.githubusercontent.com/<repo>/HEAD/<fichero>`,
   probando `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING`.

> ⚠️ **CORRECCIÓN DE MÉTODO.** El pase del 2026-11-04 escribió en tres ficheros de esta KB que
> la API de GitHub estaba **«bloqueada por el proxy de esta sesión»**. **Se reprobó hoy y NO lo
> está.** Esa creencia heredada costó: `archived` y `pushed_at` **nunca se habían medido en esta
> KB**, y por eso dos renombrados y un repo muerto pasaron inadvertidos. Un canal declarado
> bloqueado por un pase anterior **se vuelve a probar, nunca se hereda**.
>
> ⚠️ Lo que **sí** está bloqueado aquí: `gh api repos/<owner>/<name>` (fuera del scope de la
> sesión) y `curl` sobre `github.com` (devuelve 403 del proxy, no del repo). Usar el canal de
> búsqueda + `raw`. Y **siempre `/HEAD/` en las URL raw**: `OpenSign` está en `staging`,
> `databunker` y `awesome-legal-data` en `master`.

### Por qué hacen falta los dos canales
Ninguno basta solo. `freelawproject/courtlistener` y `OpenSignLabs/OpenSign` devuelven
**`NOASSERTION`** en la API y ambos tienen un AGPL-3.0 perfectamente legible en el fichero:
`NOASSERTION` es un **detector de licencia compuesta o no reconocida, no una ausencia**. A la
inversa, los dos renombrados de abajo son invisibles en `raw` (resuelve por redirección) y sólo
aparecen en la API.

### 🆕 Tercera divergencia de canal — DIAGNOSTICADA MAL EN EL PASE 2, RESUELTA EN EL PASE 3

El pase 2 encontró un repo **ausente en la API de búsqueda pero con `raw` a 200** y concluyó:
*«el repo existe, simplemente no está en el índice de búsqueda»*. **La conclusión era cómoda y
falsa.** Medido hoy por un tercer canal:

| Repo | API búsqueda | `raw` | `git ls-remote` HEAD | Lectura correcta |
|------|--------------|-------|----------------------|------------------|
| `lowtidebuild/contract-review-agent` (slug publicado) | **HTTP 422** | 200 | `e16315dd…` | **Slug obsoleto.** |
| `lowtidebuild/contract-review` (canónico) | **total=1**, ★41, Apache-2.0, `pushed_at=2026-07-24` | 200 | `e16315dd…` | **Es el mismo repo: SHA idéntico.** |

> 🔧 **G-L1 — LA IDENTIDAD DE SHA ES LA ÚNICA PRUEBA DECISIVA DE RENOMBRADO, Y ES BARATA.**
> `git ls-remote https://github.com/<slug> HEAD` **sigue la redirección de renombrado** y devuelve
> el SHA. Si el slug viejo y el candidato nuevo devuelven **el mismo SHA**, son el mismo
> repositorio, y eso es una prueba criptográfica, no un parecido.
>
> Esto **sustituye** la prueba que esta KB usaba. El pase 2 acreditó el renombrado de Presidio con
> *«LICENSE idéntico en ambos: 1.084 B, mismo MD5»*. **Un MD5 de LICENSE igual acredita que dos
> repos usan la misma licencia, no que sean el mismo repo** — y como el texto MIT sólo varía en la
> línea de copyright, miles de repos del mismo autor colisionan ahí. Reverificado hoy por SHA:
> `microsoft/presidio` ≡ `data-privacy-stack/presidio` (ambos `da946811…`) y
> `JSv4/OpenContracts` ≡ `Open-Source-Legal/OpenContracts` (ambos `56ca972a…`). **Los dos
> renombrados del pase 2 son correctos; la prueba que se dio de ellos, no.**

> 🔧 **G-L2 — HTTP 422 NO SIGNIFICA «CANAL BLOQUEADO», SIGNIFICA «ESE SLUG NO ES BUSCABLE».**
> La API no devuelve `total_count: 0` para un slug inexistente: devuelve **422 Validation Failed**
> («the listed users and repositories cannot be searched…»). Con una consulta de control que
> funciona en la misma llamada (`repo:torvalds/linux` → total=1), **un 422 es un dato sobre el
> slug, no sobre el instrumento.** Es exactamente el error que llevó al pase del 2026-11-04 a
> declarar la API «bloqueada por el proxy» y congelar una columna entera de esta KB durante un mes.

> 🔧 **G-L3 — `gh api repos/<owner>/<name>` NO ES UN INSTRUMENTO DE EXISTENCIA EN ESTA SESIÓN.**
> Devuelve **403 «GitHub access to this repository is not enabled for this session»** para
> *cualquier* repo no adjunto, incluidos los que existen con certeza (se probó contra
> `docling-project/docling`, 70.826★: también 403). **Un pase que lea ese 403 como «el repo ya no
> existe» borraría filas vivas.** Canales válidos aquí: `search/repositories`, `raw` y
> `git ls-remote`. (`curl` sobre `github.com` también da 403 del proxy, no del repo.)

> 🔧 **G-L4 — CUANDO LA API HA PERDIDO EL SLUG, LA BÚSQUEDA DE CÓDIGO LO RECUPERA.**
> `gh api -X GET search/code -f q='"<frase distintiva del README>"'` devolvió el slug canónico
> (`lowtidebuild/contract-review`) que ninguna consulta `repo:` ni `user:` encontraba. Y el mismo
> resultado trajo un segundo repo, `timc81/bridge`, **con la misma frase del README y un SHA
> distinto** (`25947064…`): es una copia, no un renombrado. ⇒ **La misma consulta que recupera el
> slug detecta copias sin atribución** — relevante porque el original es Apache-2.0, que exige
> conservar aviso de copyright y NOTICE.

> ⚠️ **Y lo que el diagnóstico equivocado costó, que es el verdadero motivo de esta sección.**
> Al dar por bueno *«existe, sólo no está indexado»*, el pase 2 publicó la fila con el slug muerto,
> con estrellas **«—»** (sin medir) y con liveness **«activo (raw)»**. Los tres campos eran
> falsos o inciertos y hoy se miden: **★41** (no es un activo relevante por tracción) y
> **`pushed_at` = 2026-07-24, es decir 4 meses dormido** — no «activo». `raw` devolvió 200 y de ahí
> se infirió actividad: **`raw` sirve contenido de un repo abandonado exactamente igual que de uno
> vivo. `raw` acredita existencia, nunca vitalidad.**

> 🔴 **G-L5 — EL FALLO QUE NINGUNA VERIFICACIÓN DE LICENCIA NI DE ESTRELLAS DETECTA:
> *BLANQUEO DE CATEGORÍA*.** Un artículo de prensa de este mes describe **`openclaw/openclaw`**
> como *«un proyecto open source de AI legal»* que se habría convertido en el repo más estrellado
> de GitHub. Medido: **existe, es MIT, y tiene 394.928★** — las tres comprobaciones que hace esta
> KB **pasan limpias**. Su propia descripción es *«The AI that really does things. Any OS. Any
> Platform. The lobster way. 🦞»*: **no contiene ni un término legal. Es un agente de propósito
> general.** Si entrase, sería al instante la fila más prominente y más errónea de la KB, con
> licencia y estrellas impecables.
> ⇒ **La verificación de existencia no puede detectar un error de pertinencia.** Hace falta un
> **canal de pertinencia** separado: leer la `description`/README del propio repo y exigir que el
> vertical aparezca **en palabras del repo**, no del medio que lo cita. Nunca se admite una fila
> por la categoría que le atribuye un tercero. Receta: `compose/patterns.md` → **P15**.

**Barrido completo del pase 3 (auditoría del pase 2, no reescritura):** se reextrajeron **las 65
URL únicas de GitHub** del conjunto de ficheros y se pasaron **las dos canales** más
`git ls-remote`. Resultado: **62 resuelven en la API; 3 devuelven 422 y los 3 están explicados**
— `microsoft/presidio` y `JSv4/OpenContracts` son slugs obsoletos citados a propósito en la tabla
de renombrados, y `lowtidebuild/contract-review-agent` era un renombrado **no detectado**, ahora
resuelto arriba. **0 enlaces roto sin declarar, 0 filas inventadas, 0 cabeceras como dato.**
Las estrellas y `pushed_at` del pase 2 se revalidaron una por una y **coinciden** (desviación
máxima +1★ por crecimiento de unas horas), de modo que **los datos del pase 2 se confirman; lo que
se corrige es un slug, un diagnóstico de método y tres campos de una fila.**

> 📌 **G-L6 — LAS ESTRELLAS SON MONÓTONAS, ASÍ QUE UN VALOR REGISTRADO POR ENCIMA DEL MEDIDO HOY
> ES PRUEBA DE UN REGISTRO MALO, NO DE UNA CAÍDA.** Un repo no pierde estrellas en masa. El
> registro de agosto de esta KB daba *«CourtListener (Apache-2.0, ~2.4k★)»*; medido hoy:
> **1.076★ y AGPL-3.0**. Como 2.400 > 1.076 y eso es imposible, **la cifra de agosto estaba
> inventada o copiada de otro proyecto** — y la licencia también estaba mal. El pase 2 ya lo había
> corregido sin señalar *por qué* era detectable: queda señalado. Aplicar la comparación a
> cualquier cifra heredada: **si bajó, no bajó; estaba mal.**

## Agentes y herramientas destacadas

| Nombre | Repo | Licencia (leída) | País / región de origen | Descripción | Stars | Último commit |
|--------|------|------------------|-------------------------|-------------|-------|---------------|
| **Claude for Legal** | [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Apache-2.0 (11.358 B) | EE. UU. · North America | **El líder de la categoría, y esta KB no lo tenía.** Suite de plugins para flujos legales: in-house commercial, privacidad, producto, corporativo, laboral, litigio, regulatorio, gobernanza de AI, IP y docencia (clínicas y estudiantes). Se instala como plugin de Claude Code/Cowork **o** se despliega vía Managed Agents API detrás de tu propio motor de workflow — mismo system prompt, mismas skills. | **10.054** | 2026-11-19 |
| mike | [open-legal-products/mike](https://github.com/open-legal-products/mike) | **AGPL-3.0** ⚠️ | EE. UU. · North America | "OSS Legal AI Platform" estilo Harvey. **Pasó de «—» a 4.504★ en esta KB: es la plataforma legal AI open source más grande que existe.** Primera publicación 29-abr-2026. ⚠️ AGPL-3.0 (copyleft de red): inviable para producto SaaS cerrado sin liberar el derivado. Referencia de arquitectura y *benchmark competitivo*, no base de código. | **4.504** | 2026-11-19 |
| Korean Law MCP | [chrisryugj/korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) | MIT (1.062 B) | Corea del Sur · APAC | Envuelve **las 42 APIs oficiales del 법제처** (Ministerio de Legislación) en 10 herramientas MCP: leyes, jurisprudencia, reglamentos administrativos, normativa autonómica, tratados e interpretaciones (incl. Agencia Tributaria). **Y contrasta las citas legales de la respuesta del LLM contra el texto original** — verificación de cita como función, no como promesa. Publicado en npm y en el MCP Registry. | **2.904** | 2026-11-20 |
| Claude für deutsches Recht | [Klotzkette/claude-fuer-deutsches-recht](https://github.com/Klotzkette/claude-fuer-deutsches-recht) | Apache-2.0 (11.358 B) | Alemania · EMEA | Plugins, skills y prompts para la práctica jurídica alemana (despachos, departamentos legales, consultoras): instrucción de expedientes, verificación de fuentes, contratos, escritos, memos y propuestas de resolución. Incluye **Testakten** — expedientes ficticios completos para ensayar los flujos sin datos reales. README de 115.817 B. | **1.866** | 2026-11-20 |
| ContextGem | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | Polonia/UE · EMEA | Extracción estructurada con LLMs: defines *aspects* y *concepts* tipados en lenguaje natural. Devuelve tipos (fecha, número, label, rating, JSON) **con trazabilidad al párrafo/oración de origen**. Lee todos los párrafos — **no hace chunking por retrieval**, así que no se le escapa una cláusula por quedar mal rankeada. | 2.095 | 2026-11-09 |
| CaseCite | [thomasunise/casecite](https://github.com/thomasunise/casecite) | Apache-2.0 (11.358 B) | Global | **El hallazgo más alineado con lo que esta KB dice que pide el mercado.** Plataforma legal RAG self-hosted y BYOK, **sin telemetría**: retrieval híbrido sobre chunks que conocen su sección y página, **cada afirmación contrastada contra el pasaje que cita**, deep research sobre corpus propio + CourtListener, pipeline de contratos con export de redline, y *tabular review* de cientos de contratos con cada valor atado a su pasaje de soporte. Conectores Drive/OneDrive/Box/Dropbox/Filevine/Clio. | 286 | 2026-11-05 |
| Presidio | [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT (1.084 B) | Global | Detección, redacción, enmascarado y anonimización de PII en texto, imágenes y datos estructurados. Pieza obligatoria antes de enviar documento de cliente a cualquier LLM externo. ⚠️ **RENOMBRADO** — ver aviso abajo. | **11.989** | 2026-11-19 |
| OpenContracts | [Open-Source-Legal/OpenContracts](https://github.com/Open-Source-Legal/OpenContracts) | MIT (1.073 B) | EE. UU. · North America | "The open document intelligence platform for builders and hackers — DMS for the agentic world". Repositorio de contratos + analítica de cláusulas + anotación. Django + frontend JS. ⚠️ **RENOMBRADO** — ver aviso abajo. | 1.550 | 2026-11-20 |
| LawGlance | [lawglance/lawglance](https://github.com/lawglance/lawglance) | Apache-2.0 (11.343 B, `LICENSE.md`) | India · APAC | Asistente legal RAG libre y open source. **Primer activo legal de la India en esta KB** y uno de los pocos no anglosajones con mantenimiento real. | 343 | 2026-09-21 |
| lavern | [AnttiHero/lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | Global | "An agentic law firm. Yours." 67 agentes especialistas que revisan documentos mediante *evidence-backed debate*, con **human gates obligatorios** (los hallazgos críticos no se entregan sin aprobación humana) y pipeline de verificación de 10 pasos. TypeScript. | 326 | 2026-09-05 |
| claude-legal-skill | [evolsb/claude-legal-skill](https://github.com/evolsb/claude-legal-skill) | MIT | Global | Skill de revisión de contratos con detección de riesgo basada en CUAD y benchmarking de mercado. **Primera medición de estrellas de esta fila**: el pase anterior la publicó con «—». | 518 | 2026-07-23 |
| contract-review | [lowtidebuild/contract-review](https://github.com/lowtidebuild/contract-review) | Apache-2.0 (11.284 B) | Global | Revisión de contratos local-first. Produce **DOCX con tracked changes** (redline interno, limpio externo y reporte), comentarios al margen y recomendaciones de negociación. ⚠️ **SLUG CORREGIDO** en el pase 3: se publicaba como `…/contract-review-agent`, que es un renombrado (mismo HEAD `e16315dd…`). ⚠️ **Y NO ESTÁ «ACTIVO»**: 4 meses sin commits, 41★. Útil como referencia de *cómo* se emite un redline en DOCX, no como base mantenida. | 41 | **2026-07-24** 🪦 |
| Claude para Abogados | [betobetico/claude-para-abogados](https://github.com/betobetico/claude-para-abogados) | Apache-2.0 (11.358 B) | **España** · EMEA | Adaptación declarada de `claude-for-legal` al **ordenamiento jurídico español y de la UE**: 20 módulos, 100 skills, 17 agentes, por área (mercantil, societario, laboral, IP, procesal, privacidad, consumo, regulatorio, gobernanza de AI, fiscal, concursal, familia…). Atribuye explícitamente el diseño a Anthropic. ⚠️ **Es derecho de España, NO de LATAM** — ver el hueco LATAM abajo. | 49 | 2026-09-30 |
| mcp-legal-it | [capazme/mcp-legal-it](https://github.com/capazme/mcp-legal-it) | Apache-2.0 | **Italia** · EMEA | Servidor MCP + plugin de Claude para derecho italiano, 200+ herramientas con statutes verificados. Pequeño pero real y mantenido. | 33 | 2026-11-18 |
| Blackstone | [ICLRandD/Blackstone](https://github.com/ICLRandD/Blackstone) | Apache-2.0 | Reino Unido · EMEA | Pipeline y modelo spaCy para NLP sobre texto legal no estructurado (rama `master`). Se declara *early prototype*. 🪦 **Sin commits desde 2024-07-16 — 28 meses.** Esta KB lo vendía como «base de NER legal» sin decirlo. | 702 | 2024-07-16 |
| DISC-LawLLM | [FudanDISC/DISC-LawLLM](https://github.com/FudanDISC/DISC-LawLLM) | Apache-2.0 | China · APAC | 中文法律大模型 — sistema legal inteligente sobre LLM para derecho chino (Fudan DISC). 🪦 **18 meses sin commits.** | 961 | 2025-05-27 |
| lawyer-llama | [AndrewZhe/lawyer-llama](https://github.com/AndrewZhe/lawyer-llama) | Apache-2.0 | China · APAC | LLM legal chino con instruction-tuning jurídico. Nuevo en esta KB. 🪦 **27 meses sin commits.** | 1.003 | 2024-08-28 |
| fuzi.mingcha (夫子·明察) | [irlab-sdu/fuzi.mingcha](https://github.com/irlab-sdu/fuzi.mingcha) | Apache-2.0 | China · APAC | LLM judicial chino (U. de Shandong + Inspur Cloud + CUPL) sobre base ChatGLM. 🪦 **16 meses sin commits.** | 401 | 2025-07-30 |
| **legal-skills-open** | [ThomasMoreAI/legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | Apache-2.0 (11.314 B) | Global · **54 jurisdicciones** | **El hallazgo que refuta el hueco LATAM de esta KB.** Biblioteca abierta de skills legales en formato `SKILL.md` para agentes compatibles con MCP: 18.000+ skills, 410+ plugins, 48 áreas de práctica, agrupados **por jurisdicción** (`br/`, `mx/`, `ar/`, `co/`, `pe/`, `do/`, `es/`…). Apache-2.0 sobre el contenido, no sólo sobre el código. Ver la corrección al hueco LATAM abajo. | 141 | 2026-10-12 |
| **opencaselaw** | [jonashertner/opencaselaw](https://github.com/jonashertner/opencaselaw) | **MIT código (1.069 B) + CC0 datos** | **Suiza** · EMEA | **El mejor activo del pase, y el primero que resuelve el problema del corpus permisivo.** Corpus legal suizo abierto: **1M+ sentencias de los 26 cantones, 1875–hoy**, 21k leyes, **grafo de citas de 10M de aristas**, 42 herramientas MCP, más REST, CLI y **Parquet** para análisis a escala de corpus. Alemán, francés e italiano. `ocl citations resolve 'BGE 136 III 513'` dice **si la sentencia existe y cuál es** — primitiva de verificación de cita ejecutable, no prometida. Vivo en `mcp.opencaselaw.ch`. | 80 | 2026-11-20 |
| devnors-data-mcp | [DevnorsAI/devnors-data-mcp](https://github.com/DevnorsAI/devnors-data-mcp) | MIT (1.064 B) | China · APAC | Servidor MCP sobre datos legales y corporativos chinos: **裁判文书** (sentencias), **法律法规/法条** (leyes y articulado), registro mercantil, cuentas anuales, datos fiscales y **失信核查/被执行人** (listas de morosos judiciales y ejecutados). Es la pieza que faltaba para due diligence de contraparte en China. | 796 | 2026-09-15 |
| tw-legal-rag | [aa0101181514/tw-legal-rag](https://github.com/aa0101181514/tw-legal-rag) | ⚠️ **Elastic License 2.0** (4.044 B) — **MIT sólo hasta v1.2.2** | **Taiwán** · APAC | MCP + CLI de derecho taiwanés: **22,8 M de sentencias**, interpretaciones administrativas y resoluciones del Tribunal Constitucional, **con verificación de cita incorporada**. Retrieval-only, BYO-LLM. ⚠️ **Relicenciado: v2.0.0+ es ELv2 (prohíbe servicio gestionado a terceros y manipular la clave de licencia). Ver el modo de fallo nuevo abajo.** | 350 | 2026-11-12 |
| mcp-taiwan-legal-db | [lawchat-oss/mcp-taiwan-legal-db](https://github.com/lawchat-oss/mcp-taiwan-legal-db) | MIT (1.092 B) | **Taiwán** · APAC | Sentencias del 司法院 (Yuan Judicial) + **全國法規資料庫** (base nacional de normativa) como servidor MCP consultable desde cualquier agente. **La alternativa permisiva a `tw-legal-rag`** para la misma jurisdicción: menos corpus, licencia limpia. | 234 | 2026-10-21 |
| legal-research-skill | [Golden2002/legal-research-skill](https://github.com/Golden2002/legal-research-skill) | MIT (1.066 B) | China · APAC | Agent Skill de búsqueda jurídica para Cursor, Claude Code y OpenCode: localización y ordenación sistemática de normas, pensada tanto para no juristas como para profesionales. | 168 | 2026-08-28 |
| contract-review (中文) | [xiaodingfeng/contract-review](https://github.com/xiaodingfeng/contract-review) | MIT (1.069 B) | China · APAC | App web de revisión de contratos en chino: carga, preanálisis AI, **puntos de revisión configurables**, previsualización y edición con **OnlyOffice**, base de conocimiento, refuerzo con sentencias y búsqueda web controlada. El flujo completo, no un wrapper de prompt. | 168 | 2026-08-05 |
| due-diligence-agents | [zoharbabin/due-diligence-agents](https://github.com/zoharbabin/due-diligence-agents) | Apache-2.0 (10.762 B) | Global | Due diligence forense de M&A: **13 agentes leen el data room en 9 dominios** (legal, financiero, comercial, tecnología, ciber, RR. HH.…) y **cruzan hallazgos entre dominios con cita** — un riesgo legal y uno financiero que se conectan. El único activo de la KB que opera a nivel transacción, no documento. | 139 | 2026-11-17 |
| Vaquill MS Word add-in | [Vaquill-AI/ms-word-addin](https://github.com/Vaquill-AI/ms-word-addin) | Apache-2.0 (11.340 B) | Global | **Cierra en licencia permisiva el canal que esta KB declara decisivo para la adopción: Word.** Add-in de task-pane para MS Word con revisión de contratos, **playbooks**, redacción e investigación legal. Del mismo equipo que `awesome-legaltech`. | 81 | 2026-10-01 |
| ayunis-legal-mcp | [ayunis-core/ayunis-legal-mcp](https://github.com/ayunis-core/ayunis-legal-mcp) | MIT (1.070 B) | **Alemania** · EMEA | Servidor MCP sobre los códigos legales alemanes. Complemento permisivo y mantenido de `claude-fuer-deutsches-recht` (que aporta los flujos, no las fuentes). | 91 | 2026-11-08 |
| italia-mcp-servers | [bsab/italia-mcp-servers](https://github.com/bsab/italia-mcp-servers) | MIT (1.069 B) | **Italia** · EMEA | Catálogo curado de servidores MCP italianos: datos públicos, legal-tech, facturación y administración pública. Mapa de entrada para un engagement italiano. | 78 | 2026-09-11 |
| us-legal-mcp | [JamesANZ/us-legal-mcp](https://github.com/JamesANZ/us-legal-mcp) | MIT (1.071 B) | EE. UU. · North America | Servidor MCP sobre legislación federal estadounidense. Pequeño, pero licencia limpia y mantenido. | 39 | 2026-10-15 |
| doc-haus | [sure-scale/doc-haus](https://github.com/sure-scale/doc-haus) | **GPL-3.0** ⚠️ (35.149 B) · rama **`dochaus`** | Global | "The open-source legal AI agent": los documentos **no salen del disco** y los redlines llegan a Word como **tracked changes**. Fork de OpenCode. ⚠️ GPL-3.0: copyleft fuerte: contamina el derivado distribuido. Para despliegue interno de cliente es viable; para producto cerrado no. | 83 | 2026-11-14 |
| bettercallclaude | [fedec65/bettercallclaude](https://github.com/fedec65/bettercallclaude) | **AGPL-3.0** ⚠️ | **Suiza** · EMEA | Plugin de Claude Cowork Desktop para la práctica jurídica suiza. Par natural de `opencaselaw` (flujos + corpus). ⚠️ AGPL-3.0. | 47 | 2026-09-20 |
| awesome-legal-skills | [lawve-ai/awesome-legal-skills](https://github.com/lawve-ai/awesome-legal-skills) | 🔴 **CC-BY-NC-ND 4.0** (19.122 B) | Global | Lista curada de Agent Skills para automatizar trabajo legal. 966★, el índice de skills legales más grande. 🔴 **NO USABLE POR GLOBANT TAL CUAL: NonCommercial + NoDerivatives.** Ver el aviso de licencia abajo: es el peor régimen de los que aparecen en esta KB y el que menos lo parece. | **966** | 2026-10-19 |
| 🔴 **ai-legal-claude** | [zubair-trabzada/ai-legal-claude](https://github.com/zubair-trabzada/ai-legal-claude) | 🔴 **NINGUNA** (no existe `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE` ni `COPYING`) | Global | **El segundo repo de agente legal más estrellado que existe tras `claude-for-legal`, y no se puede usar.** Skill de asistente legal para Claude Code: revisión de contratos, análisis de riesgo, generación de NDA y compliance. 🔴 **Sin fichero de licencia ⇒ «todos los derechos reservados» por defecto: sin licencia expresa no hay derecho de uso, copia ni derivado.** Se publica aquí **precisamente para que nadie lo vuelva a encontrar y lo adopte por las estrellas.** 🆕 **PASE 4 — y las estrellas tienen una causa medible: su propia `description` termina en *«If you want to learn how to sell this to real businesses, check out the Skool community»*, es decir el repo es el gancho de una comunidad de pago.** Ver el modo de fallo *embudo de venta* abajo. 🪦 8 meses sin commits. | **1.852** | 2026-03-27 |
| 🆕 **stella** | [stella/stella](https://github.com/stella/stella) | Apache-2.0 (11.358 B) | Global | 🆕 **Workspace legal open source con commit de hoy mismo.** Permisivo, bajo nombre de organización propia (no de autor individual), lo que en este sector es señal de proyecto con intención de continuidad. Candidato directo a base de despliegue de cliente. Ver `verticals/solutions.md`. | 282 | **2026-11-20** |
| 🆕 **Prism-Legal-OS** | [FuturixAI-and-Quantum-Works/Prism-Legal-OS](https://github.com/FuturixAI-and-Quantum-Works/Prism-Legal-OS) | **AGPL-3.0** ⚠️ (34.523 B) | India · APAC | 🆕 AI legal open source para **análisis de contratos, investigación jurídica y litigio** en un solo sistema. **Segundo activo legal de la India en esta KB** (con `lawglance`), y bastante más ambicioso en alcance. ⚠️ AGPL-3.0: copyleft de red, inviable para SaaS cerrado; válido como referencia de arquitectura y para despliegue interno. | 226 | 2026-10-03 |
| 🆕 **judicex** | [JustVugg/judicex](https://github.com/JustVugg/judicex) | Apache-2.0 (11.357 B) | Global | 🆕 Workspace legal para **redacción fundada en evidencia, análisis de expediente y respuestas verificables** — el vocabulario exacto de la tendencia de verificación de cita, y con licencia permisiva. 🪦 Pero **6 meses sin commits**: patrón de referencia, no base mantenida. | 69 | 2026-05-16 |
| 🆕 **hermes-legal** | [Lethe044/hermes-legal](https://github.com/Lethe044/hermes-legal) | MIT (1.065 B) | Global | 🆕 Análisis de contratos multi-proveedor: **puntúa riesgo, propone redlines y emite una recomendación de firmar/negociar**. Pequeño pero MIT limpio y con la decisión de negocio como salida, no sólo el análisis. | 26 | 2026-10-10 |
| 🆕 contract-review-pro | [CSlawyer1985/contract-review-pro](https://github.com/CSlawyer1985/contract-review-pro) | 🔴 **NINGUNA** | China · APAC | 🆕 专业合同审核 Skill — revisión de contratos construida sobre metodología de auditoría contractual, para juristas chinos. 🔴 **Sin fichero de licencia: no adoptable.** Se registra por volumen de señal (311★) y como medida del tamaño del problema de licencias en APAC. | 311 | 2026-08-14 |
| 🆕 legal-ai-agent | [Paparusi/legal-ai-agent](https://github.com/Paparusi/legal-ai-agent) | MIT (1.083 B) | Vietnam · APAC | 🆕 MIT limpio y 214★, pero **el repo no declara descripción ni alcance**: no se puede afirmar qué hace sin auditar el código. Se registra como **candidato a auditar**, no como recomendación. Ejemplo de por qué «licencia limpia + estrellas» no basta para recomendar. | 214 | 2026-03-21 |
| 🟢 **br-eli-mcp** | [matematicsolutions/br-eli-mcp](https://github.com/matematicsolutions/br-eli-mcp) | Apache-2.0 (11.358 B) | **Brasil · LATAM** | 🟢 **EL ACTIVO QUE REFUTA EL HUECO MÁS CITADO DE ESTA KB.** Servidor MCP de **fuentes legales oficiales brasileñas**, 8 APIs de datos abiertos **sin clave ni registro**: Câmara (proyectos), Congresso (normas promulgadas + publicación en Diário Oficial + histórico de enmiendas), `normas.leg.br` (texto a nivel de artículo), **DataJud/CNJ** (metadatos procesales), **STJ** (texto íntegro + ementas desde may-2022), **CARF** (fiscal federal), **TST** (texto íntegro, búsqueda libre + número CNJ), **TCU**. Declara citas verificables y **no hace scraping del HTML de Planalto**. | 4 | **2026-11-21** |
| 🟢 **mcp-dof** | [BEG-lag/mcp-dof](https://github.com/BEG-lag/mcp-dof) | MIT (1.082 B) | **México · LATAM** | 🟢 **ES, LITERALMENTE, LO QUE ESTA KB PEDÍA CONSTRUIR.** MCP del **Diario Oficial de la Federación** sobre la **API oficial SIDOF** (`sidof.segob.gob.mx`): ediciones diarias, texto íntegro de decretos, búsqueda por título, e indicadores FIX/UDIS/TIIE. Python 3.12+. ⚠️ La API oficial **no está documentada**: el repo mapeó los endpoints (`/notas/{fecha}`, `/notas/nota/{id}`, `/indicadores/...`) por sondeo manual — eso es deuda de mantenimiento, no defecto de licencia. | 0 | **2026-11-17** |
| 🟢 **leis-mcp** | [mazulo/leis-mcp](https://github.com/mazulo/leis-mcp) | MIT (1.071 B) | **Brasil · LATAM** | 🟢 **El de más tracción de los cuatro, y el que desmonta la explicación fácil.** MCP de legislación brasileña: **1.218.990 normas** (CF, CLT, CDC, Código Civil, LGPD…) con cita de fuente oficial (`normas.leg.br`, LexML) y **avisos de revogação**; valida vigencia contra normas.leg.br y datos abiertos del Senado. ⚠️ El README advierte de errores de conversión/OCR y de que **no sustituye la publicación en el Diário Oficial**; la búsqueda sin norma concreta sólo cubre lo ya cacheado. | **71** | **2026-11-13** |
| 🟢 **jurismcp** | [ivancaron/jurismcp](https://github.com/ivancaron/jurismcp) | MIT (1.078 B) | **Brasil · LATAM** | 🟢 **Jurisprudencia, no legislación — la mitad que faltaba.** Consulta **portales judiciales oficiales**: STJ (POST directo), STF y TST (navegador headless), TJES (REST pública), **LexML** (federado, resuelve `urn:lex`), **BNP/CNJ** (registro de precedentes `pangeabnp.pdpj.jus.br`), TNU y TRF4 (formularios eproc). **Marca explícitamente Jurisprudencias.ai como agregador de terceros, no portal oficial, y es opt-in** — hace por su cuenta la distinción que esta KB necesita. ⚠️ Scraping/headless ⇒ frágil ante cambios de portal. | 2 | 2026-09-30 |
| 🟡 **jusbrasil-mcp** | [mcp-dir/jusbrasil-mcp](https://github.com/mcp-dir/jusbrasil-mcp) | MIT (1.093 B) | Brasil · LATAM | 🟡 **SE REGISTRA PARA QUE NO SE CONFUNDA CON LOS CUATRO DE ARRIBA.** MIT limpio, pero es un **agregador de terceros** (se describe como «alternativa a Escavador y Jusbrasil»), **no fuentes oficiales**: busca procesos por nombre/CPF/CNPJ y arma un «X-ray» consolidado. Su posicionamiento SEO lo pone primero en cualquier búsqueda de «MCP jurídico Brasil» ⇒ **un pase futuro lo encontrará antes que a los oficiales y puede darlo por oficial.** Para citación defendible **no sirve**; para triage comercial, sí. | 6 | 2026-08-30 |
| 🟢 **legal-ai-skills** | [rohasnagpal/legal-ai-skills](https://github.com/rohasnagpal/legal-ai-skills) | MIT (1.069 B) | India · APAC (+ EE. UU., RU, Singapur) | 🟢 **La alternativa PERMISIVA al índice de skills que esta KB marca como no usable.** 244 skills legales (revisión de contratos, investigación, due diligence, análisis de evidencia, redacción) organizadas bajo **17 «abogados» especialistas + un Managing Partner que enruta** el asunto. Jurisdicciones con *Jurisdiction Counsel* propio: India, EE. UU., RU y **Singapur (18 skills locales, la cuarta añadida)**; el resto, neutras. Frente a `lawve-ai/awesome-legal-skills` (CC-BY-NC-ND, 966★): **un tercio de las estrellas y todos los derechos que hacen falta.** ⚠️ El propio README advierte que sus salidas no garantizan exactitud. | **215** | **2026-11-12** |
| 🆕 **kancelaria-lex** | [AI4CharityPL/kancelaria-lex](https://github.com/AI4CharityPL/kancelaria-lex) | MIT (1.069 B) | **Polonia** · EMEA | 🆕 **El mejor activo nuevo del pase 5, y el que mejor encarna la tendencia nº1 de esta KB.** AI **totalmente local** para analizar expedientes judiciales polacos. **La localidad está impuesta por arquitectura, no prometida en el README:** cuatro segmentos Docker, **tres con `internal: true`**, así que no existe ruta hacia la pasarela. **Integridad de cita por construcción:** el código reconstruye el texto desde el documento fuente y lo compara **carácter a carácter**; una cita fabricada no puede sobrevivir al verificador. Declara **0 citas inconsistentes con la fuente en todas las corridas de medición** y precisión de cita **>80%**, contra el **17–34% de citas fabricadas** de las herramientas comerciales (el mismo estudio de Stanford que cita esta KB). **Y distingue la procedencia del OCR:** lo leído con Tesseract lleva **marcador permanente** y cada cita muestra `z OCR`, porque «la cita apunta a un carácter exacto del expediente» y «…de **la lectura de un escaneo**» no son la misma afirmación. Perfiles locales con TOTP. MIT explícito: «úsalo, vende servicios alrededor, bifúrcalo». | 60 | 2026-08-23 |
| 🆕 **Kourti Legal** | [boyeesu/Kourti](https://github.com/boyeesu/Kourti) | MIT (1.069 B) | **Nigeria** (Lagos) · EMEA | 🆕 **CIERRA EL HUECO DE *PRACTICE MANAGEMENT* PERMISIVO QUE ESTA KB DECLARABA ABIERTO DESDE EL PASE 1** — y es el **primer activo africano** de esta KB. Workspace para **expedientes, documentos, clientes y plazos**: React + API Node + PostgreSQL, `docker compose up` y listo, workflow de CI, `SECURITY.md`, documentación de self-hosting y aviso explícito de que el contenido AI debe revisarlo un profesional. **524 refs** en `ls-remote` (ramas `chore/oss-release-prep`, `agent/codeql-remediation`): código real, no un esqueleto. ⚠️ **1★ y sin `description` ni `topics` en GitHub** — invisible para los tres controles de descubrimiento de esta KB. Ver el hallazgo G-L10 abajo. | 1 | 2026-11-01 |
| 🆕 **legal-agent-workshop** | [meta-models/legal-agent-workshop](https://github.com/meta-models/legal-agent-workshop) | MIT | Global | 🆕 **El activo de *enablement* que esta KB no tenía: el patrón de verificación como material de formación ejecutable.** Dos sesiones: (1) construir el agente legal — bucle agéntico en SDK de OpenAI en Python, una herramienta por fichero, lectura de documentos por Files API, gestión de expediente con hechos *quote-checked*, y termina en un memo **sin verificar**; (2) **hacerlo confiable** — se construyen los dos controles de la capa de verificación (checklist contra la verdad de base del expediente, y reglas del memo) **que el kit ejecuta FUERA del control del agente**, más rechazos, escalado, liberación de evidencia nueva, reanudación y **firma del abogado**. Incluye caso de trabajo (`northbridge-v-caldera`) y consola de ejecución en vivo. | 73 | 2026-11-06 |
| 🆕 **CourtListener MCP** | [cyanheads/courtlistener-mcp-server](https://github.com/cyanheads/courtlistener-mcp-server) | Apache-2.0 (11.317 B) | EE. UU. · North America | 🆕 **El puente MCP al expediente federal, y la cara que faltaba de CourtListener en esta KB.** Esta KB citaba CourtListener 40 veces como *corpus de jurisprudencia* (AGPL-3.0) y no tenía el acceso al **docket**: opiniones, **dockets federales**, fichas de jueces y redes de citación vía la API de CourtListener/RECAP. La diferencia importa porque el corpus sirve para investigar y el docket sirve para **litigar** (plazos, escritos presentados, histórico procesal). Apache-2.0 sobre el cliente, aunque el servidor de datos siga siendo AGPL: se integra sin contaminar el derivado. 72 refs. | 4 | 2026-11-21 |
| 🆕 **legal-hold-manager** | [noamrazbuilds/legal-hold-manager](https://github.com/noamrazbuilds/legal-hold-manager) | MIT (1.090 B) | EE. UU. · North America | 🆕 **Primer activo de *legal hold* de esta KB — una categoría con 0 menciones en los 8 ficheros antes de hoy.** Crea, emite, sigue y gestiona órdenes de conservación con seguimiento de **custodios**. Es la obligación que nace ANTES del e-discovery: si la conservación falla, el caso se pierde por sanción (FRCP 37(e)) y no por el fondo. ⚠️ 1★, 2 refs, sin actividad desde 2026-03: **esqueleto correcto de una categoría vacía**, no producto. Se publica como punto de partida, con la advertencia. | 1 | 2026-03-06 |
| 🆕 **deposition-contradiction-analysis** | [TaylorLegalEngineering/deposition-contradiction-analysis](https://github.com/TaylorLegalEngineering/deposition-contradiction-analysis) | MIT (1.086 B) | EE. UU. · North America | 🆕 Pipeline multi-agente de **5 rondas** que busca contradicciones en transcripciones de **deposición**. Capa nueva en esta KB (`deposition` y `transcript`: 0 menciones antes de hoy). El flujo tiene la propiedad que esta KB premia: la salida es **una lista de pasajes citados con referencia a línea**, es decir el abogado verifica contra el acta, no contra el modelo. ⚠️ 2★. **Y tiene una copia con descripción idéntica** (`EyeOfHorus158/CompraX`) — se registra para que un pase futuro no la cuente como hallazgo independiente. | 2 | 2026-03-11 |
| 🆕 **depo-summarizer** | [Mermiges/depo-summarizer](https://github.com/Mermiges/depo-summarizer) | MIT (1.070 B) | Global | 🆕 Resumen de transcripciones de deposición **con LLM local** y cuatro formatos de salida. Encaja con la tendencia nº1 de esta KB (soberanía del dato): el acta de una deposición contiene testimonio bajo juramento y datos de terceros, y es exactamente el documento que no debe salir del despacho. ⚠️ 0★, 2 refs, sin actividad desde 2026-03. | 0 | 2026-03-20 |
| 🆕 **DepoIndex** | [crowaltz24/DepoIndex](https://github.com/crowaltz24/DepoIndex) | MIT (1.062 B, cuerpo MIT sin línea de título) | Global | 🆕 Indexa transcripciones de deposición para producir el **índice por temas y testigos** que el litigante usa para preparar el juicio. Completa la terna de la capa de deposición junto a las dos filas anteriores. ⚠️ 0★, 5 refs, última actividad 2025-09. **Su `LICENSE.md` empieza directamente por `Copyright (c) 2025` sin la línea `MIT License`** — el texto es MIT íntegro, pero es otro caso del modo de fallo que esta KB mide: el clasificador acierta y el título engaña. | 0 | 2025-09-08 |
| 🆕 **legal-agent-skills (CN)** | [Decikingship/legal-agent-skills](https://github.com/Decikingship/legal-agent-skills) | MIT (1.081 B) | **China** · APAC | 🆕 **La plaza de China en el patrón «plantilla por jurisdicción», que esta KB tenía documentado para EE. UU., RU, India, Singapur, Alemania, Polonia y España pero no para la segunda jurisdicción del mundo por volumen.** 60 skills legales chinas + **33 flujos de trabajo expertos**, con herramientas Python, **evaluaciones** y material de despliegue. Las evaluaciones son lo que lo separa de un paquete de prompts. 6 forks en 6 semanas. | 23 | 2026-10-14 |
| 🆕 **AI-Legal-SkillsPL** | [GSkuza/AI-Legal-SkillsPL](https://github.com/GSkuza/AI-Legal-SkillsPL) | MIT (1.063 B) | **Polonia** · EMEA | 🆕 Paquetes de skills legaltech para derecho **polaco y de la UE**. Es el **segundo** activo polaco permisivo de esta KB tras `kancelaria-lex`, y confirma que Polonia es hoy el clúster legaltech abierto más activo de EMEA fuera de los grandes mercados. | 7 | 2026-10-13 |
| 🆕 **judgment-compiler** | [jordanteague/judgment-compiler](https://github.com/jordanteague/judgment-compiler) | MIT (1.070 B) | Global | 🆕 **Compila el criterio experto de un abogado en *playbooks* estructurados y validados que la AI aplica de forma consistente.** Invierte la dirección habitual del producto: no es la AI la que decide y el humano la revisa, es **el humano el que fija la regla y la AI la ejecuta sin desviarse** — el patrón que esta KB viene recomendando desde el pase 2 para flujos con responsabilidad profesional detrás. 3 forks en un mes. | 12 | 2026-10-26 |
| 🆕 **eidas-validator** | [juraj-jumic/eidas-validator](https://github.com/juraj-jumic/eidas-validator) | MIT (1.068 B) | **UE** · EMEA | 🆕 Validador **en lenguaje llano** de firmas electrónicas cualificadas (eIDAS) en PDF: traduce un informe de validación técnico a una afirmación que un abogado puede usar. Es la pieza de arriba de la capa de conformidad de firma que este pase añade a `repos/foundations.md` (`pyHanko`, `esig/dss`). ⚠️ 0★, 4 refs, creado 2026-10-12: **la categoría es nueva, no madura.** | 0 | 2026-10-12 |

**⚠️ CIFRA CORREGIDA EN EL PASE 9 — eran 49, no 43.** El total se contó con script antes de tocar la tabla: **49 filas antes del pase 9, 58 después** (+9 este pase). La cifra «43» quedó congelada en el pase 3 y los pases 5–8 añadieron filas sin actualizarla. Todas las filas están verificadas por API de búsqueda + lectura byte a byte de `LICENSE`. **0 filas de ejemplo, 0 placeholders.** (33 del pase 2, revalidadas una por una en el pase 3; 7 nuevas en el pase 3. De las 7 nuevas, **3 se publican como NO ADOPTABLES** — ver el clúster de licencias de abajo.) 🆕 **PASE 5 (2026-11-21): +3 filas** (`kancelaria-lex`, `Kourti Legal`, `legal-agent-workshop`), las tres MIT y verificadas por los dos canales. **Y una reparación estructural: esta tabla estaba PARTIDA EN DOS** — una línea en blanco dejaba 7 filas sin cabecera. Ver abajo.

> 📌 **Cómo leer la columna «Último commit»:** es `pushed_at` medido, no una impresión. 🪦 marca
> dormancia > 6 meses. Un repo dormido **no** se retira: sigue sirviendo como patrón y como corpus.
> Lo que cambia es **qué se le promete a un cliente** — no se ofrece soporte sobre un repo que
> nadie toca desde hace medio año.


## ⚠️ TRES renombrados (el tercero se detectó en el pase 3) — ahora con prueba de SHA

Esta KB apuntaba a slugs que ya no son canónicos. **Ninguno es un 404**, y por eso el método
antiguo (sólo `raw`) no podía verlos. **Los tres están ahora probados por identidad de HEAD**, que
es una prueba de que *es el mismo repositorio* y no sólo de que *se parece*:

| Slug publicado (obsoleto) | Slug canónico hoy | Prueba (HEAD vía `git ls-remote`) |
|---------------------------|-------------------|-----------------------------------|
| `microsoft/presidio` | **`data-privacy-stack/presidio`** | ambos `da946811…` ⇒ mismo repo. 11.990★, MIT 1.084 B. |
| `JSv4/OpenContracts` | **`Open-Source-Legal/OpenContracts`** | ambos `56ca972a…` ⇒ mismo repo. 1.550★, MIT. |
| 🆕 `lowtidebuild/contract-review-agent` | **`lowtidebuild/contract-review`** | ambos `e16315dd…` ⇒ mismo repo. 41★, Apache-2.0. **El owner no cambió; cambió el nombre del repo.** |

**Firma del renombrado, idéntica en los tres casos:** `repo:<slug-viejo>` devuelve **HTTP 422**
mientras `raw` sobre el slug viejo devuelve **200**, porque GitHub sirve el contenido por
redirección. Mirando sólo `raw`, el renombrado es invisible; mirando sólo la API, el repo parece
borrado. **Hacen falta los dos — y `git ls-remote` para cerrar cuál es el canónico.**

> ⚠️ **La prueba del pase 2 era insuficiente y se sustituye.** «Mismo MD5 de `LICENSE`» acredita
> que dos repos llevan el mismo texto de licencia, no que sean el mismo repositorio: el texto MIT
> sólo varía en la línea de copyright. Las dos conclusiones del pase 2 eran correctas; su prueba
> no lo era. **Ahora lo son por SHA.**

Tasa medida: **3 renombrados + 1 muerto en 65 URL = ~1 incidencia por 16 repos.** Gaming midió
~1 por 21, enterprise ~1 por 10, legal ~1 por 16. **Es una tasa estable entre industrias, no una
anomalía:** una KB que no revalida slugs acumula punteros muertos a ese ritmo, y el renombrado es
**el modo dominante** (3 de 4 incidencias), no el borrado.

## 🪦 Mortalidad y dormancia — medidas por primera vez en esta KB

`archived` y `pushed_at` **nunca se habían medido aquí** (consecuencia directa de creer la API
bloqueada). Resultados:

- **`TheAtticusProject/cuad` YA NO EXISTE.** El pase anterior lo descartó por «vivo y valioso,
  pero sin fichero LICENSE». Hoy: `repo:` da 422 **y** `raw` da 404 en `main`, `master` y `HEAD`
  para `README.md` y `README.rst`. **El descarte era correcto por la razón equivocada**, y ahora
  es definitivo. CUAD sigue siendo válido como *concepto* de benchmark (claude-legal-skill lo
  usa), pero **el puntero de GitHub está muerto**.
- **Cuatro repos dormidos que esta KB presentaba como activos**: Blackstone (28 meses),
  lawyer-llama (27), DISC-LawLLM (18), fuzi.mingcha (16). Los dos últimos eran, textualmente,
  «los dos activos de APAC» de la KB. **Siguen siendo útiles como modelos y como corpus; no son
  proyectos vivos**, y eso cambia qué se le promete a un cliente.
- `lexpredict-lexnlp`: **30 meses** sin commits (ver `repos/foundations.md`).
- Ningún repo de la tabla está `archived`. El 0-de-18 es un dato, no una omisión.

## ✅ Procedencia RESUELTA — contract-review (era «contract-review-agent»)

El pase 2 dejó esta fila abierta: *«no se pudo determinar el slug canónico actual… el owner puede
haber cambiado»*. **Cerrado en el pase 3, y el owner no había cambiado.**

El README no contiene ningún enlace a `github.com`, así que la vía de los badges no servía. Lo que
funcionó fue **buscar una frase distintiva del README en el índice de código**:

```bash
gh api -X GET search/code -f q='"AI-Powered Contract Review Workflow"'
# -> lowtidebuild/contract-review   <- slug canónico
# -> timc81/bridge                  <- copia (HEAD distinto)
```

- **Canónico: `lowtidebuild/contract-review`** — Apache-2.0 (11.284 B), **41★**, creado
  2026-03-06, `pushed_at` **2026-07-24**, rama `main`. Mismo HEAD `e16315dd…` que el slug viejo.
- **`timc81/bridge`** lleva la misma frase del README con HEAD `25947064…`: **es una copia, no un
  renombrado.** El original es Apache-2.0, que **exige conservar el aviso de copyright y el
  NOTICE**; si un cliente parte de `bridge` hereda una obligación de atribución cuyo origen no
  está declarado en el propio repo. Anotado como riesgo de cadena de licencia, no como hallazgo.

⇒ **El valor de la fila baja mucho al medirla bien**: 41★ y 4 meses dormido no es «la referencia
de redline en DOCX», es **un ejemplo de referencia de cómo se emite un DOCX con tracked changes**.
Para esa función con mantenimiento real, la KB tiene `doc-haus` (GPL-3.0) y
`Vaquill-AI/ms-word-addin` (Apache-2.0).

## 🔴 HALLAZGO AGREGADO DEL PASE 3: LOS REPOS LEGALES MÁS POPULARES *NUEVOS* NO TIENEN LICENCIA

Buscando agentes legales por estrellas en el índice de GitHub (no en listicles), los tres
candidatos nuevos con más tracción **no tienen ningún fichero de licencia**, verificado por dos
canales (la API devuelve `license: null` **y** `raw` devuelve 404 sobre los cinco nombres
canónicos `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING`):

| Repo | Stars | Licencia | Qué es |
|------|------:|----------|--------|
| `zubair-trabzada/ai-legal-claude` | **1.852** | 🔴 ninguna | Skill de asistente legal para Claude Code |
| `Ramseygithub/ai-legal-compliance-assistant` | 342 | 🔴 ninguna | Compliance de precios de bebidas alcohólicas (EE. UU.) |
| `CSlawyer1985/contract-review-pro` | 311 | 🔴 ninguna | Revisión de contratos para juristas chinos |

**≈2.500 estrellas de material legal aparentemente atractivo y jurídicamente inutilizable.** Sin
licencia expresa, el default legal es **todos los derechos reservados**: no hay derecho de uso,
copia ni obra derivada, y el hecho de estar publicado en GitHub no concede ninguno (los Términos
de GitHub conceden al público ver y *hacer fork dentro de la plataforma*, nada más).

**Por qué aparece justo en esta categoría y no es casualidad.** Las tres son *skills* y *prompt
packs*, no librerías: se publican como contenido, desde una cuenta personal, sin el reflejo de
añadir `LICENSE` que tiene quien publica código. **El formato nuevo del sector (SKILL.md, plugin,
prompt pack) trae consigo un déficit sistemático de licencia.** La KB ya tenía dos piezas del
mismo cuadro — `awesome-legal-skills` (CC-BY-NC-ND, el peor régimen) y
`legal-skills-open` (Apache-2.0 **sobre el contenido**, el mejor). Tres regímenes, un mismo
formato.

⇒ 🔧 **Regla operativa:** para un activo de tipo *skill/plugin/prompt pack*, **la licencia se
comprueba antes que la calidad**, porque la probabilidad previa de que no haya licencia es alta.
Y **las estrellas no son señal de adoptabilidad en esta categoría**: el repo sin licencia más
grande de la KB tiene 1.852★, más que 36 de las 40 filas de este fichero.

## 🆕 Dos modos de fallo de licencia nuevos — detectados hoy, ninguno visible en la API

Esta KB ya documentaba el *grant partido código/corpus*. El pase de hoy encontró dos más, y los
dos **se leen como permisivos en el canal rápido**:

### 1. El *copyleft que no lo parece*: CC-BY-NC-ND sobre contenido

`lawve-ai/awesome-legal-skills` (**966★**, el índice de skills legales más grande que existe) sale
como **`NOASSERTION`** en la API de GitHub. El fichero dice:
`Attribution-NonCommercial-NoDerivatives 4.0 International` (19.122 B).

| Cláusula | Consecuencia para Globant |
|----------|---------------------------|
| **NonCommercial** | Un engagement de cliente **es** uso comercial. Bloqueado. |
| **NoDerivatives** | Adaptar una skill a la jurisdicción del cliente **es** una obra derivada. Bloqueado. |

⚠️ **Es el régimen más restrictivo de toda esta KB, y el que menos lo parece**: un repo llamado
`awesome-*` con 966★ se asume MIT por reflejo. **Usar como mapa de lectura, nunca como insumo.**
El sustituto directo existe y es Apache-2.0: **`ThomasMoreAI/legal-skills-open`**.

### 2. El *relicenciamiento con frontera temporal* (el más peligroso de los dos)

`aa0101181514/tw-legal-rag` (350★) también aparece como `NOASSERTION`. Su LICENSE (4.044 B)
**empieza con la palabra «MIT» en los primeros 400 bytes**, así que una comprobación por `grep`
lo clasifica mal. El texto real:

> Elastic License 2.0 (ELv2) — Licensor: Dr.Legal
> *Note: versions up to and including **v1.2.2** were released under the MIT License, which
> continues to apply to those versions.*

**O sea: el mismo repo es MIT en v1.2.2 y ELv2 en v2.0.0+.** ELv2 prohíbe ofrecer el software
como servicio gestionado a terceros — exactamente el modelo de un entregable SaaS de Globant — y
prohíbe tocar la funcionalidad de clave de licencia.

> 🔧 **Regla operativa que esta KB adopta desde hoy:** la licencia se verifica **en el tag que se
> va a usar**, no en `HEAD`. Un repo cuyas estrellas se ganaron bajo MIT puede estar propietario
> hoy, y `HEAD` es lo único que miran los dos canales de verificación.
>
> ```bash
> # la licencia de HEAD NO es la licencia de la versión que vas a fijar
> curl -s https://raw.githubusercontent.com/<owner>/<repo>/v1.2.2/LICENSE | head -3
> ```
>
> Para esta jurisdicción, la alternativa sin frontera temporal es
> **`lawchat-oss/mcp-taiwan-legal-db`** (MIT, 1.092 B, 234★).

## Agentes por función

### Flujos legales completos como plugins (la categoría que faltaba)
- **anthropics/claude-for-legal** (Apache-2.0, 10.054★) — el punto de partida por defecto a
  partir de hoy. Permisivo, mantenido, y con dos vías de despliegue (plugin o Managed Agents API).
- **claude-fuer-deutsches-recht** (Alemania) y **claude-para-abogados** (España) — adaptaciones
  por jurisdicción del mismo patrón. Ver `compose/patterns.md`, receta 7.

### Verificación de cita (el problema nº1 de calidad del sector)
Con tasas de alucinación reportadas del **17–33%** en research legal, la verificación de cita deja
de ser un extra:
- **korean-law-mcp** — contrasta la cita del LLM contra el texto oficial del 법제처.
- **CaseCite** — cada afirmación se comprueba contra el pasaje citado; cada celda de la revisión
  tabular queda atada a su pasaje.
- **ContextGem** — trazabilidad al párrafo como propiedad del framework.

### Revisión y redline de contratos
- **contract-review-agent** — el único que entrega **DOCX con tracked changes**, el formato en que
  un abogado realmente negocia.
- **CaseCite** — pipeline de contratos con export de redline y comparación cláusula a cláusula.
- **claude-legal-skill** — detección de riesgo apoyada en CUAD.

### Repositorio e inteligencia documental
- **OpenContracts** — DMS + analítica de cláusulas; el punto de partida si el cliente necesita
  *dónde viven* los contratos, no sólo revisarlos.

### Privacidad y compliance (transversal, no opcional)
- **Presidio** — de-identificación de PII antes de cualquier egreso a un LLM. Es el componente que
  hace viables los patrones EMEA (EU AI Act) y LATAM (LGPD).

### Orquestación multi-agente con control humano
- **lavern** — su valor para Globant no es el código sino el **patrón**: human gates obligatorios
  + verificación multi-paso. Converge con el Art. 50 del EU AI Act.

### Jurisdicciones específicas

**El patrón de producto del año ya es un clúster medible, no una tendencia.** Hoy la KB cuenta
**13 activos por jurisdicción** frente a 6 en el pase anterior, y la forma dominante es la misma:
**un servidor MCP sobre las fuentes oficiales del país**.

- **North America**: us-legal-mcp (US, MIT), CourtListener (US, AGPL-3.0), FreeEed (e-discovery).
- **EMEA**: ayunis-legal-mcp (DE, MIT) + claude-fuer-deutsches-recht (DE, flujos),
  **opencaselaw (CH, MIT+CC0 — el más completo del clúster)** + bettercallclaude (CH, AGPL-3.0),
  mcp-legal-it + italia-mcp-servers (IT, MIT), claude-para-abogados (ES), oldp (DE, corpus),
  Blackstone (UK, dormido 28 meses).
- **APAC**: korean-law-mcp (KR, 42 APIs oficiales), **tw-legal-rag (TW, 22,8 M sentencias —
  ⚠️ ELv2 en v2+)** y mcp-taiwan-legal-db (TW, MIT, la alternativa limpia), devnors-data-mcp +
  legal-research-skill + contract-review (CN, MIT), LawGlance (IN), DISC-LawLLM / lawyer-llama /
  fuzi.mingcha (CN, los tres dormidos).
- **LATAM**: **flujos sí, fuentes no.** `legal-skills-open` aporta plugins para `br/` (15), `ar/`
  (2), `mx/` (2), `co/` (1), `pe/` (1) y `do/` (1) bajo Apache-2.0. **Servidores MCP de fuentes
  oficiales LATAM: cero.** Ver abajo — el hueco cambió de forma, no desapareció.

## 🟡 Hueco LATAM — **PARCIALMENTE REFUTADO HOY** (era 🔴 hace unas horas)

> ⚠️ **Corrección a lo que este mismo fichero afirmaba en el pase anterior de hoy.** Decía, en
> negrita: *«No existe ninguno para Brasil ni México»*, hablando de adaptaciones por jurisdicción.
> **Es falso, y la causa del error es metodológica:** se buscaron *repos* de origen LATAM y no se
> buscó **cobertura LATAM dentro de repos globales**. El activo existía, con 141★ y Apache-2.0.

**`ThomasMoreAI/legal-skills-open` cubre LATAM, y no de forma simbólica.** Recuento leído del
README (no inferido):

| Jurisdicción | Plugins | | Jurisdicción | Plugins |
|---|---:|---|---|---:|
| 🇧🇷 `br/` Brasil | **15** | | 🇨🇴 `co/` Colombia | 1 |
| 🇦🇷 `ar/` Argentina | 2 | | 🇵🇪 `pe/` Perú | 1 |
| 🇲🇽 `mx/` México | 2 | | 🇩🇴 `do/` Rep. Dominicana | 1 |

**Brasil con 15 plugins es la 9.ª jurisdicción del repo**, por delante de Francia (14), Reino
Unido (14), Italia (10) y España (9). El supuesto de esta KB de que LATAM está vacío en derecho
open source **no se sostiene para Brasil**.

**Lo que sigue siendo cierto, y ahora está cuantificado.** La asimetría, no la ausencia:

- **Alemania 44 y EE. UU. 44 plugins** frente a **Colombia 1, Perú 1, Rep. Dominicana 1**.
  Brasil (15) tiene un tercio de la cobertura de EE. UU.; el resto de LATAM está entre el 2% y
  el 5%.
- 🟢 ~~**No existe ningún servidor MCP de fuentes legales oficiales para ninguna jurisdicción
  LATAM.**~~ **FALSO — REFUTADO EN EL PASE 6 (2026-11-21) CON CUATRO CONTRAEJEMPLOS, TODOS
  PERMISIVOS Y LEÍDOS BYTE A BYTE.** Existen, y existían ya cuando esta KB escribió lo contrario:
  `br-eli-mcp` (Apache-2.0, 8 APIs oficiales brasileñas sin clave, incl. DataJud/CNJ, STJ, TST,
  TCU, CARF), `jurismcp` (MIT, portales judiciales oficiales + LexML + `urn:lex` + BNP/CNJ),
  `leis-mcp` (MIT, 1.218.990 normas con fuente oficial y avisos de revogação) y — el que duele —
  **`mcp-dof` (MIT) para el Diario Oficial de la Federación de México sobre la API oficial SIDOF,
  que es exactamente el ejemplo que esta KB ponía como cosa a construir** («DOF/SCJN para
  México», dos párrafos más abajo). Siguen sin cobertura **Argentina, Chile, Colombia y Perú**:
  el hueco es real pero es **de cuatro países, no de una región**, y eso cambia la propuesta
  comercial de «construir la primera» a «extender una que ya cita fuente oficial». Ver P12
  reescrito en `compose/patterns.md`.
- Sigue sin aparecer ningún agente legal open source **de origen** LATAM con señal. Re-verificado:
  `turborocket-dev/Agente-Assistente-Juridico-De-Contratos` (0★), `jhondados/chatbot-juridico`
  (0★), `manfredjr/legal-br` (MIT, 0★), `desdobroprod-eng/nexus-juris-agente-juridico` (3★).

⚠️ **La trampa de etiquetado se mantiene vigente:** `claude-para-abogados` está en castellano pero
es **derecho de España** → EMEA. Y en `legal-skills-open`, `es/` (9 plugins) es España, no LATAM;
el código LATAM es `br/`, `mx/`, `ar/`, `co/`, `pe/`, `do/`.

⇒ **Oportunidad reformulada, y es mejor que la anterior.** Ya no es «construir desde cero»: es
**(a)** contribuir profundidad a `br/`, `mx/`, `ar/` sobre una estructura Apache-2.0 que ya existe
y acepta contribuciones por jurisdicción, y **(b)** ~~construir el primer MCP de fuentes legales
oficiales de LATAM~~ → **PASE 6: (b) ya está construido para Brasil y México. La oportunidad real
es (b1) extender `br-eli-mcp`/`jurismcp` a los tribunales estatales que no cubren y endurecer el
scraping headless de `jurismcp`, y (b2) construir los que faltan — Argentina, Chile, Colombia,
Perú — copiando `mcp-dof`, que ya resolvió el patrón «API oficial no documentada, mapeada por
sondeo» para un boletín oficial LATAM.** La arquitectura de referencia sigue siendo `opencaselaw`
(26 cantones, 3 idiomas) y `korean-law-mcp` (42 APIs oficiales). Ver `compose/patterns.md` → P7 y
P12 (reescrito).

## Descartes documentados — revalidados este pase

> **Regla aplicada (heredada de la KB de gaming):** *un descarte caduca igual que una
> recomendación.* Un descarte mal fundado es peor que una recomendación débil, porque saca al
> candidato del campo de visión y nadie vuelve a mirar. Estos se re-comprobaron hoy.

- **`TheAtticusProject/cuad`** — descarte **confirmado y endurecido**: ya no existe (antes:
  «vivo, sin LICENSE»).
- **`coastalcph/lex-glue`** — descarte **mantenido**: vivo (276★) pero **`NONE` de licencia**
  confirmado por API. Usable para evaluación interna, no para redistribuir.
- **«Kourti Legal»** — ⚠️ **candidato refutado.** Una fuente lo describía como plataforma de
  *practice management* legal **con licencia MIT y self-hostable**, justo lo que esta KB declara
  como hueco. **No existe tal repo.** Lo que hay bajo ese nombre: `boyeesu/Kourti` (MIT, **1★**),
  `kourti2026/kourti` (0★) y cuatro cuentas personales homónimas sin relación. **El hueco de
  practice management permisivo SIGUE ABIERTO**, ahora con un candidato nombrado y refutado.
- **`mahdyet1845/Consultor-Tributario-AI`** — muerto, confirmado por segunda vez.
- **mythril, heimdall-rs, solgraph** — reales y MIT/ISC, pero son herramientas de seguridad de
  **smart contracts EVM**, no de servicios legales. Entraron por la palabra "contract".
- **`nlpaueb/legal-bert`** — no existe como repo GitHub (es un modelo HuggingFace). ABSENT.
- Repos de 0–2 estrellas sin descripción del pase automático de julio (`ClauseCopilot`,
  `legal-mitra`, `Solidity-Economic-Risk-Scanner`, `arin`, `uk-legal-workflows`): **todos vivos,
  todos verificados hoy**, ninguno con señal. Se conservan en el histórico de `trending`, no aquí.

---
*Verificado 2026-11-20 (**pase 3: auditoría del pase 2**) por tres canales: API de búsqueda
(existencia/★/`pushed_at`/`archived`/rama), lectura byte a byte de `LICENSE` por `raw`, y
`git ls-remote` para identidad de HEAD. **40 filas reales, 0 placeholders, 0 cabeceras como dato.**
Lo que el pase 3 cambió: **1 slug muerto corregido** (`contract-review-agent` → `contract-review`,
probado por SHA), **1 diagnóstico de método refutado** («no indexado» era un renombrado), **3
campos de esa fila corregidos** (★ y liveness falsos), **1 procedencia cerrada** por búsqueda de
código, **7 filas nuevas** (3 de ellas marcadas NO ADOPTABLES por ausencia de licencia) y **5
reglas de instrumento nuevas** (G-L1 identidad de SHA, G-L2 el 422, G-L3 `repos/` no es
instrumento, G-L4 recuperación de slug por búsqueda de código, G-L5 blanqueo de categoría, G-L6
monotonía de estrellas). **Las cifras del pase 2 se revalidaron una por una y se confirman.**
Pases anteriores: 2 renombrados corregidos, 1 repo muerto retirado, 4 dormancias declaradas,
2 modos de fallo de licencia documentados (CC-BY-NC-ND y relicenciamiento ELv2).*


## 🆕 PASE 4 (2026-11-21) — auditoría de las 7 filas que el pase 3 añadió y nadie había auditado

El pase 3 se describió a sí mismo como *«auditoría del pase 2, no reescritura»* y revalidó las 33
filas del pase 2 una por una. **Pero sus propias 7 filas nuevas quedaron sin auditar**, que es la
asimetría estructural de esta rotación: cada pase comprueba el anterior y **publica sin comprobar
lo que añade**. Auditadas hoy por los dos canales:

| Fila del pase 3 | Veredicto del pase 4 | Medición |
|-----------------|----------------------|----------|
| `stella/stella` | ✅ **confirmada, y mejor de lo publicado** | Apache-2.0 **11.358 B** (dentro de la banda 11.300–11.400 ✓), ★282, `archived=false`, **`pushed_at` = 2026-11-21: commit de hoy otra vez**. Y pasa el **gate de pertinencia (P15)**: su `description` es literalmente *«Open-source legal workspace»* — el vertical está **en palabras del repo**, no de un tercero. |
| `FuturixAI-and-Quantum-Works/Prism-Legal-OS` | ✅ confirmada | AGPL-3.0, ★226, `pushed_at` 2026-10-03, `archived=false`. |
| `JustVugg/judicex` | ✅ confirmada, dormancia confirmada | Apache-2.0, ★69, `pushed_at` **2026-05-16** ⇒ 🪦 6 meses, como se publicó. |
| `Lethe044/hermes-legal` | ✅ confirmada **y subvendida** | MIT, ★26, `pushed_at` 2026-10-10. La `description` añade un dato operativo que la fila no recogía: **funciona con los *free tiers* de Groq/Gemini o totalmente offline, sin API key.** Para una prueba de concepto sin coste ni fuga de datos, eso es lo relevante, no las 26★. |
| `CSlawyer1985/contract-review-pro` | ✅ confirmada (no adoptable) | ★311, **`license: NONE`** confirmado por API, `pushed_at` 2026-08-14. |
| `Paparusi/legal-ai-agent` | ✅ confirmada (candidato a auditar) | MIT, ★214, `pushed_at` **2026-03-21** ⇒ 🪦 8 meses. **`description` vacía confirmada por API** (`NO-DESC`): la cautela del pase 3 era correcta. |
| `anthropics/claude-for-legal` | ✅ confirmada | Apache-2.0, **★10.054**, `pushed_at` 2026-11-19, `archived=false`, `default_branch=main`. |

**7/7 confirmadas. 0 correcciones de licencia, 0 renombrados nuevos, 0 filas retiradas.** Es el
primer pase de esta KB que audita al anterior y **no encuentra ningún error de dato** — lo que dice
que el método de los dos canales, ya estabilizado, está funcionando. Lo que sí encuentra es un
**modo de fallo nuevo** y una **prueba de procedencia incompleta** (abajo y en `verticals/`).

### 🔴 G-L8 — MODO DE FALLO NUEVO: *EMBUDO DE VENTA*. LAS ESTRELLAS TIENEN UNA CAUSA, Y A VECES LA CAUSA ESTÁ ESCRITA EN EL REPO

Esta KB ya sabe que las estrellas son un **stock** y no miden vitalidad (G-L6, 932-G6). Falta la
pregunta anterior: **¿miden adopción?** `zubair-trabzada/ai-legal-claude` tiene **1.852★** y era
*«el segundo repo de agente legal más estrellado tras `claude-for-legal`»*. Su `description`
completa termina así:

> *«…negotiation strategy, and PDF reports — 14 skills, 5 parallel agents. **If you want to learn
> how to sell this to real businesses, check out the Skool community**»*

⇒ **El repo es el gancho de captación de una comunidad de pago.** Las 1.852★ miden el alcance de
una campaña de marketing, no el uso por profesionales. Y encaja con el resto de la medición: **sin
fichero de licencia** (⇒ todos los derechos reservados) y **8 meses sin commits** — un activo que
se vende no necesita mantenerse.

**Discriminadores, baratos y en este orden:**
1. Leer la `description` **completa** y buscar llamada a la acción comercial (`Skool`, `course`,
   `community`, `DM me`, `newsletter`, enlace de pago).
2. **Estrellas altas + sin licencia + dormido** es el patrón firma: un proyecto con adopción real
   acaba recibiendo issues y PRs que fuerzan a declarar licencia.
3. Contrastar con el líder de categoría: `claude-for-legal` tiene 10.054★ **y** commit de anteayer
   **y** Apache-2.0. Esa es la forma de una fila con adopción.

> ⚠️ **Y la razón por la que esto importa más que una fila:** el embudo de venta **pasa los tres
> controles que esta KB ya tiene** (existencia ✓, pertinencia ✓ — habla de contratos y NDAs en sus
> propias palabras —, estrellas ✓). Es el **cuarto** control que falta: *¿por qué tiene estas
> estrellas?* **Aplicar en todas las industrias de la rotación**: el patrón repo-como-gancho no
> tiene nada de legal.

---

## 🆕 PASE 5 (2026-11-21, 01:38 UTC) — una reparación estructural y un modo de fallo de *descubrimiento*

Este pase es el quinto sobre `legal` en 28 horas (pases a las 22:01, 22:55, 00:01, 00:53 y este).
Los cuatro anteriores dejaron `rotation.json` sin avanzar, así que la rotación volvió a caer en
`legal` cinco veces seguidas. **Eso se corrige en este pase** (ver nota al pie). Dado que los
números tenían una hora de vida, este pase **no reescribió métricas**: midió, comprobó que no
había deriva, y gastó el presupuesto en lo que no estaba hecho.

### 🔧 G-L11 — LA TABLA PRINCIPAL DE ESTE FICHERO ESTABA **PARTIDA EN DOS**, Y DOS AUDITORÍAS NO LO VIERON

Una **línea en blanco** entre la fila `awesome-legal-skills` y la fila `ai-legal-claude` dejaba las
**7 filas que añadió el pase 3** formando una **segunda tabla sin cabecera**.

| Aspecto | Qué pasó |
|---|---|
| Consecuencia para el compilador | En Markdown, una línea en blanco **termina** la tabla. Las 7 filas siguientes son otra tabla cuya **primera fila es la cabecera**. O se pierden 7 entidades, o `ai-legal-claude` **se compila como nombre de columna** — exactamente el fallo «cabecera como dato» que el brief prohíbe. |
| Por qué nadie lo vio | El pase 4 **auditó esas 7 filas una por una** (contenido, licencia, estrellas, procedencia) y las declaró correctas. Lo eran. **El defecto no estaba en ninguna fila: estaba en el carácter que las separaba de su cabecera.** |
| Por qué el control no lo detectó | Los controles de esta KB (licencia, pertinencia, censo de nombre, checksum de bytes) validan **filas**. Ninguno valida la **estructura de la tabla que las contiene**. |
| Detección | Mecánica y sin red: recorrer bloques de líneas que empiezan por barra vertical y exigir fila separadora en la 2.ª posición + número de columnas constante. Ver `compose/patterns.md` → **P22**. |
| 🆕 Hallazgo lateral | Al **escribir** este cuadro el propio P22 detectó un segundo defecto: una barra vertical dentro de *inline code* **también parte la celda** en GFM si no se escapa como `\|`. Es decir: documentar el fallo lo reprodujo. |

⇒ **Regla nueva, para toda la rotación: un pase que añade filas debe reimprimir el bloque de tabla
y verificar separadora + columnas constantes.** Verificado en este pase sobre los 8 ficheros:
**86 bloques de tabla, 2 defectos encontrados y reparados, 0 mismatches de columnas.** (El segundo defecto apareció al redactar el cuadro de arriba — ver «hallazgo lateral».)

### 🔴 G-L10 — EL ACTIVO PERMISIVO **INVISIBLE**: LOS TRES CONTROLES DE DESCUBRIMIENTO TIENEN UN FALSO NEGATIVO

`boyeesu/Kourti` (Kourti Legal) **cierra el hueco de practice management permisivo** que esta KB
declaraba abierto desde el pase 1. Es MIT (LICENSE **1.069 B**, dentro de la banda MIT), con stack
real (React + Node + PostgreSQL, `docker compose`, CI, `SECURITY.md`, **524 refs**). Y **ninguno de
los canales con los que esta KB descubre activos lo habría encontrado nunca**:

| Control de esta KB | Qué le hace a `Kourti` | Por qué falla |
|---|---|---|
| Ranking por estrellas (`sort=stars`) | lo entierra | **1★** |
| Gate de pertinencia **P15** | **lo RECHAZA** | exige ≥2 términos de industria en `description`/`topics`; el repo **no tiene ni `description` ni `topics`** |
| `legal AI` en la query de búsqueda | no lo devuelve | la búsqueda de GitHub puntúa sobre metadatos que el repo deja vacíos |
| Checksum de bytes **932-G1** | ✅ lo valida | 1.069 B ⇒ MIT genuino |
| `git ls-remote` (G-L1) | ✅ lo valida | 524 refs ⇒ código real, no esqueleto |

**El canal que sí lo encontró es el único que esta KB no usaba: un directorio de terceros**
(listado de agregador surgido en búsqueda web), **que además mentía en los detalles** — presentaba
Kourti como proyecto consolidado y «código fuente MIT en GitHub» sin mencionar que el repo tiene
1★. La afirmación de licencia resultó **cierta y verificable**; la de tracción, engañosa.

⇒ **Asimetría operativa, y es la lección transferible a toda la rotación:** las estrellas y la
`description` son **filtros de PRECISIÓN** (sirven para descartar ruido) y esta KB los estaba usando
como **filtros de COBERTURA** (para decidir qué mirar). Para **declarar un hueco abierto** no basta
no haber encontrado nada con ellos: hay que buscar por **función** fuera de GitHub y verificar
después en GitHub. Los huecos de esta KB declarados «no existe X permisivo» deben releerse como
**«no existe X permisivo *con señal social*»**, que es una afirmación mucho más débil.

> ⚠️ **Lo que NO se afirma:** que `Kourti` sea maduro o esté listo para producción. 1★ y un commit
> de 2026-11-01 significan proyecto joven y sin comunidad. Lo que se afirma es lo verificado: **MIT
> genuino, código real y alcance funcional de practice management** — es decir, **una base de
> partida legítima donde esta KB afirmaba que no había ninguna.**

---

## 🆕 PASE 6 (2026-11-21, 21:40 UTC) — el hueco más citado de esta KB estaba cerrado, y el fallo no fue de rigor sino de **independencia de canal**

**Lo que se corrigió:** la afirmación «no existe ningún servidor MCP de fuentes legales oficiales
para ninguna jurisdicción LATAM», publicada en **cuatro ficheros** (`agents/top.md`,
`agents/trending.md`, `intel/market.md` ×2) y convertida en un patrón entero (`P12 — El primer MCP
de fuentes legales oficiales de LATAM`). Es falsa. Cuatro contraejemplos permisivos, licencia leída
byte a byte, todos localizados en una sola búsqueda.

### 🔴 G-L12 — **EL NÚMERO DE CANALES NO ES LA INDEPENDENCIA DE LOS CANALES**

Esta KB escribió «verificado por los dos canales» y los dos canales eran:

1. `gh api search/repositories` — índice de GitHub.
2. lectura de ficheros en `raw.githubusercontent.com` — ficheros de GitHub.

**Son dos consultas al mismo sistema.** Para *confirmar* un activo que ya tienes (¿existe?, ¿qué
licencia?) son genuinamente independientes: miden cosas distintas. Para *descubrir* lo que no
tienes son **un solo canal**, porque comparten el mismo índice, el mismo tokenizador y el mismo
sesgo de idioma. Dos canales dependientes dan un falso negativo con la misma confianza que uno.

> **Regla:** un enunciado de **cobertura** («no existe X») exige al menos un canal **fuera** del
> sistema que indexa X. Un enunciado de **propiedad** («X es Apache-2.0») no. Esta KB aplicaba el
> protocolo de propiedad a enunciados de cobertura. Es la misma raíz que `P23`/`G-L10`, una vuelta
> más abajo: allí el filtro de precisión era *las estrellas*, aquí es *el índice entero*.

### 📏 Y la causa concreta, que es medible y no es la tracción

La explicación cómoda sería «tienen 0★, por eso no se vieron». No se sostiene: **`leis-mcp` tiene
71★**, más que 9 filas que esta KB ya recomendaba. Lo que los tres brasileños comparten no es
poca tracción, es **el idioma de su descripción**:

| Activo | Descripción indexada | ★ |
|--------|----------------------|---|
| `leis-mcp` | «Servidor MCP para buscar e citar a **legislação** brasileira» | 71 |
| `br-eli-mcp` | «MCP server for Brazilian law» (EN) + cuerpo en PT | 4 |
| `jurismcp` | «agent-driven research on Brazilian law» (EN) + portales PT | 2 |
| `mcp-dof` | «MCP server for Mexico's **Diario Oficial de la Federación**» | 0 |

Esta KB **sí** buscó en portugués y en castellano — así encontró
`Agente-Assistente-Juridico-De-Contratos` y `nexus-juris-agente-juridico`. Pero buscó los
**flujos** en portugués (*agente jurídico*, *assistente*) y las **fuentes** sólo en inglés (*legal
MCP*, *official sources*). El sustantivo que faltaba era `legislação` / `jurisprudência` /
`Diario Oficial`.

> **Regla, aplicable a las 12 industrias:** el instrumento de descubrimiento LATAM debe ser
> **trilingüe por categoría, no por región**. No basta «buscar también en español»: hay que buscar
> *cada categoría de activo* en EN + ES + **PT**, y en legal el idioma vinculante es el portugués,
> porque Brasil concentra la jurisdicción. Un cero medido en una sola lengua no es un cero.

### 🧮 Confirmaciones del checksum de licencias (932-G1) — 7 lecturas, 7 aciertos de banda

`br-eli-mcp` 11.358 B = Apache-2.0 (banda ~11.350, idéntico a `claude-for-legal`) · `jurismcp`
1.078 B, `mcp-dof` 1.082 B, `leis-mcp` 1.071 B, `legal-ai-skills` 1.069 B, `krayin/laravel-crm`
1.078 B = MIT (banda ~1.100) · `awesome-mcp-brasil` 7.048 B = CC0-1.0 · `apache/ofbiz-framework`
11.906 B = Apache-2.0 **con desvío de +548 B sobre la banda** (añade `NOTICE` dentro del fichero:
la banda tolera cola, no cabecera). Y **una refutación de fuente indexada**: ver
`verticals/solutions.md` → iDURAR.

### ⚠️ Limitación de este pase, declarada: **no se pudo comprobar renombrados**

El único oráculo de renombrado que esta KB conoce (identidad de HEAD por `git ls-remote`, pase 3)
**está muerto en esta sesión**: `git ls-remote` devuelve **0 refs para todo**, incluidos repos
vivos, y `api.github.com` responde 403. Las 83 URLs de esta KB resuelven (83/83, medido abajo),
pero `raw.githubusercontent.com` **sigue los redirects de renombrado**, así que un slug renombrado
se vería igual que uno canónico. ⇒ **Las 83 están vivas; no están comprobadas contra renombrado.**
La diferencia importa porque el pase 4 encontró 3 renombrados y la *promoción de suplente* (un
renombrado que esconde al líder real) fue el fallo más caro de la KB de gaming.

### 🔌 Y la razón por la que esto hay que escribirlo en el fichero: **el juego de canales cambia entre sesiones**

Medido hoy contra pares conocido-bueno / conocido-malo, y contrastado con lo que el pase 5
publicó como método:

| Canal | Pase 5 (publicado) | Pase 6 (medido hoy) |
|-------|--------------------|---------------------|
| `gh api search/repositories` | ✅ funciona, da ★+SPDX+`pushed_at` | 🔴 **422** salvo repos de la sesión |
| `git ls-remote` (existencia + renombrado) | ✅ oráculo prescrito | 🔴 **0 refs para todo** |
| `api.github.com/repos/...` | 🔴 403 | 🔴 403 (confirmado) |
| `curl -sI github.com/<slug>` | 🔴 403 para todo (ciego) | 🔴 403 para todo (confirmado) |
| `raw.githubusercontent.com/<slug>/HEAD/<f>` | ✅ 200/404 discrimina | ✅ **confirmado** (oráculo *positivo*) |
| WebFetch sobre `github.com/<slug>` | no usado | ✅ **★ + licencia + README** |

> **Regla:** ningún pase debe heredar el juego de canales del anterior. **Primera acción: sondear
> cada canal con un par conocido-bueno / conocido-malo** (aquí: un slug vivo y un slug inventado) y
> escribir el resultado. Sin el par, un canal ciego que devuelve «no existe» para todo se lee como
> hallazgo. Los dos oráculos que el pase 5 prescribió para *toda la rotación* no funcionan hoy.

### ✅ Censo de URLs de este pase

**83/83 slugs resuelven** (sonda `raw.githubusercontent.com/<slug>/HEAD/` sobre 6 nombres de
fichero; `EXISTS` definitivo en los 83, 0 `UNRESOLVED`). **0 bajas, 0 404.** Barrido de estructura
de tabla (`P22`/G-L11): **86 bloques, 0 defectos** — la reparación del pase 5 aguanta.

### 🗑️ Descartes de este pase, con la medición que los justifica

- `createrivabu/Iuris-Soft` (26★, sistema de gestión legal: contactos, societario, litigios,
  documentos, tareas, facturación, contratos). 🔴 **Sin licencia** — ausencia *medida*: 404 en
  `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING` y `LICENSE-MIT` sobre `HEAD`, y la
  barra lateral de GitHub no muestra entrada *License*. No adoptable.
- `j-lawyer-org/j-lawyer` y `j-lawyer-org/j-lawyer-server` — **ningún slug resuelve** (404 en
  WebFetch, sonda `raw` negativa en 5 nombres). Una fuente indexada describe *j-lawyer* como
  «practice management libre y open source»; **el slug no se pudo verificar**, así que no entra.
  Queda como pista, no como fila.
- `laugustyniak/lawful-ai`, `hartmut-ux/ai-legal-team` — **sin fichero de licencia** (medido, 6
  nombres). Además `lawful-ai` es un boletín diario de inteligencia AI *con sesgo legal*, no un
  activo legal: no pasa el gate de pertinencia `P15`.


## 🆕 PASE 7 (2026-11-22) — se cierran las dos deudas que el pase 6 dejó declaradas

El pase 6 terminó con dos limitaciones **escritas en el fichero**, que es la razón por la que este
pase pudo empezar por ellas en vez de redescubrirlas. Las dos están ahora cerradas con medición.

### ✅ Deuda 1 — el censo de renombrados, que el pase 6 **no pudo** hacer

El pase 6 declaró: *«no se pudo comprobar renombrados»*. Hoy sí, sobre **los 93 slugs** que esta KB
cita en sus ocho ficheros, con los dos canales a la vez (`search/repositories` + `git ls-remote`):

| Medición | Resultado |
|---|---|
| Slugs citados en la KB | **93** |
| Resuelven en `ls-remote` (existen) | **93 / 93** |
| Archivados | **0** |
| Inexistentes / 404 | **0** |
| Renombrados | **3** — los tres ya documentados abajo, ninguno nuevo |

Y la **signatura de renombrado** queda confirmada por tercera vez, ahora con prueba de identidad de
HEAD el mismo día:

| Slug citado (antiguo) | `search/repositories` | Slug canónico | HEAD compartido |
|---|---|---|---|
| `JSv4/OpenContracts` | **HTTP 422** | `Open-Source-Legal/OpenContracts` | `98286cabf3fc` |
| `microsoft/presidio` | **HTTP 422** | `data-privacy-stack/presidio` | `da9468112d60` |
| `lowtidebuild/contract-review-agent` | **HTTP 422** | `lowtidebuild/contract-review` | `e16315dd3b8e` |

> **La regla, ahora con las dos mitades.** `search/repositories` devuelve **422** tanto para un slug
> renombrado como para uno inexistente: **no distingue**. `ls-remote` resuelve en el renombrado y
> falla en el inexistente. **El par 422 + `ls-remote` OK = renombrado**, y la identidad de HEAD dice
> *hacia dónde*. Ningún canal solo lo resuelve; el par, sí, y cuesta dos llamadas por fila.

### ✅ Deuda 2 — las seis filas que se publicaron con `n/d` en «último commit»

El pase 6 incorporó la capa LATAM y la de skills permisivas **sin poder medir actividad**. Medido hoy:

| Fila | Estrellas | Último commit (medido) | Lectura |
|---|---|---|---|
| `matematicsolutions/br-eli-mcp` | 4 | **2026-11-21** | commit **de ayer** |
| `BEG-lag/mcp-dof` | 0 | **2026-11-17** | 5 días |
| `mazulo/leis-mcp` | 71 | **2026-11-13** | 9 días |
| `mcp-dir/jusbrasil-mcp` | 6 | 2026-08-30 | 3 meses (y es agregador, no fuente oficial) |
| `ivancaron/jurismcp` | 2 | 2026-09-30 | 2 meses |
| `rohasnagpal/legal-ai-skills` | **215** | **2026-11-12** | 10 días |

### 🔴 G-L14 — LA ACTIVIDAD Y LA SEÑAL SOCIAL SON **EJES INDEPENDIENTES**, Y ESTA KB SÓLO MEDÍA UNO

Los tres MCP de **fuentes legales oficiales de LATAM** suman **75 estrellas entre los tres** y los
tres tienen commits **de los últimos nueve días**. `br-eli-mcp`, con **4 estrellas**, se tocó ayer.

Esto no es un matiz del hallazgo G-L10 del pase 6, es el **segundo eje** del mismo plano:

- **G-L10** dijo: las estrellas son un filtro de *precisión*, y usarlas como filtro de *cobertura*
  produce falsos negativos. (Cómo **encontrar** el activo.)
- **G-L14** dice: una vez encontrado, **la señal social no predice si está vivo**. Un repo de 4★
  tocado ayer es una base más defendible que uno de 1.000★ parado hace 18 meses — y esta tabla
  tiene **las dos cosas** (`lawyer-llama`, 1.003★, 2024-08-28).

La consecuencia operativa es que **`pushed_at` es la columna que decide qué se le promete a un
cliente**, y las estrellas sólo deciden el orden de lectura. Esta KB ya ordenaba por estrellas y ya
marcaba 🪦; lo que faltaba era decir que **son medidas de cosas distintas y ninguna sustituye a la otra**.

> 📌 **Para las otras once industrias:** cualquier capa que una KB haya clasificado como «existe
> pero sin tracción» debe re-leerse midiendo `pushed_at`. Si está viva, el argumento no es
> «hay poco»; es «hay poco **conocido**», que es una ventaja de entrada, no un riesgo.

### 🧮 Censo de este pase

- **93 / 93** slugs verificados por doble canal. **0** inexistentes, **0** archivados, **3** renombrados (ya documentados).
- **6** filas que estaban en `n/d` ahora medidas. **0** `n/d` restantes en la columna de actividad.
- **101** bloques de tabla barridos con el control de estructura `P22`: **0 defectos** — la reparación del pase 5 se sostiene.
- **0** filas de cabecera o de ejemplo como dato. **0** placeholders.

---

## 🆕 PASE 8 (2026-11-22) — **EL PLANO DE INGRESOS**: siete pases catalogaron el trabajo del abogado y ninguno miró la factura

Este pase no añade una categoría: añade un **plano**. Los siete pases anteriores construyeron el
vocabulario de consulta con la forma del **producto jurídico** (contrato, cita, jurisprudencia,
cláusula, firma, expediente, benchmark). Ninguna de esas palabras encuentra la capa donde el
despacho **cobra** y donde **incurre en responsabilidad por mala praxis**.

### 📏 Primero la medición de ausencia, que es gratis y es la que justifica el pase

Censo sobre los 8 ficheros de esta KB **antes** de escribir nada (`grep -rioF`, 2026-11-22):

| Término buscado en la KB | Ocurrencias antes de este pase |
|---|---|
| `billing` / `invoice` / `timekeep` / `time-track` | 0 · 0 · 0 · 0 |
| `LEDES` / `UTBMS` / `SALI` / `LMSS` | 0 · 0 · 0 · 0 |
| `trust-account` / `IOLTA` | 0 · 0 |
| `conflicts of interest` / `conflict-check` | 0 · 0 |
| `calendaring` / `statute of limitations` / `docketing` | 0 · 0 · 1 |
| `legal spend` / `outside counsel` / `panel management` | 0 · 0 · 0 |
| `realization` / `collections` / `matter profitab` | 0 · 0 · 0 |

Cero en 17 de 19 términos. Y no es que la capa no exista: es que **nadie la había preguntado**.

> 🔑 **El pase 6 escribió esta carencia con sus propias palabras y no la convirtió en una consulta.**
> Al cerrar el hueco de *practice management* con `boyeesu/Kourti` anotó como salvedad, entre
> paréntesis, «*sin contabilidad de cuentas de terceros, sin comprobación de conflictos de
> interés*». Dos pases después esas dos salvedades siguen siendo las dos palabras que esta KB nunca
> buscó. **Una limitación anotada en un paréntesis es una consulta pendiente, no una nota al pie.**

### 🔴 Y la medición del ecosistema, que es peor de lo que la KB suponía

`gh api -X GET search/repositories`, 2026-11-22, `total_count` tal cual:

| Consulta | `total_count` | Lo mejor que hay |
|---|---|---|
| `legal timekeeping billable hours` | **0** | — |
| `UTBMS task codes` | **0** | — (y UTBMS es el **codelist que lleva toda factura legal**) |
| `conflicts of interest check law firm` | **1** | de 2021, sin licencia |
| `docketing court deadlines` | **1** | sin licencia |
| `trust accounting IOLTA` | **3** | ninguno utilizable (2 son perfiles de API de terceros) |
| `court rules deadline calculator` | **5** | AGPL-3.0, 2★ |
| `LEDES legal billing` | **6** | GPL-3.0, 2★ (Windows Forms) |

La capa donde vive el dinero del despacho y su riesgo de mala praxis —**el plazo procesal es la
primera causa de reclamación por negligencia**— tiene un orden de magnitud **menos** señal social
que la capa de revisión de contratos, que esta KB ya tenía con 14 filas.

### Activos nuevos de este pase — plano de ingresos

Licencia leída byte a byte sobre `raw.githubusercontent.com/<slug>/HEAD/LICENSE`; existencia por
recuento de refs de `git ls-remote`; metadatos por `search/repositories`. Tres canales, 2026-11-22.

| Nombre | Repo | Licencia (leída) | País / región de origen | Descripción | Stars | Último commit |
|--------|------|------------------|-------------------------|-------------|-------|---------------|
| **billcheck** | [unhingedpanda/billcheck](https://github.com/unhingedpanda/billcheck) | **MIT (1.080 B)** | Global | **El único parser/constructor/validador LEDES 1998B permisivo que existe.** TypeScript, **cero dependencias de runtime**. Conserva ceros a la izquierda, escala decimal y orden de líneas; acepta LF, CR y falta de salto final con aviso. Validador de navegador **local por construcción**: sin endpoint de subida, sin analítica, sin cookies, sin histórico; el servidor estático liga a `127.0.0.1`, rechaza métodos de escritura y Host inesperado, y su política de contenido **bloquea las conexiones del navegador**. Límite 5.000.000 B / 10.000 registros, corte a 15 s. | 0 | **2026-11-19** |
| **billing-lint** | [kirillsakhin/billing-lint](https://github.com/kirillsakhin/billing-lint) | **MIT (1.070 B)** | Global | Linter de **pre-factura** (CSV, XLSX o LEDES 1998B): narrativas vagas, *block billing*, aritmética que no cuadra, restos de plantilla (`"Draft letter to [client name]"`), entradas duplicadas y **códigos UTBMS inválidos**. Determinista, offline, ejecutable en CI. Documenta por qué el orden importa: la revisión por LLM en lote **es inconsistente** —el mismo defecto se marca en la entrada 3 y pasa callado en la 47, y dos ejecuciones del mismo extracto se contradicen. | 0 | 2026-08-31 |
| **aderant-legal-billing** | [itsoumya-d/aderant-legal-billing](https://github.com/itsoumya-d/aderant-legal-billing) | **MIT (1.071 B)** | Global | **Cierra la primera salvedad del pase 6: cuentas de terceros.** Motor de facturación y *trust compliance*: WIP por expediente, tarifarios, facturas con impuesto, **libros de cuenta de cliente que no pueden quedar en descubierto**, excepciones de compliance, cuadro de mando React y **export LEDES 1998B**. Publica las fórmulas en el README (`timeValue = round(minutes / 60 * effectiveRate)`), que es lo que lo hace auditable. | 0 | 2026-11-06 |
| **claude-court-deadline-reasoning** | [protomated/claude-court-deadline-reasoning](https://github.com/protomated/claude-court-deadline-reasoning) | MIT (1.067 B) | Global | Cálculo de plazos procesales **razonado paso a paso sobre la regla que se le da**, no sobre una tabla fija. Es el único permisivo de los cinco que devuelve la consulta de plazos. | 1 | 2026-07-21 |
| **mycase-mcp** | [oktopeak/mycase-mcp](https://github.com/oktopeak/mycase-mcp) | MIT (1.065 B) | EE. UU. · North America | **El puente al sistema de registro que el despacho ya paga.** Servidor MCP sobre MyCase (practice management comercial): expedientes, contactos, plazos y facturación quedan accesibles al agente sin migrar nada. Patrón opuesto al de sustituir la plataforma. | 6 | 2026-10-15 |

### 🪦 Y el activo que corona la medición: el **único** practice management Apache-2.0 murió en 2016

| Nombre | Repo | Licencia (leída) | País / región de origen | Descripción | Stars | Último commit |
|--------|------|------------------|-------------------------|-------------|-------|---------------|
| OpenLawOffice | [NodineLegal/OpenLawOffice](https://github.com/NodineLegal/OpenLawOffice) | Apache-2.0 (11.350 B, `LICENSE.txt`) | EE. UU. · North America | «Open source law office management — case management, billing, tasking and more». 27 forks, 5 refs. **Y 10,6 años sin un commit.** Es la prueba de que la casilla «permisivo + específico del sector + maduro» no está vacía por falta de intento: está vacía porque el intento no se sostuvo. | 38 | **2016-04-10** 🪦 |

### 🔑 La asimetría que ordena todo este plano (y es una regla de decisión, no una observación)

Medido en este pase, con licencia leída: **se puede tener dos de tres propiedades, nunca las tres.**

| Combinación | Qué hay, medido hoy |
|---|---|
| Específico del sector **+ maduro** | **Copyleft.** `deedbox-app` AGPL-3.0 (34.523 B), `4csolutions/casecentral` GPL-3.0 (25★, 29 forks), `Litigious` AGPL-3.0, módulo Odoo `legal_practice_management` AGPL-3.0, `legal-deadline-calculator` AGPL-3.0 |
| **Permisivo** + maduro | **Genérico.** `killbill` Apache-2.0 5.862★, `FOSSBilling` Apache-2.0 1.757★, `InvoicePlane` MIT 3.290★ — ninguno sabe qué es un expediente |
| **Permisivo + específico del sector** | **0★ y menos de 12 semanas de vida.** `billcheck` (3 días), `aderant-legal-billing` (16 días), `billing-lint` (12 semanas) — o Apache-2.0 muerto en 2016 |

> **Consecuencia para una propuesta:** en el plano de ingresos **no se adopta, se construye** — y se
> construye poniendo la semántica legal (expediente, tarifario, UTBMS, cuenta de terceros, plazo)
> **encima de un espinazo genérico permisivo**, no forkeando un producto legal AGPL. Es la decisión
> inversa a la que esta KB recomienda en el plano del producto jurídico, donde sí hay base permisiva
> madura. **Dos planos, dos arquitecturas, y la licencia es la que decide cuál.**

### 🗑️ Descartes de este pase, con la medición que los justifica

| Repo | Medición | Veredicto |
|---|---|---|
| [createrivabu/Iuris-Soft](https://github.com/createrivabu/Iuris-Soft) | 26★, 18 forks, time tracking + generación de gastos. **Licencia: 5/5 rutas → 404** (`LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING`) | **Descarte legítimo** por ausencia *medida* del fichero, no por `NOASSERTION`. Es el caso que la regla del pase 6 exige distinguir |
| [manojrevenkar12-web/legal-invoice-review-agents](https://github.com/manojrevenkar12-web/legal-invoice-review-agents) | 1★, LEDES 1998B parser/writer en `src/lira/ledes.py`. **Licencia: 5/5 → 404** | **No adoptable, pero se lee**: su arquitectura es la referencia de diseño de `P29`. Se cita en prosa, **no se forkea** |
| `emirmrkaljevic/awesome-legal-tech` | `search/repositories` → **422** | Indexado por el buscador web, inexistente por el canal de GitHub. Tercer índice `awesome-legaltech` clonado que aparece así (ver censo de nombre, `P18`) |
| `udayasri10435/CounselFlow…`, `Nefus1/court-clock`, `thegreatsze/singapore-procedural-deadline-calculator` | 0★, sin licencia, sin forks | Fuera por `P15` (pertinencia) **y** por ausencia de licencia. Se registran para que un pase futuro no los redescubra como hallazgo |

---

## 🆕 PASE 9 (2026-11-25) — **un hueco cerrado con UN activo encontrado por el nombre de la categoría no está cerrado**

**+9 filas** en la tabla principal (las 9 MIT o Apache-2.0, las 9 con licencia leída byte a byte,
`ls-remote` con refs > 0 y metadatos de `search/repositories`). **Recuento medido de la tabla: 49
filas antes de este pase, 58 después.**

> ⚠️ **Y una corrección de cifra publicada:** el pie de la tabla afirmaba «**43 agentes reales**».
> Contadas hoy mediante script, antes de añadir nada, eran **49**. Los pases 5–8 añadieron filas sin
> actualizar el total. **Una cifra agregada escrita a mano se desincroniza en el pase siguiente:** se
> cuenta con script o no se escribe.

### El hallazgo central, y repite el diagnóstico del pase 8 en un plano distinto

El **pase 2** declaró cerrado el hueco de e-discovery con **un solo activo** (`shmsoft/FreeEed`), y
dejó escrita la medición que lo justificaba: la consulta `ediscovery OR e-discovery` devolvía 56
repos *«y casi todos son falsos positivos»*. Esa frase es correcta **y es la prueba de que el plano
no se había consultado**: lo que se consultó fue **el nombre de la categoría**, no el vocabulario de
los artefactos que la componen.

Censo sobre los 8 ficheros de esta KB, **antes** de este pase:

| Término del plano | Menciones en la KB | `total_count` en GitHub | ¿Activo permisivo dentro? |
|---|---|---|---|
| `bates` (numeración Bates) | **0** | **150** | ✅ [Marisol](https://github.com/wikkiewikkie/Marisol) (MIT 1.075 B), [bates-master](https://github.com/bthomas530/bates-master) (**Unlicense** 1.211 B), [bates-stamping-tool](https://github.com/thaack/bates-stamping-tool) (MIT 1.063 B) |
| `load file` / Concordance DAT | **0** | 5 | ✅ `loadfile-tool` (MIT) — **el único permisivo de la categoría** |
| `legal hold` · `custodian` | **0** | 3 | ✅ `legal-hold-manager` (MIT) |
| `deposition` · `transcript` | **0** | 15 | ✅ tres MIT (ver filas nuevas) |
| `privilege log` | **0** | **902** | ❌ **ninguno — y no es recuperable; ver abajo** |
| `PAdES` (perfil de firma PDF) | **0** | 676 | ✅ `pyHanko` (MIT, **807★**) y `esig/dss` (**la de la Comisión Europea**) |
| `ESI protocol` | **0** | **0** | ⚠️ categoría genuinamente vacía (medida, no supuesta) |

Seis planos con cero menciones, cinco con activos permisivos dentro. **Y el mejor activo de todo el
pase —`pyHanko`, MIT, 807★, 121 forks, seis años de vida, commit de hace dos días— llevaba
existiendo todo este tiempo a una consulta de distancia.**

### 🔧 G-L18 — `total_count` TIENE **DOS** PATOLOGÍAS OPUESTAS, Y ESTA KB SÓLO SABÍA DIAGNOSTICAR UNA

`G-L17` (pase 8) resolvió el caso **sobre-restringido**: añadir la palabra del sector al nombre de un
estándar reduce el conjunto y entierra el mejor activo; síntoma, un `total_count` de un dígito. Este
pase encontró el caso **contrario**, y el síntoma es el opuesto:

| Forma de `total_count` | Diagnóstico | Arreglo |
|---|---|---|
| **Un dígito** y aparentemente confirma que la categoría no existe | **Sobre-restricción** — se añadió un calificador redundante | **QUITAR** el calificador: `{estándar}` + `{artefacto}`, nunca + `{sector}` (`G-L17`) |
| **Centenares/miles** y todo irrelevante | **HOMÓNIMO** — el término colisiona con un dominio mucho más ruidoso | **AÑADIR** un sustantivo **del mismo plano** (jamás el nombre del sector, que agrava la sobre-restricción) |
| Centenares, todo irrelevante **y ningún calificador lo recupera** | El término **no es alcanzable** por el índice de GitHub | Buscar **por función y fuera de GitHub** (`G-L10`) |

**Los homónimos medidos hasta hoy, en cuatro industrias-plano distintos:**

| Término legal | Colisiona con | `total_count` | ¿Recuperable? |
|---|---|---|---|
| `LEDES` (formato de factura legal) | la familia `LED` (`WLED` 19.102★, `FastLED` 7.539★) | 109.739 | ✅ con `+ invoice` → 26 (pase 8) |
| `bates numbering` | `Bates` como apellido, y umbralizado por entropía difusa | 150 | ✅ con `+ pdf`/`+ stamp` → 18 |
| **`PAdES signature`** | **«signature pad»** — widgets de firma táctil (7 de los 12 primeros) | 676 | ✅ con `+ eIDAS qualified` → 22 |
| **`privilege log`** | **escalada de privilegios** (seguridad): `win-brute-logon` 1.174★, CVEs, RBAC | **902** | ❌ **NO** — ver abajo |

### 🔴 El caso irrecuperable, y es el que más vale comercialmente

`privilege log` → **902 resultados, cero relevantes**: el log de privilegio del litigio compite con
la escalada de privilegios de seguridad informática, y **pierde**. Probado el arreglo de `G-L18`:
`privileged document review redaction` → **`total_count` = 0**. No hay calificador que lo rescate.

> 🔑 **Y aquí está el valor:** el pronóstico de sector para 2026 nombra **expresamente el privilege
> log** entre los flujos de e-discovery que más se automatizan este año (junto a la revisión de
> primera pasada y las investigaciones internas). **Es decir: el flujo que el mercado declara en
> expansión es exactamente el que no tiene un solo activo abierto localizable.** Esto no es un hueco
> de esta KB: es un hueco **del ecosistema**, medido por dos vías (índice ciego + ausencia de
> activos), y se publica **abierto**. No se cierra inventando una fila.

### 🔧 G-L19 — **EL IDIOMA DE UNA CONSULTA NO ES UNA REGIÓN**

Esta KB ya sabía que `es/` en un repo es España (EMEA) y no LATAM. Hoy se midió el mismo error **un
nivel más arriba, en la consulta**: buscar el marco mexicano de IA judicial en español devolvió
**mayoritariamente España** — la Instrucción 2/2026 del CGPJ, el BOE, Iberley, Jueces para la
Democracia. De los 10 resultados, **8 eran España**; el único resultado mexicano relevante
(Estado de México, `PTSJ/028/2026`) llegó **en noveno lugar**.

Causa: «Poder Judicial», «acuerdo», «expediente» y «amparo» son vocabulario **compartido** por todas
las jurisdicciones hispanohablantes, y el índice pondera por volumen de publicación, donde España
domina. **Fijar la jurisdicción exige el nombre de una institución que sólo exista en ella** — `DOF`,
`PJF`, `Gaceta del Gobierno`, `CJF` para México; `STF`, `CNJ`, `DJe` para Brasil — no el idioma.

> **Regla para las doce industrias:** una consulta en español, portugués o inglés **no** es una
> consulta de LATAM, EMEA ni APAC. El idioma es un filtro de *publicación*; la región se fija con un
> **nombre propio institucional**. Un pase que concluya «no hay nada en LATAM» tras buscar en español
> ha medido el volumen editorial de España.

### 🔌 Estado de los canales en esta sesión (cambia entre sesiones — por eso se escribe)

| Canal | Estado | Nota |
|---|---|---|
| `gh api search/repositories` | ✅ | estrellas, SPDX, `pushed_at`, `created_at`, `forks`, `archived` en una llamada |
| `git ls-remote` | ✅ | existencia real; 0 refs = no existe |
| `curl` a `raw.githubusercontent.com` | ✅ | licencia byte a byte (200/404 discrimina) |
| `curl -sI` a `github.com` | 🔴 **403 para todo** | el control prescrito por el brief **sigue siendo ciego aquí**: no distingue vivo de inexistente |
| **`WebFetch` a fuentes legales primarias** | 🔴 **ENOTFOUND** | **nuevo este pase.** `boe.es` y `edomex.quadratin.com.mx` no resuelven: fuera de los dominios permitidos de la sesión |

> ⚠️ **Consecuencia que afecta a todas las filas regulatorias de este pase:** las normas citadas
> (CGPJ Instrucción 2/2026, Edomex `PTSJ/028/2026`, *Schulte v. LinkedIn*) **están verificadas por UN
> solo canal — el índice de búsqueda — y NO contra el texto oficial.** Se publican marcadas. Por la
> regla de dos canales de esta KB, eso es **señal, no hecho establecido**.

---

## 🆕 PASE 10 (2026-11-25) — la capa de **fuentes legislativas oficiales**: la plaza por jurisdicción, completada en cuatro regiones

Los pases 6 y 7 establecieron que «el MCP de fuentes oficiales es el patrón dominante del sector»
(`intel/trends.md` §13) y lo midieron sobre **jurisprudencia** (tribunales, sentencias). Este pase
aplica el mismo patrón a la **otra** fuente oficial —**la legislación**— y encuentra que la plaza
está ocupada en las cuatro regiones, con permisivo en todas menos una.

| Agente | Licencia (leída) | Región | Fuente oficial que resuelve | ★ | Último commit |
|---|---|---|---|---|---|
| [alvarosdev/lex-chile-mcp](https://github.com/alvarosdev/lex-chile-mcp) | **MIT (1.069 B)** | **LATAM** · Chile | Ley chilena por MCP | 2 | 2026-11-14 |
| [ejaircastillo/InfoLeg-MCP](https://github.com/ejaircastillo/InfoLeg-MCP) | **MIT (1.036 B)** | **LATAM** · Argentina | **InfoLeg** (normativa nacional) | 0 | 2026-05-20 |
| [CodeandoGuadalajara/dof-rag](https://github.com/CodeandoGuadalajara/dof-rag) | **MIT (1.077 B)** | **LATAM** · México | **Diario Oficial de la Federación** (RAG) | 25 | 2026-11-02 |
| [diegoparras/notarum](https://github.com/diegoparras/notarum) | **MIT (1.069 B)** | **LATAM** · Argentina | **Boletín Oficial** | 2 | 2026-11-20 |
| [LibreCodeCoop/dou-collector](https://github.com/LibreCodeCoop/dou-collector) | **MIT (1.071 B)** | **LATAM** · Brasil | **Diário Oficial da União**. ⚠️ dormante 2024-11-13 | 11 | 2024-11-13 |
| [cyanheads/eur-lex-mcp-server](https://github.com/cyanheads/eur-lex-mcp-server) | Apache-2.0 (11.317 B) | **EMEA** · UE | EUR-Lex + TJUE + grafo **CELLAR**, sin API key | 13 | 2026-11-18 |
| [elconcept/mcp-eu-sparql](https://github.com/elconcept/mcp-eu-sparql) | **MIT (1.082 B)** | **EMEA** · UE | SPARQL de la Oficina de Publicaciones; **CELEX + ECLI en cada cita** | n/d | n/d |
| [cchew/lex-au](https://github.com/cchew/lex-au) | **MIT (1.067 B)** | **APAC** · Australia | Legislación federal australiana | 6 | 2026-11-22 |
| [openstates/openstates-scrapers](https://github.com/openstates/openstates-scrapers) | GPL-3.0 (35.147 B) | **North America** · EE. UU. | **50 estados + DC + PR**, normalizados. 522 forks | 929 | 2026-11-25 |

### 🟢 El hueco LATAM de esta categoría estaba **cerrado**, y la razón corrige la conclusión del pase 8

El pase 8 cerró su investigación del plano de ingresos con un hueco LATAM declarado explícitamente:
*«CERO activos con anclaje en LATAM»* tras consultar `LEDES`, `UTBMS`, `trust accounting IOLTA` y
`legal timekeeping`. Y razonó bien **por qué**: LEDES y UTBMS son estándares **de origen
estadounidense**, y en LATAM el equivalente funcional es la factura electrónica fiscal de cada país.

Ese razonamiento es correcto **y se queda corto**, porque implica algo que el pase 8 no sacó: si el
hueco venía del origen del estándar, entonces **cualquier categoría anclada en un estándar
estadounidense va a medir hueco en LATAM, y la medición no dice nada sobre la región.** Repetida la
consulta con la fuente oficial **de cada país** —`diario oficial`, `InfoLeg`, `LeyChile`,
`DOF`, `LexML`, `boletín oficial`— aparecen **ocho activos LATAM, siete de ellos MIT**.

| Consulta | `total_count` | Activos útiles |
|---|---|---|
| `legislacion como codigo` | **0** | — |
| `rules as code latam` | **0** | — |
| `openfisca brasil` / `mexico` / `colombia` / `chile` | **0** cada una | — |
| `diario oficial federacion dof` | 21 | `dof-rag` (**MIT, 25★**), `dof-chat` (AGPL) |
| `leychile` | 13 | `lex-chile-mcp` (**MIT**), `leychile` (**MIT**, ⚠️ archivado) |
| `infoleg argentina` | 8 | `InfoLeg-MCP` (**MIT**), `argentina-data-mcp` (NOASSERTION) |
| `lexml` | 79 | `lexml-parser-projeto-lei` (GPL-2.0, **oficial del Senado**), `lexml-eta`, `editor-articulacao` (LGPL) |
| `diario oficial scraper` | 19 | `dou-collector` (**MIT**) |
| `boletin oficial argentina api` | 1 | `notarum` (**MIT**) |

> **`G-L22` — UN HUECO REGIONAL MEDIDO SOBRE UN ESTÁNDAR EXTRANJERO NO ES UN HUECO REGIONAL: ES LA
> HUELLA DEL ESTÁNDAR.** Las cuatro consultas con vocabulario importado (`rules as code`,
> `openfisca {país}`, `legislacion como codigo`) devuelven **0**. Las seis con el nombre propio de
> la fuente oficial devuelven **141 repos y 8 activos**. El `0` no medía LATAM: medía si alguien en
> LATAM había adoptado una palabra de fuera. **Antes de declarar un hueco regional, hay que
> consultar con el nombre que la cosa tiene EN esa región** — el `urn:lex` brasileño, el `DOF`
> mexicano, el `Boletín Oficial` argentino. Aplicable a las doce industrias y **explica
> retroactivamente** los huecos LATAM de los pases 6 y 8.

### ⚠️ Y la fila que **no** se escribe como permisiva, aunque el buscador lo afirme

[`hendrillara/akoma`](https://github.com/hendrillara/akoma) —legislación federal brasileña por
artículo, para agentes, creada hace 5 semanas— fue descrita por el índice de búsqueda con la frase
**«its code is MIT-licensed»**. Su `LICENSE` son **6.732 B** titulados **«Akoma Noncommercial and
Commercial Licence 1.0»**: licencia bespoke con frontera comercial, `NOASSERTION` en la API. **No
entra en la tabla de agentes** y se registra aquí como descarte documentado. Detalle en
`agents/trending.md` (`G-L20`).

## 🆕 PASE 11 (2026-11-25) — el plano **acústico**: de dónde sale la transcripción que los pases 9 y 10 daban por hecha

Censo de entrada sobre los ocho ficheros, **antes** de consultar nada: `whisper` **0**, `diariz` **0**,
`speech` **0**, `estenotip` **0**, `taquigra` **0**, `audiencia` **0**, `oralidad` **0**,
`ASR` **2**, `audio` **3**, `voz` **1**. Diez sondas, cero señal en 8.235 líneas.

El pase 9 inventarió el **plano de la prueba** y cerró la capa de deposición con `DepoIndex`,
`deposition-contradiction-analysis` y `depo-summarizer`. Los tres **parten de una transcripción que
ya existe**. Ninguno dice de dónde sale, y en 2026 es exactamente donde está el cuello de botella:
el récord verbatim cuesta días y lo produce una profesión que se está vaciando. **Esta KB sabía
explotar la transcripción y no sabía producirla.**

> **Frontera limpia con el pase 9.** Pase 9 = *qué se hace con el transcript* (texto dentro, análisis
> fuera). Pase 11 = *audio dentro, transcript fuera*. No hay solape: cero de los 28 activos de este
> pase aparecía en la KB.

### Agentes y servidores de transcripción (licencia leída + `ls-remote` + `search/repositories`, 2026-11-25)

| Agente | Licencia (leída) | Región | Por qué entra | ★ | Último commit |
|---|---|---|---|---|---|
| [QuentinFuxa/WhisperLiveKit](https://github.com/QuentinFuxa/WhisperLiveKit) | Apache-2.0 | Global | Transcripción **en vivo** con diarización, servidor local. El perfil exacto de una sala de audiencias: streaming, no lote | **11.294** | 2026-11-23 |
| [MahmoudAshraf97/whisper-diarization](https://github.com/MahmoudAshraf97/whisper-diarization) | BSD-2-Clause | Global | Pipeline ASR + **quién habla** ya ensamblado. En una audiencia multiparte la atribución de locutor *es* el dato jurídico | **5.676** | 2026-08-15 |
| [collabora/WhisperLive](https://github.com/collabora/WhisperLive) | MIT | Global | Cliente/servidor de transcripción casi en tiempo real. Respaldo institucional (Collabora), no proyecto de una persona | **4.362** | 2026-11-24 |
| [speaches-ai/speaches](https://github.com/speaches-ai/speaches) | MIT | Global | Servidor con **API compatible OpenAI** para STT y TTS. Sustituye el endpoint de un proveedor sin tocar el cliente: la pieza de migración a on-premise | **3.782** | 2026-11-25 |
| [ahmetoner/whisper-asr-webservice](https://github.com/ahmetoner/whisper-asr-webservice) | MIT | Global | Servicio ASR en Docker, el despliegue más repetido de la categoría (582 forks) | **3.371** | 2026-11-24 |
| [innovatorved/whisper.api](https://github.com/innovatorved/whisper.api) | MIT | Global | API autoalojada sobre `whisper.cpp` con endpoints compatibles OpenAI **y Deepgram**: reemplazo directo de dos nubes distintas | 914 | 2026-11-20 |
| [BUTSpeechFIT/DiariZen](https://github.com/BUTSpeechFIT/DiariZen) | **MIT (leída)** | **EMEA** (Chequia, BUT Brno) | Diarización de grupo académico europeo. Alternativa a `pyannote` **sin** la dependencia de pesos con registro previo | 573 | 2026-08-04 |
| [hwdsl2/scribecrate](https://github.com/hwdsl2/scribecrate) | **NOASSERTION** → MIT íntegro (**2.304 B**) | Global | Servidor `faster-whisper` **offline por diseño**: modelos en caché, diarización, salida JSON/SRT/VTT, Docker CPU o CUDA. ⚠️ **RENOMBRADO desde `hwdsl2/docker-whisper`** | 125 | 2026-11-18 |
| [gitchrisqueen/hearing-copilot](https://github.com/gitchrisqueen/hearing-copilot) | **MIT (1.074 B)** | Global | **El único activo jurídico-específico permisivo de todo el plano.** Copiloto de sala para litigante **autorrepresentado**: transcripción en vivo, etiquetado de locutor y cotejo contra un catálogo de réplicas preparadas. ⚠️ 0★, creado hace días. Núcleo compartido en [copilot-core](https://github.com/gitchrisqueen/copilot-core) (MIT, 0★) | **0** | 2026-11-23 |

**Nueve filas, nueve reales.** No se rellena: lo que la categoría jurídica tiene medido es una fila
con 0★, y esa escasez *es* el hallazgo (ver `T30` más abajo).

### ⛔ La trampa de licencia del pase, y es **geográfica**

[moonshine-ai/moonshine](https://github.com/moonshine-ai/moonshine) — 11.598★, `NOASSERTION`,
renombrado desde `usefulsensors/moonshine`. Su `LICENSE` son **14.180 B** y empieza por un
reparto, no por una concesión. Leído byte a byte:

- El **código** es MIT. Los modelos **streaming** y **todos los de inglés** son MIT.
- Los modelos heredados **no-streaming** de los demás idiomas quedan bajo *Moonshine Community
  License*, y la lista es exhaustiva: **árabe, japonés, coreano, mandarín, español (Base),
  ucraniano y vietnamita**.
- Esa licencia **limita el uso comercial por facturación**: permite uso comercial sólo por debajo de
  **USD 1.000.000 de ingresos anuales** (o equivalente en moneda local).

> 🔴 **Para Globant esto es un «no» directo, y cae sólo fuera de Norteamérica.** El único idioma que
> un despliegue judicial en LATAM o España necesita —**español**— está en la lista restringida; el
> inglés no. **En este plano la exclusión de licencia no es por componente: es por idioma, y por
> tanto por región.** Un equipo que leyera «11.598★, MIT» y lo metiera en una propuesta en México,
> Chile o Madrid estaría enviando un modelo no licenciable para uso comercial.
>
> **Mitigación medida, sin coste:** `openai/whisper` (MIT), `SYSTRAN/faster-whisper` (MIT),
> `k2-fsa/sherpa-onnx` (Apache-2.0) y `alphacep/vosk-api` (Apache-2.0) cubren español sin
> restricción de ingresos. Ver `repos/foundations.md`.

### `T30` — la matriz `T28` se confirma por **cuarta** industria, y aquí con el contraste más brutal

`T28` (pase 8): *se pueden tener dos de tres propiedades, nunca las tres.* Medido hoy en este plano:

- **permisivo + maduro ⇒ GENÉRICO**: `whisper` 113.472★, `whisper.cpp` 55.504★,
  `faster-whisper` 27.003★, `whisperX` 25.661★, `pyannote-audio` 10.841★. **Ninguno sabe qué es una
  audiencia, una deposición ni una línea de transcript.**
- **permisivo + específico ⇒ 0★ y días de vida**: `hearing-copilot` (MIT, 0★, commit de hace 2
  días), `DepoIndex` (MIT, 0★, del pase 9).
- Y el censo del ecosistema, con `total_count` de `search/repositories`:
  `court transcript page line` = **0** · `hearing transcription judicial` = **0** ·
  `legal transcript diarization` = **1** (sin licencia) · `deposition transcript parser` = **1** ·
  `courtroom transcription` = **7** (de los 7, **uno** permisivo y vivo).

La capa con **113.000 estrellas de infraestructura** tiene **cero estrellas de producto jurídico**.
