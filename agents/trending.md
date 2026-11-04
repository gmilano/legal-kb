---
industry: legal
region: Global
updated: 2026-11-04
---

# 📈 Agentes trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. No se reescribe: la serie temporal *es* el contenido.

## 🆕 2026-11-04 — primer pase con verificación de licencia byte a byte

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
