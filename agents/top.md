---
industry: legal
region: Global
updated: 2026-11-04
---

# 🎯 Agentes AI — Legal Services

> Agentes y herramientas AI open source para la industria legal. Foco: MIT / Apache 2.0 / BSD.
> Última actualización: 2026-11-04
>
> **Método de verificación (2026-11-04):** cada repo se comprobó vivo con
> `git ls-remote --symref` (devuelve la rama por defecto real) y **cada licencia se leyó
> byte a byte** desde `raw.githubusercontent.com/<repo>/<rama>/LICENSE`. No se tomó ninguna
> licencia de un listicle ni de la API de GitHub (bloqueada por el proxy de esta sesión).
> Las estrellas sólo se declaran donde se leyeron ese día; `—` significa *no releído*, no cero.

## Agentes y herramientas destacadas

| Nombre | Repo | Licencia (leída) | Descripción | Stars (2026-11-04) |
|--------|------|------------------|-------------|--------------------|
| Presidio | [microsoft/presidio](https://github.com/microsoft/presidio) | MIT | Framework para detectar, redactar, enmascarar y anonimizar PII en texto, imágenes y datos estructurados. Pieza obligatoria antes de enviar documento de cliente a cualquier LLM externo. | 11.7k |
| ContextGem | [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) | Apache-2.0 | Extracción estructurada de documentos con LLMs: defines *aspects* (temas) y *concepts* (valores tipados) en lenguaje natural y genera los prompts. Devuelve tipos (fecha, número, label, rating, JSON) **con trazabilidad al párrafo/oración de origen**. Lee todos los párrafos — no hace chunking por retrieval, así que no se le escapan cláusulas mal rankeadas. | 2.1k |
| OpenContracts | [JSv4/OpenContracts](https://github.com/JSv4/OpenContracts) | MIT | "The open document intelligence platform for builders and hackers — DMS for the agentic world". Repositorio de contratos + analítica de cláusulas + anotación. Django + frontend JS. | 1.5k |
| Blackstone | [ICLRandD/Blackstone](https://github.com/ICLRandD/Blackstone) | Apache-2.0 | Pipeline y modelo spaCy para NLP sobre texto legal no estructurado (rama `master`). El README se declara *early prototype*: útil como base de NER legal, no como producto. | 703 |
| lavern | [AnttiHero/lavern](https://github.com/AnttiHero/lavern) | Apache-2.0 | "An agentic law firm. Yours." 67 agentes especialistas que revisan documentos mediante *evidence-backed debate*, con **human gates obligatorios** (los hallazgos críticos no se entregan sin aprobación humana) y pipeline de verificación de 10 pasos (context, ux, clarity, structure, accuracy, completeness, risk, formatting, legal_design, delivery). TypeScript. | 320 |
| contract-review-agent | [lowtidebuild/contract-review-agent](https://github.com/lowtidebuild/contract-review-agent) | Apache-2.0 | Revisión de contratos local-first: todo el procesamiento ocurre en el filesystem local. Produce **DOCX con tracked changes** (redline interno, limpio externo y reporte), comentarios al margen y recomendaciones de negociación. | 41 |
| claude-legal-skill | [evolsb/claude-legal-skill](https://github.com/evolsb/claude-legal-skill) | MIT | Skill de revisión de contratos con detección de riesgo basada en CUAD y benchmarking de mercado. | — |
| DISC-LawLLM | [FudanDISC/DISC-LawLLM](https://github.com/FudanDISC/DISC-LawLLM) | Apache-2.0 | 中文法律大模型 — sistema legal inteligente sobre LLM para derecho chino (Fudan DISC). Relevante para engagements APAC. | — |
| fuzi.mingcha (夫子·明察) | [irlab-sdu/fuzi.mingcha](https://github.com/irlab-sdu/fuzi.mingcha) | Apache-2.0 | LLM judicial chino (Universidad de Shandong + Inspur Cloud + CUPL) sobre base ChatGLM, entrenado con corpus judicial chino. Relevante para APAC. | — |
| mike | [open-legal-products/mike](https://github.com/open-legal-products/mike) | **AGPL-3.0** ⚠️ | "OSS Legal AI Platform", actividad reciente (oct 2026). ⚠️ **AGPL-3.0 leída en el LICENSE (34.523 B)** — copyleft de red: inviable para producto SaaS cerrado de cliente sin liberar el código. Sirve como referencia de arquitectura. | — |

**10 agentes reales, los 10 vivos y con licencia leída.** No hay filas de ejemplo ni placeholders en esta tabla.

## Agentes por función

### Revisión y redline de contratos
- **contract-review-agent** — el único de la lista que entrega **DOCX con tracked changes**, que es el formato en que un abogado realmente negocia. Local-first.
- **ContextGem** — la capa de extracción: cláusulas tipadas con cita al párrafo de origen (auditable).
- **claude-legal-skill** — detección de riesgo apoyada en CUAD.

### Repositorio e inteligencia documental
- **OpenContracts** — DMS + analítica de cláusulas; el punto de partida si el cliente necesita *dónde viven* los contratos, no sólo revisarlos.

### Privacidad y compliance (transversal, no opcional)
- **Presidio** — de-identificación de PII antes de cualquier egreso a un LLM. Es el componente que hace viables los patrones EMEA (EU AI Act) y LATAM (LGPD).

### Orquestación multi-agente con control humano
- **lavern** — su valor para Globant no es el código sino el **patrón**: human gates obligatorios + verificación multi-paso. Es exactamente la forma que exige un despliegue legal defendible.

### NLP legal y jurisdicciones específicas
- **Blackstone** — NER/parsing de texto legal (inglés).
- **DISC-LawLLM**, **fuzi.mingcha** — razonamiento legal en chino; los dos activos de APAC de la lista.

## Descartes documentados de este pase

No se incluyen por razones explícitas, para que no vuelvan a entrar por keyword:

- **`mahdyet1845/Consultor-Tributario-AI`** — **URL muerta**. `git ls-remote` no resuelve a 2026-11-04. Estaba publicado como dato en `agents/trending.md` e `intel/trends.md`.
- **mythril, heimdall-rs, solgraph** — reales y MIT/ISC, pero son herramientas de seguridad de **smart contracts EVM**, no de servicios legales. Entraron por la palabra "contract". Pertenecen a una KB de blockchain, no a esta.
- **CUAD** ([TheAtticusProject/cuad](https://github.com/TheAtticusProject/cuad)) y **lex-glue** ([coastalcph/lex-glue](https://github.com/coastalcph/lex-glue)) — vivos y valiosos como dataset/benchmark, pero **sin fichero LICENSE** (probado contra LICENSE, LICENSE.md, LICENSE.txt, COPYING, LICENCE). Usables para evaluación interna, no para redistribuir en un entregable de cliente sin aclarar términos.
- **`nlpaueb/legal-bert`** — no existe como repo GitHub (es un modelo HuggingFace). Verificado ABSENT.
- Repos de 0–2 estrellas sin descripción del pase automático anterior (`ClauseCopilot`, `legal-mitra`, `Solidity-Economic-Risk-Scanner`, etc.): vivos pero sin señal; no son hallazgos.

---
*Verificado repo por repo el 2026-11-04 (ls-remote + lectura de LICENSE). 10 filas reales, 0 placeholders.*
