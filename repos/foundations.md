---
industry: legal
region: Global
updated: 2026-11-04
---

# 🏗️ Repos fundacionales — Legal Services

> Bases sobre las cuales construir. Licencia abierta, comunidad activa.
> Última actualización: 2026-11-04
>
> Verificación: existencia por `git ls-remote --symref`, licencia leída desde el LICENSE real
> en la rama por defecto. La columna de rama importa: tres de estos repos **no están en `main`**.

## Ingesta y parsing documental (la capa que todo engagement legal necesita primero)

| Repo | Rama | Licencia (leída) | Descripción | Stars | ¿Base para AI? |
|------|------|------------------|-------------|-------|----------------|
| [docling-project/docling](https://github.com/docling-project/docling) | main | MIT | "Get your documents ready for gen AI". Parsea PDF, DOCX, PPTX, XLSX, HTML, EPUB, ODT/ODS/ODP, email (EML/MSG), imágenes, LaTeX, audio y vídeo, preservando estructura y números de página. | 70.1k | ✅ entrada canónica del pipeline |
| [Unstructured-IO/unstructured](https://github.com/Unstructured-IO/unstructured) | main | Apache-2.0 | Librerías de preprocesado e ingesta de documentos para LLM/RAG. Alternativa/complemento a Docling con más conectores. | — | ✅ ingesta a escala |
| [apache/tika](https://github.com/apache/tika) | main | Apache-2.0 | Detección de tipo y extracción de contenido/metadatos para ~1.000 formatos. Maduro, JVM, probado en e-discovery. | — | ✅ formatos legacy y forense |

## Privacidad, PII y compliance

| Repo | Rama | Licencia (leída) | Descripción | Stars | ¿Base para AI? |
|------|------|------------------|-------------|-------|----------------|
| [microsoft/presidio](https://github.com/microsoft/presidio) | main | MIT | Detección, redacción, enmascarado y anonimización de PII en texto, imágenes y datos estructurados. | 11.7k | ✅ habilitador de LGPD / GDPR / EU AI Act |

## Automatización de documentos y acceso a la justicia

| Repo | Rama | Licencia (leída) | Descripción | Stars | ¿Base para AI? |
|------|------|------------------|-------------|-------|----------------|
| [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | **master** | MIT | Sistema experto libre para entrevistas guiadas y *document assembly*, basado en Python, YAML y Markdown. El estándar de facto en access-to-justice. | 999 | ✅ intake y redacción guiada |
| [SuffolkLITLab/docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | main | MIT | "Quickly go from a paper court form to a runnable, guided, step-by-step web application powered by Docassemble". Proyecto insignia: CourtFormsOnline.org. | 73 | ✅ formularios judiciales → web app |

## Datos legales abiertos (corpus para RAG y benchmarking)

| Repo | Rama | Licencia (leída) | Descripción | Stars | ¿Base para AI? |
|------|------|------------------|-------------|-------|----------------|
| [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | main | MIT | Plataforma de datos legales abiertos (sentencias y leyes) con API REST y búsqueda Elasticsearch. Django, Python 3.12. Demo y tema en alemán → datos legales alemanes. | 158 | ✅ **el único corpus-platform permisivo (MIT)** |
| [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | main | **AGPL-3.0** ⚠️ | "A fully-searchable and accessible archive of court data": opiniones, audios de alegatos, jueces, declaraciones financieras judiciales y expedientes federales (EE. UU.). 26.634 commits. | 1.1k | ⚠️ sí, pero ver nota AGPL |
| [LexPredict/lexpredict-lexnlp](https://github.com/LexPredict/lexpredict-lexnlp) | **master** | **AGPL-3.0** ⚠️ | LexNLP: extracción de hechos legales (fechas, montos, cláusulas, definiciones, jurisdicciones) sobre texto legal. Base de ContraxSuite. | — | ⚠️ sí, pero ver nota AGPL |

## Índices de investigación

| Repo | Rama | Licencia (leída) | Descripción | Stars |
|------|------|------------------|-------------|-------|
| [maastrichtlawtech/awesome-legal-nlp](https://github.com/maastrichtlawtech/awesome-legal-nlp) | **master** | MIT | Lista curada de recursos de Legal NLP. | — |
| [chen-friedman/awesome-legaltech](https://github.com/chen-friedman/awesome-legaltech) | main | CC0-1.0 | Legal AI/LegalTech curado, **etiquetado por jurisdicción** — útil precisamente para colocar hallazgos por región. | — |

**12 repos reales, los 12 vivos, las 12 licencias leídas del fichero.**

## Por qué estos repos

### La capa de parsing es el cuello de botella real, no el modelo
En legal, el 80% del esfuerzo es convertir un PDF escaneado de 200 páginas en algo con estructura.
**Docling** (MIT, 70.1k★) es hoy la entrada por defecto y además es el backend de lectura de
**ContextGem**, lo que hace que esos dos encajen sin pegamento.

### ⚠️ Nota de licencia AGPL-3.0 — leer antes de proponer
`courtlistener`, `lexnlp` y `mike` son **AGPL-3.0** (verificado leyendo el LICENSE: 35.140 B,
34.519 B y 34.523 B respectivamente — el payload AGPL es constante porque no interpola nombre).
AGPL es copyleft **de red**: si el cliente expone el servicio por red, debe ofrecer el código
fuente de la obra derivada. Para un entregable SaaS propietario esto es normalmente un
bloqueante contractual, no un detalle. Alternativas permisivas: **OLDP (MIT)** para
corpus-platform, y **Blackstone (Apache-2.0)** + **ContextGem (Apache-2.0)** para extracción.

### Lo que se eliminó de este fichero y por qué
La versión anterior (2026-07-02) listaba **mythril**, **heimdall-rs** y **solgraph** como
repos fundacionales de legal. Son herramientas de análisis de bytecode **EVM / smart contracts**:
entraron por la coincidencia léxica de "contract" y no tienen relación con servicios legales.
También listaba `Paparusi/legal-ai-agent` (vivo, pero sin descripción ni señal). Retirados.

---
*Ver también: `verticals/solutions.md` para plataformas verticales completas. Verificado 2026-11-04.*
