---
industry: legal
region: Global
updated: 2026-11-20
---

# 📈 Agentes trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. No se reescribe: la serie temporal *es* el contenido.

## 🆕 2026-11-20 (pase 2) — el clúster por jurisdicción se vuelve medible, y dos licencias mienten

**Qué cambió respecto al pase de hace unas horas:** aquel pase cerró con la frase *«el patrón de
producto del año es la plantilla por jurisdicción»* y contaba 6 activos de ese tipo. Hoy, con el
mismo canal de búsqueda pero consultas por **`legal mcp server`** en vez de por nombre de agente,
el recuento es **13**. La tendencia no era una lectura: es un clúster, y tiene una forma repetida.

### Agentes con señal real esta semana

| Agente | Licencia (leída) | Región | Señal | Stars |
|--------|------------------|--------|-------|-------|
| [awesome-legal-skills](https://github.com/lawve-ai/awesome-legal-skills) | 🔴 CC-BY-NC-ND 4.0 (19.122 B) | Global | El índice de skills legales más grande que existe — **y no se puede usar**. Ver correcciones. | **966** |
| [devnors-data-mcp](https://github.com/DevnorsAI/devnors-data-mcp) | MIT (1.064 B) | APAC (CN) | Primer acceso MCP a sentencias, normativa y registro mercantil chinos en esta KB. Creado jul-2026. | 796 |
| [tw-legal-rag](https://github.com/aa0101181514/tw-legal-rag) | ⚠️ ELv2 (4.044 B) | APAC (TW) | 22,8 M de sentencias taiwanesas **con verificación de cita incorporada**. Licencia cambiada en v2. | 350 |
| [mcp-taiwan-legal-db](https://github.com/lawchat-oss/mcp-taiwan-legal-db) | MIT (1.092 B) | APAC (TW) | La alternativa limpia a la anterior, misma jurisdicción. | 234 |
| [legal-research-skill](https://github.com/Golden2002/legal-research-skill) | MIT (1.066 B) | APAC (CN) | Agent Skill de búsqueda normativa para Cursor / Claude Code / OpenCode. | 168 |
| [contract-review](https://github.com/xiaodingfeng/contract-review) | MIT (1.069 B) | APAC (CN) | Revisión de contratos en chino con **OnlyOffice** y puntos de revisión configurables. | 168 |
| [legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | Apache-2.0 (11.314 B) | Global · 54 jurisd. | **18.000+ skills, 410+ plugins — y cobertura LATAM real.** Refuta un hueco declarado. | 141 |
| [due-diligence-agents](https://github.com/zoharbabin/due-diligence-agents) | Apache-2.0 (10.762 B) | Global | 13 agentes sobre el data room en 9 dominios, **cruzando legal con financiero y citando**. | 139 |
| [ayunis-legal-mcp](https://github.com/ayunis-core/ayunis-legal-mcp) | MIT (1.070 B) | EMEA (DE) | Códigos legales alemanes por MCP. Complemento de fuentes a los flujos de `claude-fuer-deutsches-recht`. | 91 |
| [doc-haus](https://github.com/sure-scale/doc-haus) | **GPL-3.0** ⚠️ (35.149 B) | Global | Redline local con tracked changes en Word. Rama **`dochaus`**, no `main`. | 83 |
| [ms-word-addin](https://github.com/Vaquill-AI/ms-word-addin) | Apache-2.0 (11.340 B) | Global | Revisión de contratos **dentro de Word** con licencia permisiva. | 81 |
| [opencaselaw](https://github.com/jonashertner/opencaselaw) | **MIT + CC0 datos** (1.069 B) | EMEA (CH) | **El activo del pase.** 1M+ sentencias suizas, grafo de citas de 10M aristas, 42 tools MCP, commit de hoy. | 80 |
| [italia-mcp-servers](https://github.com/bsab/italia-mcp-servers) | MIT (1.069 B) | EMEA (IT) | Catálogo de MCP italianos (datos públicos, legal-tech, PA). | 78 |
| [bettercallclaude](https://github.com/fedec65/bettercallclaude) | **AGPL-3.0** ⚠️ | EMEA (CH) | Plugin de práctica jurídica suiza. Par natural de `opencaselaw`. | 47 |
| [us-legal-mcp](https://github.com/JamesANZ/us-legal-mcp) | MIT (1.071 B) | NA (US) | Legislación federal estadounidense por MCP. | 39 |

**15 filas, las 15 verificadas hoy por API de búsqueda + lectura byte a byte del LICENSE.
0 placeholders.**

### Correcciones registradas este pase

1. 🔴 **`awesome-legal-skills` no es permisivo: es CC-BY-NC-ND 4.0.** La API dice `NOASSERTION`;
   el fichero dice NonCommercial **y** NoDerivatives. Un engagement de cliente es uso comercial y
   adaptar una skill a su jurisdicción es una obra derivada: **las dos cosas que haría Globant
   están prohibidas.** Con 966★ y nombre `awesome-*`, es la trampa de licencia más probable de
   toda esta KB.
2. ⚠️ **`tw-legal-rag` se relicenció a mitad de su historia.** LICENSE de 4.044 B que **empieza
   mencionando MIT** (así que un `grep` lo aprueba) y resulta ser **Elastic License 2.0**, con
   nota explícita: *MIT se mantiene sólo hasta v1.2.2*. **Modo de fallo nuevo para esta KB: la
   licencia depende del tag, no del repo.** Regla adoptada: verificar la licencia **en la versión
   que se va a fijar**.
3. 🟡 **Hueco LATAM parcialmente refutado — error propio, de hace unas horas.** `agents/top.md`
   afirmaba en negrita *«No existe ninguno para Brasil ni México»*. `legal-skills-open` tiene
   **Brasil 15 plugins** (9.ª jurisdicción del repo, por delante de Francia, UK, Italia y España),
   Argentina 2, México 2, Colombia 1, Perú 1, Rep. Dominicana 1. **Causa del error: se buscaron
   repos de *origen* LATAM y no cobertura LATAM *dentro de* repos globales.** Corregido en
   `agents/top.md` y en `intel/market.md`.
4. **El clúster por jurisdicción pasa de 6 a 13 activos.** Hoy hay MCP de fuentes oficiales para
   EE. UU., Alemania, Suiza, Italia, Taiwán (×2) y Corea; más flujos para España, India y China.

### Hueco declarado — el que queda, y es más preciso que el anterior

🔴 **No existe ningún servidor MCP de fuentes legales oficiales para ninguna jurisdicción LATAM.**
Verificado por los dos canales. El hueco **cambió de forma**: no es «LATAM no tiene nada» (falso,
hay flujos Apache-2.0), es **«LATAM no tiene fuentes»**. Es un hueco mejor, porque la arquitectura
a copiar ya está probada dos veces: `opencaselaw` (26 cantones, 3 idiomas, CC0) y `korean-law-mcp`
(42 APIs oficiales).

🗄️ *Nota de histórico: la sección de abajo es el primer pase del 2026-11-20, conservado íntegro.*

## 2026-11-20 (pase 1) — el líder de la categoría estaba ausente, y dos slugs eran obsoletos

**Qué cambió respecto al pase anterior:** el pase del 2026-11-04 verificó licencias byte a byte
pero creyó que **la API de GitHub estaba bloqueada**. No lo está. Reprobada hoy, aportó lo que la
lectura de `raw` no puede ver: `archived`, `pushed_at` y la **existencia canónica del slug**.
Resultado: **1 agente líder que faltaba, 2 renombrados, 1 repo muerto y 4 dormancias**, todo
invisible para el método anterior.

### Agentes con señal real esta semana

| Nombre | Repo | Licencia (leída) | Por qué importa | Stars | Último commit |
|--------|------|------------------|-----------------|-------|---------------|
| **Claude for Legal** | [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Apache-2.0 | 🥇 **EL HALLAZGO DEL PASE.** Suite de plugins para flujos legales (in-house, privacidad, corporativo, laboral, litigio, regulatorio, gobernanza AI, IP, clínicas). Permisiva, mantenida y con dos vías de despliegue: plugin de Claude Code/Cowork **o** Managed Agents API. **30× lavern, y esta KB no la tenía en ningún fichero.** | **10.054** | 2026-11-19 |
| mike | [open-legal-products/mike](https://github.com/open-legal-products/mike) | ⚠️ AGPL-3.0 | De «—» a **4.504★**: la plataforma legal AI open source más grande que existe. Primera publicación 29-abr-2026 ⇒ **todo ese crecimiento es de siete meses.** Licencia bloqueante para SaaS cerrado: sirve de benchmark competitivo, no de base. | **4.504** | 2026-11-19 |
| Korean Law MCP | [chrisryugj/korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) | MIT (1.062 B) | 🇰🇷 **El mayor MCP legal que existe** y el primer activo APAC de peso de esta KB. Las **42 APIs oficiales del 법제처** en 10 herramientas, y **contraste de las citas del LLM contra el texto original**. En npm y en el MCP Registry. | **2.904** | 2026-11-20 |
| Claude für deutsches Recht | [Klotzkette/claude-fuer-deutsches-recht](https://github.com/Klotzkette/claude-fuer-deutsches-recht) | Apache-2.0 | 🇩🇪 **Primer activo EMEA de peso de esta KB**, que declaraba no haber encontrado ninguno. Plugins, skills y prompts para la práctica alemana, con **Testakten** (expedientes ficticios) para ensayar sin datos reales. README de 115.817 B. | **1.866** | 2026-11-20 |
| CaseCite | [thomasunise/casecite](https://github.com/thomasunise/casecite) | Apache-2.0 | Legal RAG self-hosted **BYOK y sin telemetría**: cada afirmación contrastada contra su pasaje, deep research sobre corpus propio + CourtListener, pipeline de contratos con redline y **revisión tabular de cientos de contratos** con cada valor atado a su pasaje. Lo más cercano a lo que esta KB describe como producto ideal. | 286 | 2026-11-05 |
| LawGlance | [lawglance/lawglance](https://github.com/lawglance/lawglance) | Apache-2.0 | 🇮🇳 Asistente legal RAG libre. Primer activo de India en esta KB. | 343 | 2026-09-21 |
| Claude para Abogados | [betobetico/claude-para-abogados](https://github.com/betobetico/claude-para-abogados) | Apache-2.0 | 🇪🇸 Adaptación declarada de `claude-for-legal` al derecho **español y de la UE**: 20 módulos, 100 skills, 17 agentes. **Prueba de que la plantilla por jurisdicción se replica.** ⚠️ Es España (EMEA), **no LATAM**. | 49 | 2026-09-30 |
| mcp-legal-it | [capazme/mcp-legal-it](https://github.com/capazme/mcp-legal-it) | Apache-2.0 | 🇮🇹 MCP + plugin para derecho italiano, 200+ herramientas con statutes verificados. Pequeño pero real. | 33 | 2026-11-18 |

**8 agentes con señal. No se rellena la tabla hasta un número redondo.**

### Correcciones registradas este pase

1. ⚠️ **LA API DE GITHUB NO ESTÁ BLOQUEADA.** Esta KB lo afirmaba en tres ficheros. Reprobada hoy:
   `gh api -X GET search/repositories -f q='repo:<owner>/<name>'` devuelve existencia, SPDX,
   estrellas, `archived`, `pushed_at` y rama en **una sola llamada**. Lo que sí está bloqueado:
   `gh api repos/<owner>/<name>` (fuera de scope) y `curl` sobre `github.com` (403 del proxy).
   **Un canal declarado bloqueado por un pase anterior se vuelve a probar, nunca se hereda.**
2. ⚠️ **DOS RENOMBRADOS.** `microsoft/presidio` → **`data-privacy-stack/presidio`** (11.989★;
   probado con `LICENSE` idéntico de 1.084 B y MD5 `edb1b1745226` en ambos slugs) y
   `JSv4/OpenContracts` → **`Open-Source-Legal/OpenContracts`** (1.550★, coincide con el «1.5k★»
   que la KB atribuía al slug viejo). **Firma, idéntica en ambos:** `repo:` da **422** mientras
   `raw` sobre el slug viejo da **200** (GitHub sirve por redirección). Con sólo `raw` el
   renombrado es invisible; con sólo la API el repo parece borrado.
   **Tasa medida: 2 renombrados + 1 muerto en 31 URL ≈ 1 incidencia por 10 repos.**
3. ⚠️ **`TheAtticusProject/cuad` ESTÁ MUERTO**, no sólo sin licencia como se publicó. `repo:` da
   422 y `raw` da 404 en `main`, `master` y `HEAD`. El descarte era correcto por la razón
   equivocada.
4. ⚠️ **CUATRO DORMANCIAS NO DECLARADAS**, medidas por primera vez porque `pushed_at` nunca se
   había consultado: Blackstone **28 meses**, lawyer-llama **27**, DISC-LawLLM **18**,
   fuzi.mingcha **16**. Los dos últimos eran, textualmente, «los dos activos de APAC» de esta KB.
   Siguen sirviendo como modelos y corpus; **no son proyectos vivos.**
5. ⚠️ **«Kourti Legal» NO EXISTE.** Una fuente lo describía como practice management legal **MIT y
   self-hostable**, exactamente el hueco que esta KB declara. Buscado: `boyeesu/Kourti` (MIT, 1★),
   `kourti2026/kourti` (0★) y cuatro cuentas homónimas sin relación. **Un candidato que cerraría
   el hueco de la KB merece verificación nominal antes de celebrarlo.**
6. ⚠️ **Estrellas medidas por primera vez** en filas que la KB publicaba con «—»:
   claude-legal-skill **518**, DISC-LawLLM **961**, fuzi.mingcha **401**, mike **4.504**.

### Hueco declarado — y uno cerrado

- ✅ **CERRADO: «no hay agentes legales de origen EMEA ni APAC».** El pase anterior lo declaró.
  **Era un artefacto de búsqueda:** las búsquedas se hicieron en inglés sobre blogs y listicles.
  El canal `topic:legal-ai` / `topic:legal-tech` de GitHub devuelve de inmediato activos alemanes,
  italianos, coreanos, vietnamitas, taiwaneses, indios y chinos. **Un hueco hallado en blogs no es
  un hueco de mercado hasta buscarlo en el índice de la plataforma.**
- 🔴 **ABIERTO Y CONFIRMADO: ningún agente legal open source de origen LATAM con señal.** Medido
  hoy con vocabulario es/pt (`juridico IA agente contratos`, `direito juridico IA LGPD brasil`,
  `derecho legal IA abogados español`, `jurisprudencia IA busqueda legal`): todo lo hallado está
  entre 0 y 3★. ⚠️ Y el único activo en castellano con tracción, `claude-para-abogados`, es
  **derecho de España**. Contarlo como LATAM sería un error de etiquetado con consecuencias.

---

## 🗄️ Histórico de pases anteriores

## 2026-11-04 — primer pase con verificación de licencia byte a byte

**Qué cambió respecto al histórico:** el pase anterior (2026-07-02) era salida de pipeline
automático sin verificación. Este pase comprobó cada repo con `git ls-remote --symref` y **leyó
cada LICENSE** desde `raw.githubusercontent.com`. Resultado: 1 URL muerta, 1 licencia mal
atribuida por fuentes secundarias y 3 repos de industria equivocada.

### Agentes con señal real esta semana

| Nombre | Repo | Licencia (leída) | Por qué importa | Stars |
|--------|------|------------------|-----------------|-------|
| ContextGem | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | Extracción tipada **con cita al párrafo**; lee todos los párrafos en vez de hacer chunking por retrieval → no se pierde la cláusula rara. Backend de lectura: Docling. | 2.1k |
| OpenContracts | [JSv4/OpenContracts](https://github.com/JSv4/OpenContracts) | **MIT** | "DMS for the agentic world". Se reposiciona de gestor documental a plataforma de *document intelligence*. | 1.5k |
| lavern | [AnttiHero/lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | 67 agentes con **human gates obligatorios** + verificación de 10 pasos. El patrón, más que el código. Subió de 267★ (jul) a **320★**. | 320 |
| contract-review-agent | [lowtidebuild/contract-review-agent](https://github.com/lowtidebuild/contract-review-agent) | Apache-2.0 | Pasó de informes JSON/MD (v1-alpha) a **DOCX con tracked changes** (v1-beta). Subió de 40★ a 41★. | 41 |
| mike | [open-legal-products/mike](https://github.com/open-legal-products/mike) | ⚠️ AGPL-3.0 | Plataforma legal AI con actividad oct-2026. Licencia bloqueante para SaaS cerrado. | — |

**5 agentes con señal. No se rellena la tabla hasta un número redondo.**

### Correcciones registradas este pase

1. ⚠️ **`mahdyet1845/Consultor-Tributario-AI` está MUERTO.** No resuelve por `ls-remote` a
   2026-11-04. Aparecía en el histórico de abajo y en `intel/trends.md` como repo activo.
   Se marca en el histórico (no se borra: append-only) y se retira de `intel/trends.md`.
2. ⚠️ **OpenContracts es MIT, no GPL-3.** Fuentes secundarias (awesome-lists y resultados de
   búsqueda) lo listaban como GPL-3. Su `LICENSE` son 1.073 B de texto MIT. Esta es la razón por
   la que este pase lee ficheros en lugar de creer listados.
3. ⚠️ **Este fichero era byte a byte idéntico a `repos/trending.md`.** Dos ficheros con el mismo
   contenido no son dos observaciones; eran la misma consulta escrita dos veces. Desde este pase
   divergen: aquí van **agentes**, allí van **repos/infraestructura**.
4. Los repos de 0–2 estrellas del histórico (`ClauseCopilot`, `legal-mitra`,
   `AI-Powered-Legacy-Protection-POC`, `Solidity-Economic-Risk-Scanner`, `uk-legal-workflows`)
   **existen** pero no tienen señal. Se conservan como histórico, no como hallazgo.

### Hueco declarado
No apareció **ningún agente legal open source nuevo con tracción desde LATAM, EMEA o APAC**
en las búsquedas de esta semana, salvo los dos LLM legales chinos ya recogidos en `agents/top.md`
(DISC-LawLLM, fuzi.mingcha). Los agentes con tracción son anglófonos y de autor individual.

---

## 🗄️ Histórico

### 2026-07-02 — salida de pipeline automático (sin verificar)

> Conservado tal cual por la regla append-only. ⚠️ No verificado en su momento: licencias
> declaradas como `?`, estrellas de 0–2 y una URL que hoy está muerta (marcada abajo).

| Nombre | Licencia | Descripción | Stars |
|--------|----------|-------------|-------|
| [lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | An agentic law firm. Yours. 67 specialist AI agents that review documents throug | 267 |
| [arin](https://github.com/sandip-pathe/arin) | ? | Anaya is a local-first legal document workspace for reading, summarizing, and di | 1 |
| ⚠️ DEAD-URL (no resuelve 2026-11-04) — Consultor-Tributario-AI `mahdyet1845/Consultor-Tributario-AI` | ? | Analise a Reforma Tributária com IA e dados da web em tempo real para responder  | 0 |
| [legal-mitra](https://github.com/Ronald482777/legal-mitra) | ? | Build a secure, AI-driven digital justice platform with blockchain features usin | 0 |
| [uspto_fpd_mcp](https://github.com/Tam1379/uspto_fpd_mcp) | MIT | 🚀 Improve patent analysis with a high-performance MCP server for USPTO Final Pe | 2 |
| [nl-rag-qdrant-legal](https://github.com/kjgdgch65g/nl-rag-qdrant-legal) | MIT | 📄 Explore Retrieval-Augmented Generation for legal document Q&A, leveraging QDr | 6 |
| [AI-Powered-Legacy-Protection-POC](https://github.com/Sneaky-Pablo/AI-Powered-Legacy-Protection-POC) | ? | 🛡️ Empower families with AI-driven legacy planning and legal guidance for Spani | 0 |
| [uk-legal-workflows](https://github.com/Kalyuzhner1966/uk-legal-workflows) | ? | UK Legal AI Agents 2026 – Automation for Compliance, Contracts & Litigation | 2 |
| [ClauseCopilot](https://github.com/Afifmutaz/ClauseCopilot) | ? | 📄 Analyze vendor contracts effortlessly with ClauseCopilot, providing risk asse | 0 |
| [Solidity-Economic-Risk-Scanner](https://github.com/Jessej123-hash/Solidity-Economic-Risk-Scanner) | MIT |  | 1 |

---
*Append-only. Último pase: 2026-11-04.*

---
*Append-only. Último pase: 2026-11-20.*
