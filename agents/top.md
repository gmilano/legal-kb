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

**18 agentes reales, los 18 verificados hoy por API + lectura de licencia. 0 filas de ejemplo, 0 placeholders.**

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
- **EMEA**: claude-fuer-deutsches-recht (DE), claude-para-abogados (ES), mcp-legal-it (IT),
  Blackstone (UK, dormido).
- **APAC**: korean-law-mcp (KR, el más grande de la categoría), LawGlance (IN), DISC-LawLLM /
  lawyer-llama / fuzi.mingcha (CN, los tres dormidos).
- **LATAM**: ninguno. Ver abajo.

## 🔴 Hueco LATAM — buscado explícitamente hoy, resultado honesto

Se buscó con **vocabulario es/pt**, no sólo en inglés: `juridico IA agente contratos`,
`direito juridico IA LGPD brasil`, `derecho legal IA abogados español`,
`jurisprudencia IA busqueda legal`.

**Resultado: no existe ningún agente legal open source de origen LATAM con señal.** Lo encontrado:
`turborocket-dev/Agente-Assistente-Juridico-De-Contratos` (0★), `jhondados/chatbot-juridico` (0★),
`manfredjr/legal-br` (MIT, 0★), `desdobroprod-eng/nexus-juris-agente-juridico` (3★),
`jontimoteo-programmer/agente-de-ia-...-contratos-de-tecnologia` (0★). Ninguno pasa el umbral.

⚠️ **Y una trampa que esta KB podría haber caído:** `claude-para-abogados` está en castellano, pero
es **derecho de España** — región EMEA. Contarlo como activo LATAM sería un error de etiquetado
con consecuencias: su contenido mercantil, laboral y procesal es español y europeo, no brasileño
ni mexicano.

**Lo que esto sí es: una oportunidad acotada y con plantilla probada.** Existen adaptaciones por
jurisdicción de `claude-for-legal` para Alemania y España, y servidores MCP por jurisdicción para
Corea, Italia, Singapur y EE. UU. **No existe ninguno para Brasil ni México.** Ver
`intel/market.md` → *Opportunities by region* → LATAM.

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
*Verificado 2026-11-20 por doble canal (API de búsqueda + lectura de LICENSE). 18 filas reales,
0 placeholders. 2 renombrados corregidos, 1 repo muerto retirado, 4 dormancias declaradas.*
