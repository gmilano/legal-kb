---
industry: legal
region: Global
updated: 2026-11-04
---

# 📈 Repos trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. Este fichero cubre **repos e infraestructura**; los agentes van en `agents/trending.md`.

## 🆕 2026-11-04 — infraestructura, no agentes

**Divergencia deliberada:** hasta este pase, este fichero era **byte a byte idéntico** a
`agents/trending.md`. Desde hoy cubre la capa de infraestructura — parsing, PII, corpus — que es
donde está el trabajo real de un engagement legal y donde el histórico no miraba.

### Repos de infraestructura con tracción (verificados 2026-11-04)

| Repo | Licencia (leída) | Por qué importa ahora | Stars |
|------|------------------|----------------------|-------|
| [docling-project/docling](https://github.com/docling-project/docling) | MIT | **70.1k★.** Se ha convertido en la entrada por defecto del pipeline documental: PDF, DOCX, PPTX, XLSX, HTML, EPUB, ODF, email, imágenes, LaTeX, audio y vídeo, preservando estructura y páginas. Es además el backend de lectura de ContextGem. | 70.1k |
| [microsoft/presidio](https://github.com/microsoft/presidio) | MIT | **11.7k★.** PII en texto, imágenes y datos estructurados. En 2026 deja de ser "nice to have": es el componente que hace viables los despliegues EMEA (EU AI Act) y LATAM (LGPD). | 11.7k |
| [Unstructured-IO/unstructured](https://github.com/Unstructured-IO/unstructured) | Apache-2.0 | Alternativa/complemento a Docling con más conectores de ingesta. | — |
| [apache/tika](https://github.com/apache/tika) | Apache-2.0 | ~1.000 formatos. El que sigue ganando en e-discovery y formatos legacy. | — |
| [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | MIT | **999★.** Entrevistas guiadas + document assembly. El documento sale de plantilla determinista, no de generación → patrón defendible. | 999 |
| [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | **MIT** | **La única plataforma de corpus legal con licencia permisiva** hallada. Django + Elasticsearch + API REST. Alternativa a CourtListener cuando el entregable es cerrado. | 158 |
| [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | ⚠️ **AGPL-3.0** | 26.634 commits, archivo judicial EE. UU. Gran corpus, licencia de red. | 1.1k |
| [chen-friedman/awesome-legaltech](https://github.com/chen-friedman/awesome-legaltech) | CC0-1.0 | Índice **etiquetado por jurisdicción** — directamente útil para colocar hallazgos por región. | — |

**8 repos, los 8 vivos, las 8 licencias leídas del fichero.**

### Observación metodológica de este pase

Las licencias AGPL-3.0 leídas en este pase miden **35.140 B** (courtlistener), **34.519 B**
(lexnlp) y **34.523 B** (mike): el payload AGPL es prácticamente constante porque **no interpola
ningún nombre**. Las MIT, en cambio, varían (1.070–1.110 B) porque el texto MIT **contiene el
titular del copyright**. Consecuencia práctica: el tamaño del fichero sirve para detectar AGPL de
un vistazo, pero **no** para identificar MIT — hay que leer el cuerpo.

### Huecos declarados

- 🔴 **Ningún repo de infraestructura legal con origen LATAM, EMEA o APAC** apareció con tracción
  esta semana. OLDP es el único no-estadounidense relevante (datos alemanes, MIT).
- 🔴 **No existe practice management open source permisivo con procedencia clara.** Litigious es
  AGPL-3.0; LexATT y ArkCase no declaran licencia; LawLink es MIT pero con **tres copias casi
  idénticas** bajo cuentas distintas y upstream canónico sin establecer. Ver `verticals/solutions.md`.

---

## 🗄️ Histórico

### 2026-07-02 — salida de pipeline automático (sin verificar)

> Conservado tal cual por la regla append-only. ⚠️ Idéntico a `agents/trending.md` en su momento;
> licencias `?`, varios repos de 0–2 estrellas y una URL hoy muerta (marcada abajo).

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
