---
industry: legal
region: Global
updated: 2026-11-21
---

# 📈 Repos trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. Este fichero cubre **repos e infraestructura**; los agentes van en `agents/trending.md`.

## 🆕 2026-11-21 (pase 3) — un Estado mantiene ley-como-código en MIT, y el checksum de licencias se confirma entre industrias

**Divergencia mantenida:** este fichero cubre **repos e infraestructura**; los agentes y los
movimientos de producto van en `agents/trending.md`.

**Qué cambió respecto al pase de hace una hora:** el pase 2 cerró diciendo que *«el corpus
permisivo es más escaso que el código permisivo»* y que el corpus abierto venía de voluntarios
(`opencaselaw`) o de dominio público (`legal-templates`). **Hoy aparece una tercera fuente, y es
la de mayor autoridad posible: el propio Estado.**

### Repos de infraestructura nuevos (verificados 2026-11-20, pase 3)

| Repo | Licencia (leída) | Stars | Último commit | Señal |
|------|------------------|------:|---------------|-------|
| [betagouv/mon-entreprise](https://github.com/betagouv/mon-entreprise) | MIT (1.074 B) | 337 | **2026-11-20** | **Ley como código, mantenida por el Gobierno francés** (beta.gouv.fr). Derecho laboral/fiscal/societario francés como **reglas ejecutables** (`publicodes`), no como prompts. MIT ⇒ incorporable. |
| [thunlp/CAIL](https://github.com/thunlp/CAIL) | MIT (1.063 B) | 519 | 2019-05-13 🪦 | **Chinese AI & Law Challenge**: el benchmark fundacional de AI legal en chino. Cubre el hueco de evaluación en APAC (la KB sólo tenía LegalBench, en inglés). Entra **como dataset y definición de tarea**, no como código vivo. |
| [stella/stella](https://github.com/stella/stella) | Apache-2.0 (11.358 B) | 282 | **2026-11-20** | Workspace legal permisivo con commit de hoy; ver `verticals/solutions.md`. |

### 🧮 El checksum de bytes de licencia se corrobora ENTRE INDUSTRIAS ⇒ es una constante, no una heurística

Esta familia de KBs lleva meses registrando el tamaño en bytes de cada licencia. El pase 3 lo usó
como **checksum** sobre 7 licencias nuevas y no relacionadas: **7 dentro de banda, 0 fuera, 0
falsas alarmas.** El resultado decisivo:

> **`Prism-Legal-OS` mide 34.523 B de AGPL-3.0 — exactamente el mismo número que la KB de gaming
> registró para `grafana` y que esta KB registró para `courtlistener`.** Tres repos sin relación,
> tres industrias, un número idéntico ⇒ **la banda es la longitud del texto canónico de la FSF**,
> no una estimación local. Coste de red adicional: **cero** (el fichero ya se descarga para leerlo).

Bandas confirmadas: MIT/Expat **1.050–1.150** · CC0 **~7.048** · Apache-2.0 **~11.358** ·
MPL-2.0 ~16.700 · CC-BY-NC-ND-4.0 ~19.122 · **AGPL-3.0 ~34.523** · GPL-3.0 ~35.149.
Regla asimétrica: por encima de banda ⇒ licencia compuesta o preámbulo (**leer el fichero**); muy
por debajo ⇒ **fichero puntero** (seguir el puntero, **nunca** concluir «sin licencia»).

### 🔧 Instrumento nuevo del pase, aplicable a toda la rotación: identidad de HEAD por `git ls-remote`

```bash
# ¿El slug viejo y el nuevo son el mismo repo? Mismo SHA = sí, criptográficamente.
git ls-remote https://github.com/<slug-viejo> HEAD
git ls-remote https://github.com/<slug-nuevo> HEAD
```

`git ls-remote` **sigue la redirección de renombrado** y devuelve el SHA, así que cierra lo que ni
la API ni `raw` pueden cerrar por separado. Resultados en este fichero y en `agents/top.md`:
**3 renombrados probados por SHA** (incluido uno que el pase 2 había diagnosticado mal como «repo
no indexado») y **3 slugs de `LawLink` probados como un único codebase espejado** (mismo HEAD
`4736aa10…`, mismo titular de copyright), lo que **desbloquea** el único *practice management*
permisivo de la KB.

**Y lo que NO es un instrumento de existencia aquí:** `gh api repos/<owner>/<name>` devuelve **403
«access not enabled for this session»** para cualquier repo no adjunto, **incluidos los que existen
con certeza** (probado contra `docling-project/docling`, 70.826★). Un pase que lea ese 403 como
«borrado» destruiría filas vivas. Canales válidos: `search/repositories`, `raw`, `git ls-remote`.

### 📋 Barrido de integridad del pase 3

- **65 URL de GitHub** reextraídas y comprobadas: **62 resuelven**, **3 devuelven 422 y los 3
  están explicados** (2 slugs obsoletos citados a propósito + 1 renombrado no detectado, ya
  corregido). **0 enlaces roto sin declarar.**
- 🔧 **G-L7, hueco de método cerrado:** el barrido sólo miraba `github.com/...`, así que **28
  slugs citados en backticks sin URL nunca se habían verificado** — entre ellos
  **`lexifina/global-law`, de la que `repos/foundations.md` deriva toda la regla del grant partido
  código/corpus**. Verificados los 28: 24 se confirman, 1 (`nlpaueb/legal-bert`) no existe como
  repo y **la KB ya lo decía correctamente**, y 3 son los `LawLink`. La regla se sostuvo **por
  suerte, no por método**; ahora el barrido incluye los slugs sin enlace.
- Estrellas y `pushed_at` del pase 2: **revalidados uno por uno, coinciden** (máx. +1★).

---

## 🆕 2026-11-20 (pase 2) — el corpus en dominio público existe, y la capa de e-discovery nunca se había mirado

**Divergencia mantenida:** este fichero cubre **repos e infraestructura**; los agentes van en
`agents/trending.md`.

**Qué cambió respecto al pase de hace unas horas:** aquel pase escribió que *«el corpus permisivo
es más escaso que el código permisivo»* y coronó `General-Legal/legal-templates` (CC0) como el
único corpus incorporable a un entregable cerrado. **Hoy hay un segundo, y es jurisprudencia real,
no plantillas.**

### Repos de infraestructura con tracción (verificados 2026-11-20, pase 2)

| Repo | Licencia (leída) | Capa | Señal | Stars |
|------|------------------|------|-------|-------|
| [DevnorsAI/devnors-data-python](https://github.com/DevnorsAI/devnors-data-python) | MIT (1.064 B) | Acceso a datos | SDK Python de sentencias, normativa, registro mercantil y listas de morosos judiciales de China. Creado jul-2026, 867★ en 4 meses. | 867 |
| [shmsoft/FreeEed](https://github.com/shmsoft/FreeEed) | Apache-2.0 (12.177 B) | **E-discovery** | **Capa entera que esta KB no tenía.** Creado 2011-02-24, **commit de hoy**: 15 años de continuidad, el récord de esta KB con diferencia. | 155 |
| [ThomasMoreAI/legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | Apache-2.0 (11.314 B) | Conocimiento | 18.000+ skills en 54 jurisdicciones, **Apache-2.0 sobre el contenido**. Cobertura LATAM real. | 141 |
| [jonashertner/opencaselaw](https://github.com/jonashertner/opencaselaw) | **MIT (1.069 B) + CC0 datos** | **Corpus** | **El hallazgo del pase.** 1M+ sentencias suizas (1875–hoy, 26 cantones, 3 idiomas), 21k leyes, grafo de citas de 10M de aristas. MCP + REST + CLI + **Parquet**. Commit de hoy. | 80 |

**4 filas, las 4 verificadas por API de búsqueda + lectura byte a byte del LICENSE. 0 placeholders.**

### 🆕 Por qué `opencaselaw` cambia una conclusión publicada de este fichero

Este fichero venía sosteniendo que **el grant partido código/corpus** es el modo de fallo propio
del sector: código permisivo, corpus restringido. `opencaselaw` tiene el grant partido **a favor**:

| Parte | Licencia | Consecuencia |
|-------|----------|--------------|
| Código (42 tools MCP, REST, CLI) | MIT (1.069 B) | Se integra en producto cerrado. |
| **Datos (1M+ sentencias, 21k leyes, grafo de citas)** | **CC0** | **Dominio público: el texto entra en el entregable del cliente sin atribución ni cadena de licencias.** |

⇒ **El grant partido no es intrínsecamente un problema: es un problema cuando se parte en la
dirección contraria.** La lección operativa no es «desconfiar del grant partido», es
**«leer las dos mitades»** — que es lo que esta KB ya hacía y ahora tiene un caso positivo que lo
demuestra.

Y aporta una primitiva que ningún otro repo de esta KB tiene como comando:

```bash
# devuelve, por cada referencia: si la sentencia existe y cuál es
ocl citations resolve 'BGE 136 III 513' '4A_747/2012' 'BGE 999 III 1'
```

Con la regla de Indiana (Trial Rule 11, 1-ago-2026) y la sanción colombiana **AC739-2026**, esto
deja de ser una utilidad de investigación y pasa a ser **un control con consecuencia disciplinaria
detrás**. Ver `compose/patterns.md` → P10.

### Observación metodológica de este pase

El pase anterior corrigió la creencia heredada de que *«la API de GitHub está bloqueada»*. Este
pase corrige algo más fino: **las consultas estaban formuladas por nombre de agente, no por capa
de arquitectura.** Buscar `legal mcp server` y `ediscovery` devolvió 13 y 56 repos donde buscar
`legal ai agent` devolvía 13 en total. **La cobertura de una KB está limitada por el vocabulario
de sus consultas antes que por lo que existe en GitHub.**

⚠️ Y un recordatorio del coste del ruido: de los 56 resultados de `ediscovery`, **la mayoría son
falsos positivos de *service discovery*** (ECS, etcd, Prometheus). Una capa puede parecer vacía
porque el término está ocupado por otra industria.

### Huecos declarados

- 🔴 **Corpus LATAM en licencia permisiva: sigue vacío.** `opencaselaw` (CH) y `oldp` (DE) cubren
  EMEA; `CourtListener` (US) es AGPL-3.0. **No hay equivalente para ningún país LATAM.**
- 🟢 **Cerrado este pase:** e-discovery (`FreeEed`). Se deja constancia de que el hueco existió
  **sin declararse** durante todos los pases anteriores, porque la capa no se buscó.
- 🔴 **Practice management permisivo:** sigue abierto (ver `verticals/solutions.md`).

🗄️ *Nota de histórico: la sección de abajo es el primer pase del 2026-11-20, conservado íntegro.*

## 2026-11-20 (pase 1) — corpus, firma y el canal que esta KB creía cerrado

**Divergencia mantenida:** este fichero cubre **repos e infraestructura**; los agentes van en
`agents/trending.md`. Este pase añade dos capas que la KB no tenía: **corpus de plantillas con
licencia redistribuible** y **firma electrónica**.

### Repos de infraestructura con tracción (verificados 2026-11-20)

| Repo | Licencia (leída) | Por qué importa ahora | Stars | Último commit |
|------|------------------|----------------------|-------|---------------|
| [docling-project/docling](https://github.com/docling-project/docling) | MIT | **70.821★** (+721 en 16 días). Sigue siendo la entrada por defecto del pipeline documental y el backend de lectura de ContextGem. | **70.821** | 2026-11-20 |
| [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT (1.084 B) | **11.989★.** PII en texto, imágenes y datos estructurados; el componente que hace viables los despliegues EMEA (EU AI Act) y LATAM (LGPD). ⚠️ **RENOMBRADO** desde `microsoft/presidio` — la KB apuntaba al slug viejo. | **11.989** | 2026-11-19 |
| [Unstructured-IO/unstructured](https://github.com/Unstructured-IO/unstructured) | Apache-2.0 | **15.770★ — primera medición**: la KB lo publicaba con «—», así que resulta ser **más grande que Presidio**, no un complemento menor de Docling. | **15.770** | 2026-11-19 |
| [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | ⚠️ **AGPL-3.0** (35.051 B) | 🆕 **Capa que esta KB nunca tuvo: la firma electrónica.** Alternativa open source a DocuSign. Ningún flujo legal termina sin firma. ⚠️ La API dice `NOASSERTION`; el fichero son 35.051 B con 16 menciones a Affero. Rama por defecto **`staging`**. | **7.315** | 2026-11-20 |
| [apache/tika](https://github.com/apache/tika) | Apache-2.0 | **4.153★ — primera medición.** ~1.000 formatos; el que sigue ganando en e-discovery y formatos legacy. | 4.153 | 2026-11-20 |
| [General-Legal/legal-templates](https://github.com/General-Legal/legal-templates) | CC0-1.0 (7.048 B) | 🆕 **El mayor corpus abierto de plantillas legales hallado.** CC0 = dominio público sin atribución obligatoria: **el único régimen que permite incorporar el texto en un entregable cerrado de cliente** sin arrastrar cadena de licencias. | **3.753** | 2026-09-22 |
| [securitybunker/databunker](https://github.com/securitybunker/databunker) | MIT (1.078 B) | 🆕 Vault de PII con API para GDPR/CCPA: cifra y custodia los datos personales fuera de la base de la aplicación y devuelve tokens. **Complementa a Presidio** — Presidio *detecta y redacta*, Databunker *custodia*. Rama **`master`**. | 1.498 | 2026-11-20 |
| [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | MIT | **1.015★.** Entrevistas guiadas + document assembly. El documento sale de **plantilla determinista, no de generación** → el patrón más defendible que existe ante un regulador. Rama **`master`**. | 1.015 | 2026-11-13 |
| [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | ⚠️ **AGPL-3.0** (35.140 B, **`LICENSE.txt`**) | Archivo judicial EE. UU., muy activo. CaseCite lo usa como fuente externa de research. Gran corpus, licencia de red. | 1.076 | 2026-11-20 |
| [accordproject/template-archive](https://github.com/accordproject/template-archive) | Apache-2.0 (11.356 B) | 🆕 Plantillas del **Accord Project** (Linux Foundation): contratos como plantillas con lógica ejecutable. **Gobernanza de fundación, no de autor individual** — poco común en este sector y relevante para riesgo de proveedor. | 381 | 2026-10-20 |
| [openlegaldata/awesome-legal-data](https://github.com/openlegaldata/awesome-legal-data) | **NONE** ⚠️ | 🆕 Índice de fuentes de datos legales abiertos, del equipo de OLDP. Útil para localizar corpus por país. Sin licencia: usar como mapa, no redistribuir. Rama **`master`**. | 330 | 2026-10-20 |
| [Vaquill-AI/awesome-legaltech](https://github.com/Vaquill-AI/awesome-legaltech) | **NONE** ⚠️ | 🆕 **8× el índice que esta KB venía usando**, y además cubre servidores MCP. Mismo nombre de repo que `chen-friedman/awesome-legaltech` (34★), dueño distinto — **no es un renombrado, es que el pequeño estaba coronado.** | 273 | 2026-10-26 |
| [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | **MIT** | Sigue siendo **la única plataforma de corpus legal con licencia permisiva**. Django + Elasticsearch + API REST. | 164 | 2026-11-11 |
| [LexPredict/lexpredict-lexnlp](https://github.com/LexPredict/lexpredict-lexnlp) | ⚠️ **AGPL-3.0** | 798★ — **primera medición**. 🪦 Y **30 meses sin commits**, también primera medición. La KB lo listaba como repo fundacional sin indicar ninguna de las dos cosas. Rama **`master`**. | 798 | 2024-05-27 |

**14 repos, los 14 verificados hoy por API + lectura de licencia.**

### Observación metodológica de este pase — rectificando la del pase anterior

> El pase del 2026-11-04 escribió aquí: *«el payload AGPL es prácticamente constante porque no
> interpola ningún nombre»*, apoyándose en **35.140 B** (courtlistener), **34.519 B** (lexnlp) y
> **34.523 B** (mike). **Las tres cifras refutan la afirmación en el mismo renglón:** courtlistener
> difiere de los otros dos en **617 B**. Leído hoy el fichero, el motivo es que **sí lleva texto
> antepuesto**: `"This software and any associated files are Copyright 2010, Free Law Project."`
> sobre el AGPL canónico de ~34.523 B. Y un segundo error de método en la misma frase: la KB
> declaraba leer `.../<rama>/LICENSE`, pero **courtlistener no tiene `LICENSE`** — tiene
> **`LICENSE.txt`**, y `LICENSE` devuelve 404. **El procedimiento publicado no reproducía el
> resultado publicado.**

**La regla correcta, y es útil:** las licencias tienen longitudes canónicas — MIT/Expat
1.050–1.150, CC0 ~7.048, Apache-2.0 ~11.358, MPL-2.0 ~16.700, AGPL-3.0 ~34.523, GPL-3.0 ~35.149.
Una fila cuyos bytes caen fuera de la banda de su familia **está mal clasificada o lleva texto
añadido**, y la regla es **asimétrica**: bytes *por encima* ⇒ preámbulo o licencia compuesta (leer
el fichero); bytes *muy por debajo* ⇒ **fichero puntero** (seguir el puntero, nunca concluir «sin
licencia»). Aplicada hoy a 12 licencias leídas: **3 señaladas, 3 explicadas, 0 falsas alarmas.**

### 🆕 Un modo de fallo nuevo, y es específico de esta industria

**En legal, la licencia del repo frecuentemente NO cubre el texto legal que contiene.** Los dos
casos los destapó la regla de bytes:

- **`lexifina/global-law`** (2.143★, activo hoy) — `LICENSE.md` de **935 B**, muy por debajo de los
  ~7.048 de CC0 ⇒ señalado como puntero. Es **CC0 1.0 en forma corta** y lleva una sección
  *«What this does not cover»*: cubre el árbol de jurisdicciones, el manifiesto, las herramientas,
  los tests y la documentación — **no la ley**, que vive en `lexifina/<country>-law` como
  **submódulos git, cada uno con su propio LICENSE y SOURCES.md**. La API dice `NOASSERTION`.
- **`mhfed/vn-law-check`** (508★) — `LICENSE` de **1.356 B**, ~200 por encima de la banda MIT ⇒
  señalado. Es **MIT + nota añadida**: *«does not and cannot license the underlying Vietnamese
  legal texts»*. (Su aviso de copyright nombra *"Contributors to vn-web-compliance-audit"*, **un
  proyecto distinto del nombre del repo** — señal de derivación sin confirmar.)

**Por qué importa para un entregable:** decir «el repo es MIT» **no responde la pregunta del
cliente**, que es *¿puedo redistribuir el corpus?*. Son **dos licencias** y hay que verificar las
dos. Es el análogo exacto de la pregunta de los *pesos del modelo* que la KB de gaming dejó
abierta: en ambos casos **la mitad del entregable queda fuera de la licencia que se verificó.**

### Huecos declarados

- ✅ **CERRADO: «ningún repo de infraestructura legal de origen EMEA/APAC».** Artefacto de
  búsqueda. El canal `topic:` devuelve activos alemanes, italianos, franceses (`betagouv/mon-entreprise`,
  MIT, 337★, del gobierno francés), rumanos, coreanos, vietnamitas, taiwaneses e indios.
- 🔴 **Ningún repo de infraestructura legal de origen LATAM.** Confirmado hoy con vocabulario es/pt.
- 🔴 **No existe practice management open source permisivo con procedencia clara** — y este pase
  **refutó el único candidato** («Kourti Legal» no existe). Ver `verticals/solutions.md`.
- 🔴 **No existe firma electrónica open source permisiva.** OpenSign, la única relevante, es
  AGPL-3.0. Para un entregable cerrado esta capa se compra, no se forkea.
- 🔴 **En legal el corpus es más escaso que el código:** de los cinco repos de datos de
  `repos/foundations.md`, **sólo dos permiten redistribuir** (OLDP MIT, legal-templates CC0); dos
  son AGPL y uno no declara licencia. Al contrario que en la mayoría de industrias de esta rotación.

---

## 🗄️ Histórico de pases anteriores

## 2026-11-04 — infraestructura, no agentes

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

---
*Append-only. Último pase: 2026-11-20.*
