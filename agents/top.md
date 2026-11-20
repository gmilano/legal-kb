---
industry: legal
region: Global
updated: 2026-11-20
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

### 🆕 Tercera divergencia de canal, medida hoy — y protege contra un borrado futuro

El pase anterior documentó que los canales discrepan en una dirección (`NOASSERTION` en la API con
LICENSE legible, y renombrados invisibles en `raw`). **Hoy apareció la tercera, y es la peligrosa:**

| Repo | API de búsqueda | `raw` | Lectura correcta |
|------|-----------------|-------|------------------|
| `lowtidebuild/contract-review-agent` | **ausente** (`repo:` no devuelve nada) | **200** en `README.md` y `LICENSE` | **El repo existe.** No está en el índice de búsqueda. |

> 🔧 **Regla que esta KB adopta:** **ausente en la API de búsqueda ≠ inexistente.** Antes de
> retirar una fila por «no encontrada», hay que **probar `raw`**. Un repo puede existir y no estar
> indexado (recién creado, poca señal, o excluido del índice).
>
> La inversa también sigue vigente: **existir en `raw` no acredita procedencia.** `raw` resuelve
> por redirección, así que un slug renombrado devuelve 200 apuntando a otro sitio. Por eso esta
> fila conserva su ⚠️ de procedencia: *está viva, pero no verificada en origen.*

**Cómo se verificó todo lo nuevo de este pase:** los **16 repos añadidos** pasaron **los dos
canales** (API de búsqueda para existencia/estrellas/`pushed_at`/`archived`/rama, y lectura byte a
byte del LICENSE por `raw`). **Barrido completo del fichero: 65 URL únicas de GitHub comprobadas,
62 resuelven en la API, 1 resuelve sólo por `raw` (arriba) y 2 son slugs obsoletos citados a
propósito** en la tabla de renombrados de más abajo. **0 enlaces roto sin declarar.**

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
| contract-review-agent | [lowtidebuild/contract-review-agent](https://github.com/lowtidebuild/contract-review-agent) | Apache-2.0 (11.284 B) | Global | Revisión de contratos local-first. Produce **DOCX con tracked changes** (redline interno, limpio externo y reporte), comentarios al margen y recomendaciones de negociación. Progresó de v1-beta a **v1.0.0**. ⚠️ Procedencia a confirmar — ver aviso abajo. | — | activo (raw) |
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

**33 agentes reales, los 33 verificados hoy por API de búsqueda + lectura byte a byte de LICENSE. 0 filas de ejemplo, 0 placeholders.** (18 heredadas y revalidadas, 15 nuevas en este pase.)


## ⚠️ Dos renombrados detectados hoy (y cómo se detectan)

Esta KB llevaba meses apuntando a dos slugs que ya no son canónicos. **Ninguno es un 404**, y por
eso el método anterior (sólo `raw`) no podía verlos:

| Slug publicado (obsoleto) | Slug canónico hoy | Prueba |
|---------------------------|-------------------|--------|
| `microsoft/presidio` | **`data-privacy-stack/presidio`** | `LICENSE` idéntico en ambos: **1.084 B, mismo MD5 `edb1b1745226`**. 11.989★. |
| `JSv4/OpenContracts` | **`Open-Source-Legal/OpenContracts`** | 1.550★ coincide con el «1.5k★» que esta KB atribuía al slug viejo. |

**Firma del renombrado, idéntica en los dos casos:** `repo:<slug-viejo>` devuelve **HTTP 422**
(«the listed users and repositories cannot be searched») **mientras `raw` sobre el slug viejo
devuelve 200**, porque GitHub sirve el contenido por redirección. Mirando sólo `raw`, el
renombrado es invisible; mirando sólo la API, el repo parece borrado. **Hacen falta los dos.**

Tasa medida: **2 renombrados + 1 muerto en 31 URL = ~1 incidencia por 10 repos.** La KB de
gaming midió ~1 por 21 y la de enterprise ~1 por 10. **Es una tasa, no una anomalía:** una KB que
no revalida slugs acumula punteros muertos a ese ritmo.

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

## ⚠️ Procedencia a confirmar — contract-review-agent
`lowtidebuild/contract-review-agent` **resuelve en `raw`** (README 17.409 B, `LICENSE` 11.284 B de
texto Apache-2.0, `package.json` declara `"license": "Apache-2.0"`, versión 1.0.0) **pero
`repo:` devuelve 422**, la misma firma que los dos renombrados. Su README no contiene ningún
enlace a `github.com`, así que **no se pudo determinar el slug canónico actual**. Se publica con
licencia verificada y con la advertencia: **el owner puede haber cambiado.** No se declara
muerto —`raw` lo sirve— ni vivo-en-este-slug, porque ninguna de las dos cosas está probada.

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
- **No existe ningún servidor MCP de fuentes legales oficiales para ninguna jurisdicción LATAM.**
  Esto sí se verificó por los dos canales y **sigue vacío**. Hoy hay MCP de fuentes oficiales para
  EE. UU., Alemania, Suiza, Italia, Taiwán (×2) y Corea. Para Brasil, México, Argentina, Chile,
  Colombia y Perú: **nada**. Es el hueco real, y es de *fuentes*, no de *flujos*.
- Sigue sin aparecer ningún agente legal open source **de origen** LATAM con señal. Re-verificado:
  `turborocket-dev/Agente-Assistente-Juridico-De-Contratos` (0★), `jhondados/chatbot-juridico`
  (0★), `manfredjr/legal-br` (MIT, 0★), `desdobroprod-eng/nexus-juris-agente-juridico` (3★).

⚠️ **La trampa de etiquetado se mantiene vigente:** `claude-para-abogados` está en castellano pero
es **derecho de España** → EMEA. Y en `legal-skills-open`, `es/` (9 plugins) es España, no LATAM;
el código LATAM es `br/`, `mx/`, `ar/`, `co/`, `pe/`, `do/`.

⇒ **Oportunidad reformulada, y es mejor que la anterior.** Ya no es «construir desde cero»: es
**(a)** contribuir profundidad a `br/`, `mx/`, `ar/` sobre una estructura Apache-2.0 que ya existe
y acepta contribuciones por jurisdicción, y **(b)** construir **el primer MCP de fuentes legales
oficiales de LATAM** — DJe/Jusbrasil para Brasil, DOF/SCJN para México — copiando la arquitectura
ya probada de `opencaselaw` (26 cantones, 3 idiomas) y `korean-law-mcp` (42 APIs oficiales). Ver
`compose/patterns.md` → P7 y P12.

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
*Verificado 2026-11-20 (pase 2 del día) por doble canal (API de búsqueda + lectura byte a byte de
LICENSE). **33 filas reales, 0 placeholders** (18 heredadas y revalidadas + 15 nuevas). En este
pase: 2 modos de fallo de licencia nuevos documentados (CC-BY-NC-ND y relicenciamiento ELv2 con
frontera temporal), 1 hueco declarado parcialmente refutado con la causa del error a la vista, y el
clúster de activos por jurisdicción pasa de 6 a 13. Pases anteriores: 2 renombrados corregidos,
1 repo muerto retirado, 4 dormancias declaradas.*
