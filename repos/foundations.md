---
industry: legal
region: Global
updated: 2026-11-21
---

# 🏗️ Repos fundacionales — Legal Services

> Bases sobre las cuales construir. Licencia abierta, comunidad activa.
> Última actualización: 2026-11-20
>
> Verificación por doble canal: **API de búsqueda de GitHub** (existencia, SPDX, estrellas,
> `archived`, `pushed_at`, rama) + **lectura byte a byte del LICENSE** en `raw` sobre `/HEAD/`.
> La columna de rama importa: cuatro de estos repos **no están en `main`**.

## Ingesta y parsing documental (la capa que todo engagement legal necesita primero)

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [docling-project/docling](https://github.com/docling-project/docling) | main | MIT | "Get your documents ready for gen AI". Parsea PDF, DOCX, PPTX, XLSX, HTML, EPUB, ODT/ODS/ODP, email (EML/MSG), imágenes, LaTeX, audio y vídeo, preservando estructura y números de página. | **70.821** | 2026-11-20 |
| [Unstructured-IO/unstructured](https://github.com/Unstructured-IO/unstructured) | main | Apache-2.0 | Librerías de preprocesado e ingesta de documentos para LLM/RAG. Alternativa/complemento a Docling con más conectores. **Primera medición de estrellas en esta KB** (antes «—»). | **15.770** | 2026-11-19 |
| [apache/tika](https://github.com/apache/tika) | main | Apache-2.0 | Detección de tipo y extracción de contenido/metadatos para ~1.000 formatos. Maduro, JVM, probado en e-discovery. **Primera medición de estrellas** (antes «—»). | **4.153** | 2026-11-20 |

## Privacidad, PII y compliance

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | main | MIT (1.084 B) | Detección, redacción, enmascarado y anonimización de PII en texto, imágenes y datos estructurados. ⚠️ **RENOMBRADO desde `microsoft/presidio`** — ver `agents/top.md`. | **11.989** | 2026-11-19 |
| [securitybunker/databunker](https://github.com/securitybunker/databunker) | **master** | MIT (1.078 B) | Vault de datos personales con API, pensado para GDPR/CCPA: almacena PII cifrada fuera de la base de datos de la aplicación y devuelve tokens. **Nuevo en esta KB.** Complementa a Presidio: Presidio *detecta y redacta*, Databunker *custodia*. | 1.498 | 2026-11-20 |

## Automatización de documentos y acceso a la justicia

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | **master** | MIT | Sistema experto libre para entrevistas guiadas y *document assembly*, basado en Python, YAML y Markdown. El estándar de facto en access-to-justice. **El documento sale de plantilla determinista, no de generación → patrón defendible ante un regulador.** | 1.015 | 2026-11-13 |
| [SuffolkLITLab/docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | main | MIT | "Quickly go from a paper court form to a runnable, guided, step-by-step web application powered by Docassemble". Proyecto insignia: CourtFormsOnline.org. | 75 | 2026-11-20 |

## Datos legales abiertos (corpus para RAG y benchmarking)

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | main | MIT | Plataforma de datos legales abiertos (sentencias y leyes) con API REST y búsqueda Elasticsearch. Django, Python 3.12. Datos legales alemanes. **El único corpus-platform permisivo (MIT).** | 164 | 2026-11-11 |
| [General-Legal/legal-templates](https://github.com/General-Legal/legal-templates) | main | CC0-1.0 (7.048 B) | **Nuevo en esta KB y el mayor corpus de plantillas legales abierto que se encontró.** CC0 = dominio público, sin obligación de atribución: el único régimen que permite incorporar el texto en un entregable cerrado de cliente sin cadena de licencias. | **3.753** | 2026-09-22 |
| [accordproject/template-archive](https://github.com/accordproject/template-archive) | main | Apache-2.0 (11.356 B) | Archivo de plantillas del **Accord Project** (Linux Foundation): contratos como plantillas con lógica ejecutable (*smart legal contracts*). **Nuevo en esta KB.** Gobernanza de fundación, no de autor individual — poco común en este sector. | 381 | 2026-10-20 |
| [openlegaldata/awesome-legal-data](https://github.com/openlegaldata/awesome-legal-data) | **master** | **NONE** ⚠️ | Índice de fuentes de datos legales abiertos, del mismo equipo que OLDP. Útil para localizar corpus por país. ⚠️ Sin fichero de licencia: usar como *mapa*, no redistribuir su contenido. | 330 | 2026-10-20 |
| [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | main | **AGPL-3.0** ⚠️ (35.140 B en `LICENSE.txt`) | "A fully-searchable and accessible archive of court data": opiniones, audios de alegatos, jueces, declaraciones financieras judiciales y expedientes federales (EE. UU.). Muy activo. | 1.076 | 2026-11-20 |
| [LexPredict/lexpredict-lexnlp](https://github.com/LexPredict/lexpredict-lexnlp) | **master** | **AGPL-3.0** ⚠️ | LexNLP: extracción de hechos legales (fechas, montos, cláusulas, definiciones, jurisdicciones). Base de ContraxSuite. 🪦 **30 meses sin commits** — medido por primera vez aquí. | 798 | 2024-05-27 |
| [jonashertner/opencaselaw](https://github.com/jonashertner/opencaselaw) | main | **MIT código (1.069 B) + CC0 datos** | 🆕 **Resuelve el problema que este fichero lleva declarando desde el primer pase: el corpus permisivo es más escaso que el código permisivo.** Corpus legal suizo: **1M+ sentencias de los 26 cantones (1875–hoy)**, 21k leyes, **grafo de citas de 10M de aristas**, en alemán, francés e italiano. Se consume por **MCP (42 herramientas), REST, CLI o descarga Parquet**. CC0 sobre los datos = dominio público: el texto entra en un entregable cerrado de cliente sin cadena de licencias. Incluye `ocl citations resolve`, que comprueba si una cita existe. | 80 | 2026-11-20 |
| [DevnorsAI/devnors-data-python](https://github.com/DevnorsAI/devnors-data-python) | main | MIT (1.064 B) | 🆕 SDK Python sobre datos legales y corporativos chinos: sentencias (**裁判文书**), leyes y articulado (**法律法规/法条**), registro mercantil, cuentas anuales, datos fiscales y listas de morosos judiciales (**失信核查/被执行人**). Par del servidor MCP del mismo equipo. **El primer acceso programático a fuentes legales chinas en esta KB.** | 867 | 2026-09-15 |

## 🆕 Ley como código, y el benchmark fundacional que faltaba (pase 3)

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [betagouv/mon-entreprise](https://github.com/betagouv/mon-entreprise) | main | MIT (1.074 B) | 🆕 **El activo más inesperado del pase 3 y el único mantenido por un Estado.** «L'assistant officiel des entrepreneurs» de **beta.gouv.fr (Gobierno francés)**: codifica derecho laboral, fiscal y societario francés como **reglas ejecutables** (motor `publicodes`), no como prompts. MIT, con commits de hoy. **Es la prueba de existencia de la tesis que este fichero defiende** — que el documento/cálculo salga de una regla determinista y no de generación — y además con una fuente de autoridad que ningún LLM puede igualar: **el propio Estado la mantiene**. | 337 | **2026-11-20** |
| [thunlp/CAIL](https://github.com/thunlp/CAIL) | main | MIT (1.063 B) | 🆕 **Chinese AI & Law Challenge** (THUNLP) — el benchmark fundacional de AI legal en chino: predicción de sentencia, recuperación de jurisprudencia y QA legal. **Cubre el hueco de evaluación en APAC** que esta KB sólo tenía cubierto para inglés (LegalBench) . 🪦 **Sin commits desde 2019-05-13: 7 años.** Se incorpora **como dataset y como definición de tarea**, que no caducan, explícitamente **no** como código mantenido. | 519 | 2019-05-13 🪦 |

> 📌 **Por qué un repo de 2019 entra en «foundations» mientras un repo dormido de 6 meses se
> marca 🪦 en `agents/top.md`.** Porque **la dormancia significa cosas distintas según el tipo de
> activo**: un *dataset* o una *definición de benchmark* no se degrada con el tiempo — CAIL define
> tareas y reparte etiquetas, y eso sigue siendo válido y citable. Un *agente* dormido sí se
> degrada, porque depende de APIs de modelos, de SDKs y de formatos de skill que cambian cada mes.
> ⇒ **Regla: aplicar el umbral de dormancia al código ejecutable, no al corpus ni al benchmark.**
> Esta KB venía aplicando un único umbral a todo, que es lo que hacía parecer «muertos» activos de
> datos perfectamente utilizables (y lo que, al revés, dejaba pasar agentes dormidos como vivos).

## 🆕 E-discovery — una capa que esta KB no tenía en ningún fichero

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [shmsoft/FreeEed](https://github.com/shmsoft/FreeEed) | main | Apache-2.0 (12.177 B) | **La única plataforma de e-discovery open source con mantenimiento real que se encontró.** Procesamiento de evidencia electrónica: ingesta de contenedores (PST, ZIP, imágenes forenses), deduplicación, extracción de metadatos, cultling y producción. **Creada en 2011 y con commits de hoy mismo (2026-11-20)** — 15 años de continuidad, algo que ningún otro activo de esta KB puede decir. | 155 | 2026-11-20 |

> **Por qué importa el hueco que cierra.** E-discovery es donde el sector legal **ya** gasta en
> volumen de datos, y es el flujo que mejor tolera automatización porque el output es un conjunto
> de documentos responsivos, no un consejo jurídico: **el riesgo de alucinación no se traslada al
> cliente final de la misma forma.** Hasta hoy esta KB no tenía una sola fila en esta capa.
>
> ⚠️ **Descartes medidos en la misma búsqueda** (para que nadie repita el barrido): la consulta
> `ediscovery OR e-discovery` devuelve 56 repos y **casi todos son falsos positivos de
> *service discovery*** (ECS, etcd, Prometheus). De los realmente legales:
> `FreeDiscovery/FreeDiscovery` (79★) está **muerto desde 2022-06** y en `NOASSERTION`.

## 🆕 Bibliotecas de skills legales por jurisdicción

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [ThomasMoreAI/legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | main | Apache-2.0 (11.314 B) | **18.000+ skills `SKILL.md`, 410+ plugins, 54 jurisdicciones, 48 áreas de práctica**, organizados por código de país. Apache-2.0 cubre **el contenido**, no sólo el código — poco común en corpus de conocimiento. Cubre LATAM (`br/` 15, `ar/` 2, `mx/` 2, `co/` 1, `pe/` 1, `do/` 1). Acepta contribuciones por jurisdicción. | 141 | 2026-10-12 |
| [lawve-ai/awesome-legal-skills](https://github.com/lawve-ai/awesome-legal-skills) | main | 🔴 **CC-BY-NC-ND 4.0** (19.122 B) | El índice de skills legales más grande (966★) y **el peor régimen de licencia de esta KB**. NonCommercial bloquea el uso en engagement; NoDerivatives bloquea adaptarlo a la jurisdicción del cliente. 🔴 **Mapa de lectura, nunca insumo.** Ver `agents/top.md` → modos de fallo de licencia. | **966** | 2026-10-19 |

## Índices de investigación

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [maastrichtlawtech/awesome-legal-nlp](https://github.com/maastrichtlawtech/awesome-legal-nlp) | **master** | MIT | Lista curada de recursos de Legal NLP. Académica (Maastricht). | 347 | 2025-10-14 |
| [Vaquill-AI/awesome-legaltech](https://github.com/Vaquill-AI/awesome-legaltech) | main | **NONE** ⚠️ | Lista curada de LegalTech: plataformas open source, modelos AI, **servidores MCP**, empresas, datasets. **8× más grande que el índice que esta KB venía usando** — ver corrección abajo. ⚠️ Sin licencia. | 273 | 2026-10-26 |
| [chen-friedman/awesome-legaltech](https://github.com/chen-friedman/awesome-legaltech) | main | CC0-1.0 | Legal AI/LegalTech curado, **etiquetado por jurisdicción**. Pequeño (34★) pero es el único de los tres índices con licencia limpia. | 34 | 2026-04-06 |

**16 repos reales, los 16 verificados hoy, las 16 licencias comprobadas (12 leídas del fichero, 2 `NONE` confirmadas, 2 por SPDX de API coincidente con lectura previa).**

## ⚠️ Corrección: el índice equivocado estaba coronado

Esta KB usaba `chen-friedman/awesome-legaltech` (34★) como índice de referencia. Existe
`Vaquill-AI/awesome-legaltech` (**273★**, activo 2026-10-26), **con el mismo nombre de repo**,
ocho veces más grande y que además cubre servidores MCP — la categoría que más creció este pase.
No es un renombrado: **son dos repos distintos con nombre idéntico**, y el pequeño ganó el puesto
por llegar antes a los resultados de búsqueda.

**Discriminador para no repetirlo:** cuando dos repos comparten nombre, **comparar estrellas y
`pushed_at` antes de citar a uno como «el índice»**. Aquí la decisión no es obvia y se publican
los dos a propósito: Vaquill es más completo pero **no tiene licencia**; chen-friedman es
pequeño pero **CC0**. Para *consultar*, Vaquill. Para *derivar material de cliente*, chen-friedman.

## ⚠️ Nota de licencia AGPL-3.0 — y una corrección al razonamiento publicado

`courtlistener`, `lexnlp` y `mike` son **AGPL-3.0**, verificado leyendo el fichero. AGPL es
copyleft **de red**: si el cliente expone el servicio por red, debe ofrecer el código fuente de la
obra derivada. Para un entregable SaaS propietario esto es normalmente un **bloqueante
contractual**, no un detalle. Alternativas permisivas: **OLDP (MIT)** para corpus-platform,
**ContextGem (Apache-2.0)** y **CaseCite (Apache-2.0)** para extracción y research.

> ⚠️ **Corrección de un razonamiento que esta KB publicó durante 16 días.** `repos/trending.md`
> afirmaba que *«el payload AGPL es prácticamente constante porque no interpola ningún nombre»*,
> y lo apoyaba en estas tres cifras: **35.140 B** (courtlistener), **34.519 B** (lexnlp) y
> **34.523 B** (mike). **Las cifras refutan la afirmación en el mismo renglón:** courtlistener
> difiere de los otros dos en **617 B**. Leído hoy, el motivo es que su fichero **sí lleva un
> preámbulo de copyright antepuesto** (`"This software and any associated files are Copyright
> 2010, Free Law Project."`) sobre el texto AGPL canónico de ~34.523 B.
>
> La licencia era correcta; **el razonamiento y el método no**. Y había un segundo error oculto:
> la KB declaraba haber leído cada licencia desde `.../<rama>/LICENSE`, pero **courtlistener no
> tiene `LICENSE`** — tiene **`LICENSE.txt`**, y `LICENSE` devuelve 404. El procedimiento
> publicado no reproducía el resultado publicado.
>
> **Regla que se deriva (aplicable a cualquier KB de esta rotación):** las licencias tienen
> longitudes canónicas — MIT/Expat 1.050–1.150, Apache-2.0 ~11.358, CC0 ~7.048, MPL-2.0 ~16.700,
> AGPL-3.0 ~34.523, GPL-3.0 ~35.149. Una fila cuyos bytes caen fuera de la banda de su familia
> **está mal clasificada o lleva texto añadido**. La regla es **asimétrica**: bytes *por encima*
> ⇒ preámbulo o licencia compuesta (leer el fichero); bytes *muy por debajo* ⇒ **fichero puntero**
> (seguir el puntero, nunca concluir «sin licencia»). Aplicada hoy a 12 licencias leídas:
> **3 señaladas, 3 explicadas, 0 falsas alarmas** — ver la sección siguiente.

## 🆕 Un modo de fallo de licencia propio de la industria legal: el grant partido código/corpus

Este es el hallazgo metodológico más transferible del pase y **no aparece en ninguna otra KB de la
rotación**, porque es específico de los sectores cuyo entregable incluye un *corpus*:

**En legal, la licencia del repo frecuentemente NO cubre el texto legal que contiene.** Dos casos
detectados hoy, los dos por la regla de bytes:

1. **`lexifina/global-law`** (2.143★, activo hoy) — `LICENSE.md` de **935 B**, muy por debajo de
   los ~7.048 B de CC0 ⇒ señalado como posible puntero. Leído: **es CC0 1.0 en forma corta**, y
   lleva una sección explícita *«What this does not cover»*: la dedicación al dominio público
   cubre el árbol de jurisdicciones, el manifiesto, las herramientas, los tests y la documentación
   — **no la ley**. Cada país vive en su propio repo (`lexifina/<country>-law`) enlazado como
   **submódulo git, con su propio LICENSE y su propio SOURCES.md**. La API, por su parte, reporta
   `NOASSERTION`.
2. **`mhfed/vn-law-check`** (508★) — `LICENSE` de **1.356 B**, ~200 B por encima de la banda MIT
   ⇒ señalado. Leído: **MIT + una nota añadida** que dice que la licencia *«does not and cannot
   license the underlying Vietnamese legal texts»*. (Dato de procedencia: su aviso de copyright
   nombra *"Contributors to vn-web-compliance-audit"*, **un proyecto distinto del nombre del
   repo** — señal de derivación o renombrado, sin confirmar.)

**Consecuencia operativa, y es la que importa para un entregable:** en un engagement legal, decir
«el repo es MIT» **no responde la pregunta que hace el cliente**, que es *¿puedo redistribuir el
corpus?*. Son **dos licencias distintas** y hay que verificar las dos. Es el análogo exacto de la
pregunta de los *pesos del modelo* que la KB de gaming dejó abierta: en ambos casos, **la mitad
del entregable queda fuera de la licencia que se verificó**.

## 🆕 PASE 3 — DOS RESULTADOS DE MÉTODO SOBRE ESTE FICHERO

### 1. El checksum de bytes se corrobora **entre industrias**, lo que lo convierte en una constante
Este fichero publicó bandas canónicas de longitud de licencia (MIT 1.050–1.150, Apache-2.0
~11.358, CC0 ~7.048, AGPL-3.0 ~34.523, GPL-3.0 ~35.149). El pase 3 leyó licencias de repos
**nuevos y no relacionados** y cayeron todas dentro de la banda, al byte en varios casos:

| Repo leído en el pase 3 | Familia declarada | Bytes medidos | Banda | ¿Dentro? |
|---|---|---:|---|---|
| `stella/stella` | Apache-2.0 | 11.358 | ~11.358 | ✅ exacto |
| `JustVugg/judicex` | Apache-2.0 | 11.357 | ~11.358 | ✅ (−1 B, salto de línea final) |
| `FuturixAI…/Prism-Legal-OS` | AGPL-3.0 | **34.523** | ~34.523 | ✅ **exacto** |
| `betagouv/mon-entreprise` | MIT | 1.074 | 1.050–1.150 | ✅ |
| `Lethe044/hermes-legal` | MIT | 1.065 | 1.050–1.150 | ✅ |
| `thunlp/CAIL` | MIT | 1.063 | 1.050–1.150 | ✅ |
| `Paparusi/legal-ai-agent` | MIT | 1.083 | 1.050–1.150 | ✅ |

**El dato fuerte: `Prism-Legal-OS` mide 34.523 B de AGPL-3.0, exactamente el mismo número que la
KB de gaming registró para `grafana` y que esta KB registró para `courtlistener`.** Tres repos sin
relación, tres industrias, un número idéntico ⇒ **la banda no es una heurística de esta KB: es la
longitud del texto canónico de la FSF.** Eso la vuelve utilizable como **checksum**, con un coste
de red nulo adicional (el fichero ya se descarga para leerlo). **7 licencias nuevas señaladas: 0
fuera de banda, 0 falsas alarmas.**

### 2. 🔧 G-L7 — UN SLUG CITADO SIN URL NO PASA POR EL BARRIDO DE URLs
El barrido de verificación de esta KB extrae `github.com/<owner>/<repo>` de los ficheros. **Pero
este fichero y otros citan repos en `código entre comillas` sin enlace**, y esos **no los ve el
barrido**. Extraídos aparte en el pase 3: **28 slugs citados sin URL**, varios de ellos
*portadores de conclusiones*. El caso límite: **`lexifina/global-law`, de la que este fichero
deriva toda la regla del «grant partido código/corpus», no estaba en la lista de URLs
verificadas.** Verificada ahora: **existe, ★2.146 (eran 2.143: creció 3), `pushed_at` hoy** — la
regla se sostiene. Pero **se sostuvo por suerte, no por método.**

Verificados los 28 en el pase 3: **24 existen y se confirman**; `nlpaueb/legal-bert` **no existe
como repo** (la KB ya lo declaraba ABSENT correctamente — es un modelo de HuggingFace, acierto del
pase 2); y los tres `LawLink` se resuelven abajo.

⇒ **Regla: el barrido de verificación extrae `github.com/...` Y ADEMÁS los slugs en backticks con
forma `owner/repo`.** Un slug sin enlace es igual de citable y por tanto igual de falsable; que no
sea clicable no lo exime.

## Por qué estos repos

### La capa de parsing es el cuello de botella real, no el modelo
En legal, el 80% del esfuerzo es convertir un PDF escaneado de 200 páginas en algo con estructura.
**Docling** (MIT, 70.821★) es hoy la entrada por defecto y además es el backend de lectura de
**ContextGem**, lo que hace que esos dos encajen sin pegamento.

### El corpus permisivo es más escaso que el código permisivo
De los cinco repos de datos de arriba, **sólo dos tienen licencia que permita redistribuir**
(OLDP MIT, legal-templates CC0). Dos son AGPL y uno no declara licencia. **En legal, la
restricción suele estar en los datos, no en el software** — al contrario que en la mayoría de
industrias de esta rotación.

### Lo que se mantuvo retirado de este fichero y por qué
La versión de julio listaba **mythril**, **heimdall-rs** y **solgraph** como repos fundacionales
de legal: son herramientas de análisis de bytecode **EVM / smart contracts**, entraron por la
coincidencia léxica de "contract" y no tienen relación con servicios legales. Retirada confirmada.

---
*Ver también: `verticals/solutions.md` para plataformas verticales completas. Verificado 2026-11-20
por doble canal. 16 filas reales, 0 placeholders.*
