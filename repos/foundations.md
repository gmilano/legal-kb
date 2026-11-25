---
industry: legal
region: Global
updated: 2026-11-25
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
| 🆕 [daniel-filius/awesome-mcp-brasil](https://github.com/daniel-filius/awesome-mcp-brasil) | main | **CC0-1.0** (7.048 B) | 🆕 **El primer índice LATAM de esta KB, y el primero que es también un canal de descubrimiento.** Directorio auto-verificado de servidores MCP y agent skills **brasileños**: *Jurídico/Legislativo* **13 entradas** (DataJud/PJe, Câmara…), Dados públicos 24, Fiscal/Tributário 7, Comércio & SaaS BR 17, Pix 8, Eleições/Governo 7, Skills & prompts BR 5, Guias em português 6. **CC0 = dominio público**, el mismo régimen que `chen-friedman` y `General-Legal/legal-templates` (7.048 B exactos, los tres ⇒ banda CC0 confirmada por triplicado). | 0 | n/d ⚠️ |

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


## 🆕 PASE 4 (2026-11-21) — el censo de nombre aplicado a esta misma tabla: eran CINCO, no dos

La corrección de arriba dice: *«No es un renombrado: **son dos repos distintos con nombre
idéntico**»*. Correcto, e **incompleto por el mismo motivo que la procedencia de LawLink**: se
razonó sobre los candidatos que trajo una búsqueda, no sobre un censo. Aplicado el instrumento
nuevo (**P18**):

```
gh api -X GET search/repositories -f q='awesome-legaltech in:name' --jq '.total_count'  →  5
```

| Repo | Licencia | Stars | `pushed_at` | Lectura |
|------|----------|------:|-------------|---------|
| `Vaquill-AI/awesome-legaltech` | **NONE** ⚠️ | 273 | 2026-10-26 | el más grande, no adoptable |
| `chen-friedman/awesome-legaltech` | CC0-1.0 | 34 | 2026-04-06 | limpio, pequeño, **7 meses dormido** |
| 🆕 **`apiotrowski-afk/awesome-legaltech-pl`** | **CC-BY-4.0** (17.023 B) | 14 | **2026-11-20** | **el más activo de los cinco. Ver abajo.** |
| `JSv4/awesome-legaltech` | NONE | 4 | **2022-11-21** 🪦 | 🔴 **VACÍO, no muerto: `size=0`, cero refs en `ls-remote`, `raw` 404.** Creado y nunca empujado (`created_at` y `pushed_at` distan **1 segundo**). **`JSv4` es el owner antiguo de `OpenContracts`.** Ver **G-L9** abajo. |
| `mrtonyirving/awesome-legaltech` | NONE | 0 | 2026-06-29 | ruido |

### 🆕 Activo nuevo: `apiotrowski-afk/awesome-legaltech-pl` — **Polonia**, y es el único índice legal de esta KB que Globant puede derivar

- **Licencia leída: CC-BY-4.0, 17.023 B.** Primera línea: *«Creative Commons Attribution 4.0
  International»*. **Permite uso comercial y obras derivadas con atribución** ⇒ es el **único**
  índice legal de esta KB que se puede *derivar* para material de cliente. Compárese:
  `Vaquill-AI` **sin licencia** (todos los derechos reservados), `lawve-ai/awesome-legal-skills`
  **CC-BY-NC-ND** (ni comercial ni derivados), `chen-friedman` **CC0** (derivable, pero dormido
  desde abril).
- **Contenido — «Prawo w kodzie» (derecho en código):** catálogo de herramientas, datos y modelos
  jurídicos polacos: **APIs del Sejm/ELI, SAOS, CBOSA**, jurisprudencia, **servidores MCP**, skills
  de AI y **anonimización de documentos**. `topics`: `legal-ai`, `legal-tech`, `mcp`, `open-data`,
  `poland`, `polish-law`, `prawo` ⇒ **pasa el gate de pertinencia (P15) por `description` y por
  `topics`.**
- **Jurisdicción nueva en esta KB: Polonia** — hasta hoy la KB sólo tocaba Polonia a través de
  `ContextGem` (que es una herramienta, no una fuente jurídica polaca). Y ahora **EMEA tiene cinco
  jurisdicciones con activo propio**: Alemania, España, Italia, Suiza y **Polonia**.
- 🔑 **Y lo más interesante del repo no es el contenido, es su método:** se declara *«ze skalą
  otwartości i automatyczną kontrolą świeżości»* — **con escala de apertura y control automático de
  frescura**. Es decir: **automatiza exactamente las dos cosas que esta KB hace a mano en cada
  pase** (graduar la licencia y medir si el repo está vivo). ⇒ **Merece una lectura de su
  implementación en el próximo pase**, no como fuente sino como **par metodológico**: si su control
  de frescura funciona, es un patrón adoptable para toda la rotación.

### ⚠️ Corrección a la tabla de bandas del checksum de licencias (932-G1)

La banda heredada para **CC-BY-4.0** es *«~18.650 B»*. Este fichero mide **17.023 B** y es
CC-BY-4.0 **confirmado por lectura de la primera línea**. ⇒ **La banda estaba demasiado estrecha y
habría marcado un falso positivo.** Corregida a **CC-BY-4.0 ≈ 17.000–18.700 B**. Es la primera
corrección a la tabla de bandas desde que se importó, y confirma su propio caveat: **los bytes
MARCAN, la lectura DECIDE.** Propagar la banda corregida a las demás KBs de la rotación.

### 🔴 G-L9 — SIGNATURA DE CANAL NUEVA, DESCUBIERTA EN LA VERIFICACIÓN FINAL DE ESTE PASE: **EL REPOSITORIO VACÍO**

`JSv4/awesome-legaltech` se publicó arriba (antes de la verificación final) como «4 años muerto»,
leyendo su `pushed_at` de 2022. **Es peor que muerto: está vacío, y nunca tuvo contenido.** Medido:

| Canal | `JSv4/awesome-legaltech` | Control (`chen-friedman/awesome-legaltech`) |
|-------|--------------------------|---------------------------------------------|
| API búsqueda | **presente**: 4★, `archived=false`, `disabled=false`, `default_branch=main` | presente |
| **`size`** | **0** | **88** |
| `git ls-remote` (todas las refs) | **exit 0, CERO refs** | exit 0, **33 refs** |
| `raw` cualquier ruta | **404** | 200 |
| `created_at` vs `pushed_at` | **2022-11-21T15:43:19Z vs :20Z — UN SEGUNDO** | separados por meses |

**Es un repo creado desde la web y al que nunca se hizo push.** El `updated_at` de 2026-06-15 es
sólo metadato (alguien le dio una estrella).

> 🔧 **LAS DOS TRAMPAS, Y LAS DOS AFECTAN A INSTRUMENTOS QUE ESTA KB YA USA.**
>
> **1. `pushed_at` miente aquí, y es el campo en el que esta KB más ha confiado.** Reporta un push
> que **no llevó contenido**. Un pase que mida sólo los tres campos de 932-G6
> (★ / `pushed_at` / `archived`) publica *«dormido desde 2022»* — y «dormido» **implica que hay algo
> que revivir o forkear**. No hay nada. ⇒ **Los tres campos no bastan: hace falta `size`**, que
> viene **en el mismo payload** que la KB ya descarga, gratis, y que nadie estaba leyendo. Es el
> mismo error de forma que 932-G1 (los bytes de licencia llevaban meses registrados sin usarse).
>
> **2. `git ls-remote` devuelve EXIT 0.** No es un error: es un éxito con cero refs, así que es
> **invisible a cualquier comprobación de error**. Y el script de **P16** hace
> `if [ -z "$SHA" ]; then ... "NO EXISTE (o es privado)"`, que aquí es **falso en las dos ramas**:
> el repo existe y no es privado. **P16 confunde TRES estados en una rama**: *no existe*, *es
> privado* y *está vacío*. Corregir P16 añadiendo la distinción por conteo de refs + `size`.
>
> **Discriminador, gratis y decisivo: `size == 0` y `created_at == pushed_at` (al segundo).**
> Taxonomía completa de estados que esta KB ya sabe distinguir, ahora con el quinto:
>
> | Estado | API | `size` | refs | `raw` |
> |--------|-----|-------:|-----:|-------|
> | vivo | presente | >0 | >0 | 200 |
> | dormido | presente | >0 | >0 | 200 |
> | **archivado** | presente, `archived=true` | >0 | >0 | 200 |
> | **renombrado** | **422** en el slug viejo | — | >0 (redirección) | **200** |
> | 🆕 **vacío** | **presente**, `archived=false` | **0** | **0** | **404** |
> | borrado | 422 / NOT_FOUND | — | — | 404 |
>
> **Aplicar en todas las industrias de la rotación:** un `size: 0` en una fila publicada es una
> fila que promete un codebase inexistente, y pasa todos los controles actuales menos este.

---

## 🆕 PASE 5 (2026-11-21) — dos activos fundacionales nuevos y una práctica de descarte que hay que revisar

### Activos incorporados

| Repo | Licencia (leída) | Capa | Por qué es fundacional | Stars | Push |
|---|---|---|---|---:|---|
| [AI4CharityPL/kancelaria-lex](https://github.com/AI4CharityPL/kancelaria-lex) | **MIT** (1.069 B) | Expediente local + verificación de cita | **Es la primera implementación de referencia, con licencia permisiva, de las DOS exigencias que esta KB declara no negociables a la vez**: (a) **soberanía del dato impuesta por arquitectura** — 4 segmentos Docker, 3 con `internal: true`, sin ruta a la pasarela, no una promesa de README; y (b) **integridad de cita por construcción** — el código reconstruye el texto desde el documento fuente y compara **carácter a carácter**, de modo que una cita fabricada no sobrevive al verificador. Declara **0 citas inconsistentes con la fuente en todas las corridas** y >80% de precisión, contra el **17–34%** de fabricación medido en herramientas comerciales. | 60 | 2026-08-23 |
| [meta-models/legal-agent-workshop](https://github.com/meta-models/legal-agent-workshop) | **MIT** | Enablement / arquitectura de verificación | **La capa de verificación como código de formación, no como diagrama.** El kit construye el agente y luego **los dos controles que corren FUERA del control del agente** (checklist contra la verdad de base del expediente + reglas del memo), más rechazos, escalado, liberación de evidencia nueva, reanudación y **firma del abogado**. Es el patrón que `compose/patterns.md` describe en P2/P8/P10, en forma ejecutable y con caso de trabajo. | 73 | 2026-11-06 |

### 🧮 Revisión de práctica: `NOASSERTION` **no** es «sin licencia»

Este pase encontró **dos** repos que GitHub clasifica como `NOASSERTION` y que, leídos, son
**perfectamente adoptables**:

| Repo | Bytes de LICENSE | Banda | Lectura real | ¿Adoptable? |
|---|---:|---|---|---|
| [mayan-edms/Mayan-EDMS](https://github.com/mayan-edms/Mayan-EDMS) | **586** | muy por debajo de Apache (11.300–11.400) ⇒ **puntero** | puntero **Apache-2.0** genuino | ✅ sí (⚠️ espejo, 🪦 6 meses sin push) |
| [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | **35.051** | por encima de AGPL (~34.500) ⇒ **compuesta** | **AGPL-3.0** + carve-out de `apps/OpenSignServer/cloud/customRoute` + terceros | ⚠️ sí para despliegue interno; no para SaaS cerrado |

⇒ **Regla, y corrige una práctica de esta KB:** `NOASSERTION` significa «el clasificador de GitHub
no pudo», no «no hay licencia». **Nunca se descarta una fila por `NOASSERTION` sin abrir el
fichero**; los bytes dicen de antemano qué se va a encontrar (puntero por debajo de la banda,
compuesta por encima). El descarte legítimo es **la ausencia del fichero**, que es otra medición:
`raw` devuelve 404 en `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE` y `COPYING`, en `HEAD`,
`main` y `master`.

---

## 🆕 PASE 6 (2026-11-21) — la capa que faltaba no faltaba: **fuentes legales oficiales de LATAM**

Este fichero declaraba desde el pase 1 que *«el corpus permisivo es más escaso que el código
permisivo»* y que para LATAM no había **nada**. La segunda mitad de esa frase es falsa. Cuatro
servidores MCP, todos permisivos, todos sobre **fuentes oficiales de Estado**, licencia leída byte
a byte:

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| 🟢 [matematicsolutions/br-eli-mcp](https://github.com/matematicsolutions/br-eli-mcp) | HEAD | Apache-2.0 (11.358 B) | 🇧🇷 **La base fundacional de la capa.** 8 APIs de datos abiertos **sin clave ni registro**: Câmara (proyectos federales), Congresso (normas promulgadas + **publicación en Diário Oficial** + histórico de enmiendas), `normas.leg.br` (texto a nivel de **artículo**), **DataJud/CNJ** (metadatos procesales, no texto), **STJ** (íntegro + ementas desde may-2022), **CARF** (fiscal federal, sólo por número), **TST** (íntegro, búsqueda libre + número CNJ), **TCU**. Declara citas verificables y **no hace scraping del HTML de Planalto** — es decir, se apoya en API, no en maquetación. | 4 | n/d ⚠️ |
| 🟢 [mazulo/leis-mcp](https://github.com/mazulo/leis-mcp) | HEAD | MIT (1.071 B) | 🇧🇷 **1.218.990 normas** brasileñas (CF, CLT, CDC, Código Civil, LGPD…) citando fuente oficial (`normas.leg.br`, LexML) y emitiendo **avisos de revogação**; valida vigencia contra normas.leg.br y datos abiertos del Senado. ⚠️ Dos límites declarados por el propio README: el texto convertido puede traer errores de conversión/OCR y **no sustituye la publicación en el Diário Oficial**; la búsqueda sin norma concreta sólo cubre lo ya cacheado. Lee de `ctresb/leis`. | **71** | n/d ⚠️ |
| 🟢 [ivancaron/jurismcp](https://github.com/ivancaron/jurismcp) | HEAD | MIT (1.078 B) | 🇧🇷 **La mitad jurisprudencial.** Portales judiciales oficiales: STJ (POST directo), STF y TST (navegador headless), TJES (REST pública), **LexML** (federado, resuelve `urn:lex`), **BNP/CNJ** (`pangeabnp.pdpj.jus.br`, registro de precedentes), TNU y TRF4 (formularios eproc). Marca Jurisprudencias.ai como **agregador de terceros, no portal oficial**, y lo deja opt-in. ⚠️ El headless/scraping es frágil ante rediseños: es la pieza a endurecer. | 2 | n/d ⚠️ |
| 🟢 [BEG-lag/mcp-dof](https://github.com/BEG-lag/mcp-dof) | HEAD | MIT (1.082 B) | 🇲🇽 **El primer activo mexicano de fuentes oficiales de esta KB.** **Diario Oficial de la Federación** sobre la **API oficial SIDOF** (`sidof.segob.gob.mx`): ediciones diarias, texto íntegro de decretos, búsqueda por título, indicadores FIX/UDIS/TIIE. Python 3.12+. ⚠️ **La API oficial no está documentada**: los endpoints (`/notas/{fecha}`, `/notas/nota/{id}`, `/indicadores/...`) se mapearon por sondeo manual ⇒ deuda de mantenimiento real, y a la vez **el patrón reutilizable** para los boletines oficiales de AR/CL/CO/PE. | **0** | n/d ⚠️ |

### Por qué esta capa cambia la propuesta, no sólo la tabla

1. **Pasa de «construir» a «extender».** P12 pedía 4–8 semanas para *el primer* MCP oficial LATAM.
   Ya hay cuatro: el trabajo es endurecer `jurismcp` (headless → API donde exista), ampliar
   cobertura a tribunales estatales y replicar `mcp-dof` en los otros cuatro países.
2. **La pieza de citación defendible ya existe en portugués y castellano.** `leis-mcp` emite
   avisos de revogação y `br-eli-mcp` arrastra la publicación en DOU: es *provenance*, que es
   exactamente lo que la obligación de verificar citas exige en las tres regiones.
3. **El hueco real queda acotado a cuatro países:** **Argentina, Chile, Colombia y Perú**. Es un
   hueco de cuatro jurisdicciones, no de una región — y el de Perú es el más vendible, porque allí
   los *human gates* son **reglamentarios** (Ley 31814 + reglamento vigente 22-ene-2026), no buena
   práctica.

### 🧮 Banda CC0 confirmada por triplicado

`awesome-mcp-brasil` **7.048 B** = `chen-friedman/awesome-legaltech` **7.048 B** =
`General-Legal/legal-templates` **7.048 B**. Tres repos sin relación, idéntico byte a byte ⇒ la
banda CC0-1.0 del checksum 932-G1 es **exacta**, no aproximada. Las bandas MIT (1.062–1.093 B en
7 lecturas) y Apache-2.0 (11.314–11.358 B) tienen dispersión por la línea de copyright; CC0 no la
tiene porque **no lleva titular**. Útil: en CC0, cualquier desvío del 7.048 significa fichero
modificado.


## 🔴 PASE 7 (2026-11-22) — **LA CAPA DE EVALUACIÓN DE ESTA KB ESTABA MAL ATRIBUIDA DESDE EL PRIMER PASE**

Esta KB cita **LegalBench** en tres ficheros (`intel/market.md`, `intel/trends.md`,
`repos/trending.md`) como su base de evaluación en inglés, y los pases 3 y 4 lo registraron en el
histórico de rotación como **«LegalBench (MIT, ~1.8k★, 162 tareas, Stanford)»**.

**No tenía fila. No tenía URL. Y por tanto nunca pasó por el barrido de URLs ni por la lectura de
licencia** — es el modo de fallo `G-L7` que esta misma KB documentó («un slug citado sin URL no
pasa por el barrido»), aplicado al activo del que cuelga todo el argumento de evaluación.

Medido hoy, por los dos canales:

| Afirmación publicada por esta KB | Medición de hoy (2026-11-22) |
|---|---|
| Licencia **MIT** | 🔴 **FALSO.** `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING` → **404 los cinco**. SPDX de la API: **`NOASSERTION`**. |
| `~1.8k★` | 🔴 **663★** medidas |
| `162 tareas` | ✅ **162** — lo único correcto |
| «Stanford» | ⚠️ El repo canónico es **`HazyResearch/legalbench`**; `stanford-crfm/legalbench` da **422** |

### 🧭 G-L15 / CANAL 5 — EN UN REPO DE **DATOS**, LA LICENCIA NO ESTÁ EN EL REPO: ESTÁ **POR ÍTEM**

El `README` de LegalBench no omite la licencia por descuido. **Dice explícitamente dónde está:**

> *«LegalBench is a mix of created and transformed datasets. We ask that you follow the license of
> the dataset creator. Please see the task page for a list of tasks and licenses.»*

Eso **no es una concesión de derechos, es una instrucción de enumerar**. Así que se enumeró: se
leyó la línea `**License**:` de **las 162 tareas**.

| Licencia de la tarea | Tareas | ¿Uso comercial? |
|---|---|---|
| CC BY 4.0 | **124** | ✅ sí, con atribución |
| MIT | 4 | ✅ sí |
| CC BY-SA 4.0 | 2 | ⚠️ sí, pero **share-alike** sobre el derivado |
| CC BY-NC-SA 4.0 | 16 | 🔴 **no** |
| «Creative Commons Attribution-NonCommercial License» | 9 | 🔴 **no** |
| CC BY-NC 4.0 | 4 | 🔴 **no** |
| CC BY-NC 3.0 | 1 | 🔴 **no** |
| Sin línea de licencia | 2 | 🔴 **no** (sin concesión expresa) |

**30 tareas son NonCommercial y 2 no tienen concesión: 32 de 162 (19,8%) no son utilizables en un
entregable comercial.** Las 130 restantes sí.

Las familias NC están **agrupadas por prefijo**, que es lo que hace la exclusión barata y auditable:

```
# Excluir de cualquier corrida que sustente un entregable de cliente (32 tareas):
learned_hands_*            # 16 · CC BY-NC-SA 4.0
opp115_*                   #  9 · CC BY-NC
textualism_tool_*          #  2 · CC BY-NC 4.0
canada_tax_court_outcomes  #  1 · CC BY-NC 4.0
consumer_contracts_qa      #  1 · CC BY-NC 4.0
privacy_policy_entailment  #  1 · CC BY-NC 3.0
abercrombie, rule_qa       #  2 · sin línea de licencia
```

> **Y el propio repo lo anticipó**: incluye `UsingLegalBench.ipynb`, descrito en el README como
> *«an example of how to select tasks based on license information»*. El filtro por licencia **es
> una función del dataset**, no un parche nuestro. Lo que faltaba no era la herramienta: era que
> alguien la usara antes de escribir «MIT» en una KB.

**La regla, para las doce industrias:** cuando la fila es un **dataset o un corpus**, la licencia
tiene una quinta ubicación posible —**dentro del árbol de datos, una por ítem**— y la respuesta a
nivel de repo puede ser legítimamente *«depende de cada ítem»*. Ese `NOASSERTION` **no es un
clasificador que falla**, es la respuesta correcta. Enumerar es obligatorio, y es barato: 162
`curl` a `raw.githubusercontent.com` y un `grep`. Receta ejecutable en `compose/patterns.md`, `P26`.

### ✅ Y la sustitución permisiva existe, la publica el líder comercial, y lleva seis meses fuera

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|---|---|---|---|---|---|
| [harveyai/harvey-labs](https://github.com/harveyai/harvey-labs) | `main` | **MIT (1.067 B)** | 🆕 **Harvey LAB — «Legal Agent Benchmark»: el banco de pruebas de agentes legales que publica Harvey, la empresa de 11.000 M USD contra la que esta KB se posiciona, y lo publica en MIT a nivel de repositorio.** No es sólo un dataset: son **2.010 tareas** sobre **24 áreas de práctica + contratación in-house** (instrucciones, documentos y **rúbricas**) **más un harness de ejecución** con adaptadores de modelo (Anthropic, OpenAI, Google, Meta, xAI, Mistral opcional), *sandbox*, *grader* por rúbrica con juez LLM, informes y *sweeps*. Se instala como librería (`lab-core`, wheel por release). | **1.668** | **2026-11-12** |
| [HazyResearch/legalbench](https://github.com/HazyResearch/legalbench) | `main` | 🔴 **NOASSERTION — y es correcto**: sin fichero de licencia (5/5 → 404). Licencia **por tarea**: 124 CC BY 4.0 · 4 MIT · 2 CC BY-SA · **30 NC** · 2 sin concesión | Benchmark de razonamiento jurídico en modelos fundacionales, **162 tareas**. Sigue siendo la referencia académica de la industria y se mantiene en esta KB **como corpus**, pero **sólo utilizable sobre el subconjunto de 130 tareas filtrado por licencia** (ver arriba). **No es MIT y nunca lo fue.** | 663 | 2026-03-30 |

### 🔗 Cierre de dependencias aplicado a `harvey-labs` (regla de la KB de *gaming*, `channel 4`)

Se resolvió cada dependencia que el repo declara, porque un proyecto no es más libre que la menos
libre de las que te manda instalar:

- **`pyproject.toml`** — 12 dependencias declaradas, **todas permisivas**: `pdfplumber`,
  `markitdown`, `openpyxl`, `python-pptx` (MIT), `httpx`, `pandas`, `seaborn` (BSD), `anthropic`,
  `openai`, `google-genai` (MIT/Apache-2.0), `matplotlib` (PSF-like), `mistralai` (opcional).
- **🟡 Y una que no está en `pyproject.toml`**: el README exige la **CLI `pandoc` ≥ 3.5** para
  puntuar salidas `.docx`. **`jgm/pandoc` es GPL-2.0.** Declarada **sólo en prosa y en un
  comentario**, exactamente la signatura que predice la regla.
- **Y aquí la distinción que importa, porque cambia la conclusión:** `lab_core/sandbox/install_pandoc.sh`
  **descarga** el binario de pandoc 3.11 desde el release oficial (con verificación SHA-256) y lo
  instala en `/usr/local/bin` **en tiempo de instalación**. El repositorio **no redistribuye código
  GPL**, así que `harvey-labs` es MIT limpio. ⚠️ **Lo que sí redistribuye GPL-2.0 es la imagen de
  contenedor que Globant construya con pandoc dentro**, y esa imagen arrastra la obligación de
  oferta de fuentes. Mitigación trivial: pandoc sólo hace falta para puntuar `.docx`; una corrida
  que evalúe texto o `.xlsx`/`.pptx` no lo carga.
- ⚖️ **Sesgo declarado, y hay que decirlo al cliente:** `LawNext` (mayo-2026) observó que LAB es
  *«un benchmark construido por un participante del mercado»* — las tareas y las rúbricas definen
  «buen trabajo legal» según el equipo de Harvey. Se usa como **banco común de comparación**, no
  como definición neutral de calidad. Por eso **conviven** en esta KB con `legalbench` (académico,
  filtrado) y `thunlp/CAIL` (chino): tres definiciones de la tarea, no una.

> 📈 **Y la curva de tamaño es medible, lo que la vuelve un indicador y no una anécdota:**
> **>1.200** tareas al lanzamiento (mayo-2026) → **1.749** (leaderboard de Mercor) → **2.010** hoy.
> Un benchmark que crece un 67% en seis meses es un **compromiso sostenido**, no un lanzamiento de
> marketing. Esta KB lo había perdido durante **seis pases**: se publicó en mayo y nadie lo citó.

---

## 🆕 PASE 8 (2026-11-22) — **LA CAPA DE ESTÁNDARES DEL NEGOCIO JURÍDICO**, y una de las tres es MIT

Esta KB tenía la capa de **corpus** (jurisprudencia, legislación, benchmarks) y la capa de
**parsing**. No tenía la capa de **estándares de datos del negocio**: los formatos y taxonomías con
los que un despacho y su cliente intercambian expedientes y facturas. Son tres, y su estado de
apertura es radicalmente distinto:

| Estándar | Qué normaliza | Quién lo mantiene | Estado open source, medido 2026-11-22 |
|---|---|---|---|
| **SALI LMSS** | **Taxonomía de materia**: área de derecho, tipo de asunto, industria, rol, >18.000 etiquetas con IRI única | SALI Alliance™ | ✅ **MIT, en GitHub, 92★** — ver fila abajo |
| **LEDES 1998B** | **Factura legal**: ASCII delimitado por `\|`, 24 campos | LEDES Oversight Committee | ⚠️ Especificación abierta, **implementaciones casi inexistentes**: `total_count=6` para `LEDES legal billing`. Documentación del formato revisada por última vez en 2014 |
| **UTBMS** | **Códigos de tarea y actividad** que lleva cada línea de la factura | UTBMS / ABA‑ACCA | 🔴 **`total_count = 0`**. El codelist que valida toda factura legal **no tiene ninguna implementación open source**. `billing-lint` valida contra él, pero embebe su propia copia |

> 🔑 **La lectura que importa:** los tres son estándares *abiertos* y sólo uno es *software* abierto.
> Esta KB venía midiendo la apertura de **repos**; aquí la unidad que decide si un entregable es
> interoperable es el **estándar**, y un estándar puede estar publicado y aun así no tener con qué
> ejecutarlo. **Especificación abierta ≠ implementación disponible**, y la distancia entre las dos
> es exactamente el trabajo que se factura.

### Activo fundacional nuevo

| Repo | Licencia (leída) | Región | Qué aporta | Stars | Último commit |
|---|---|---|---|---|---|
| [sali-legal/LMSS](https://github.com/sali-legal/LMSS) | **MIT (1.073 B, © 2022 SALI Alliance™)** | Global | **La ontología de materia del sector, en abierto y permisiva.** `LMSS.owl`, XML/OWL, **más de 18.000 etiquetas**, cada una con su IRI. Esos mismos IRI son los identificadores del **SALI API standard** (`sali-legal/api`, `SALI_API.yml`), de modo que es a la vez taxonomía y contrato de interfaz. 31 refs. | 92 | 2026-03-10 |

**Por qué entra en `foundations` y no en `agents`:** no hace nada por sí sola. Es la pieza que hace
que *expediente*, *factura*, *panel de despachos* y *analítica de gasto* hablen del mismo asunto —
el equivalente funcional a lo que un esquema de códigos es en salud o en finanzas. Sin ella, cada
integración de facturación legal reinventa su propia tabla de materias y **ninguna cruza con la del
cliente**. Con ella, el eje por el que se agrega el gasto legal es un identificador estable y
público, y eso es precondición de cualquier analítica vendible.

### 🧮 Confirmaciones del checksum de licencias (932-G1) en este pase — 11 lecturas, 11 aciertos de banda

- **Banda MIT (≈1.056–1.084 B), 7 lecturas:** `sali-legal/LMSS` 1.073 · `billcheck` 1.080 ·
  `aderant-legal-billing` 1.071 · `billing-lint` 1.070 · `claude-court-deadline-reasoning` 1.067 ·
  `mycase-mcp` 1.065 · `lawyered-matter-tracker` 1.056 B.
- **Banda Apache-2.0 (≈11.284–11.454 B), 3 lecturas:** `killbill` 11.357 · `FOSSBilling` 11.454 ·
  `OpenLawOffice` 11.350 B (`LICENSE.txt`, con BOM inicial).
- **Banda AGPL-3.0, 3 lecturas y el dato más limpio del pase:** `kimai`, `deedbox-app` y
  `legal-deadline-calculator` miden **34.523 B exactos, los tres**, en repos sin relación entre sí.
  La banda AGPL no es un intervalo: es **una constante**, porque nadie edita ese texto.

### 🔁 `NOASSERTION` — tercera confirmación consecutiva, y el modo de fallo es nuevo

`InvoicePlane/InvoicePlane` (3.290★): GitHub dice `NOASSERTION`. La regla asimétrica de bandas
predijo **composite** antes de abrir el fichero (5.087 B, muy por encima de la banda MIT). Al
leerlo, la causa es específica y no estaba catalogada: **el fichero abre con un aviso de marca**
—restricciones de uso del nombre y el logotipo «InvoicePlane»— y sólo después, bajo el encabezado
`License for InvoicePlane`, viene el texto **MIT íntegro** (© 2012‑2014 InvoicePlane.com).

> **Modo de fallo: el clasificador lee el principio del fichero.** Un `LICENSE` que antepone marca,
> atribución o aviso de terceros al texto de la licencia se clasifica como `NOASSERTION` **aunque la
> concesión sea impecable**. Las restricciones de marca **no son restricciones de código**: no se
> puede redistribuir *bajo el nombre* InvoicePlane, y se puede hacer todo lo demás que MIT permite.
> Tercer pase consecutivo en que `NOASSERTION` resulta ser una licencia utilizable.

---

## 🆕 PASE 9 (2026-11-25) — **la capa de conformidad de firma**, y es la que tiene los mejores activos permisivos de toda la KB

Esta KB tenía el **producto** de firma electrónica (`OpenSign`, AGPL-3.0 compuesta) y no tenía la
capa de **conformidad**: la que decide si una firma es válida ante un tribunal europeo. Censo previo:
`PAdES` **0 menciones**, `eIDAS` **0 menciones**, `pyHanko` **0 menciones**. Los dos activos que
siguen son, por estrellas, licencia y madurez, **de los más fuertes que esta KB ha incorporado**.

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [MatthiasValvekens/pyHanko](https://github.com/MatthiasValvekens/pyHanko) | HEAD | **MIT (1.080 B)** | **El mejor activo de este pase y uno de los mejores de la KB: firma y sellado de PDF en Python, con los perfiles avanzados (PAdES) que la UE exige para la firma cualificada.** Firma, sella, estampa, **y valida**. 121 forks, creado 2020-08-06, **commit de hace dos días**: seis años de continuidad. MIT íntegro ⇒ Globant puede empotrarlo en un entregable cerrado. **Es el cimiento permisivo de cualquier flujo de firma legal, y la KB no lo tenía.** | **807** | 2026-11-23 |
| [esig/dss](https://github.com/esig/dss) | HEAD | LGPL-2.1 (26.530 B) | **La implementación de referencia de la propia Comisión Europea.** El README lo declara: *«This is the official repository for project DSS»*, alojado en los Digital Building Blocks de la CE y publicado en Maven Central bajo el grupo **`eu.europa.ec.joinup.sd-dss`**. Crea, extiende y **valida** firmas electrónicas avanzadas (PAdES, XAdES, CAdES, ASiC) contra las listas de confianza de la UE. 417 forks, Java. ⚠️ **LGPL-2.1: copyleft DÉBIL** — se puede enlazar como biblioteca desde un producto cerrado; lo que debe permanecer libre son las modificaciones **a DSS mismo**. Para un entregable comercial es la diferencia entre viable e inviable, y es **la única autoridad normativa** de esta capa. | **1.051** | 2026-11-04 |

> 🔑 **Por qué esta capa importa más de lo que parece, y es un argumento de venta en EMEA:** el
> entregable de un flujo legal automatizado casi siempre termina en **un documento firmado**. Si la
> firma no es válida, nada de lo anterior cuenta. Y en la UE la validez no es una opinión: es un
> perfil técnico (PAdES) contra una lista de confianza. **`pyHanko` lo produce y `esig/dss` lo
> valida con la autoridad del regulador** — y las dos licencias permiten construir producto encima.

## 🆕 PASE 9 — soporte de litigio: los artefactos que el plano de e-discovery sí tiene

El pase 2 cerró «e-discovery» con un activo. Estos son los artefactos **dentro** del plano, que
nunca se consultaron (ver `G-L18` en `agents/top.md`):

| Repo | Rama | Licencia (leída) | Descripción | Stars | Último commit |
|------|------|------------------|-------------|-------|---------------|
| [frisk55frisk/loadfile-tool](https://github.com/frisk55frisk/loadfile-tool) | HEAD | **MIT (1.078 B)** | **El único activo permisivo de la categoría de *load file*, y es la pieza de interoperabilidad del e-discovery.** CLI que **valida, convierte e inspecciona** `Concordance DAT`, `OPT`, `LFP` y `DII` — los formatos con los que las plataformas de revisión se intercambian producciones documentales. Sin esto, mover una producción entre proveedores es trabajo manual facturable. ⚠️ **0★, 2 refs, creado 2026-03-31**: la categoría es nueva y el activo es un cimiento, no un producto. **Y 0★ es exactamente por qué ningún filtro por estrellas lo encontraría nunca** (`G-L10`). | 0 | 2026-03-31 |
| [wikkiewikkie/Marisol](https://github.com/wikkiewikkie/Marisol) | HEAD | **MIT (1.075 B)** | Biblioteca Python para **numeración Bates, estampado de texto y redacción** de PDF: las tres operaciones que convierten un documento en **prueba producible**. La numeración Bates es el identificador único por página con el que todo litigio estadounidense cita documentos. ⚠️ **Dormante: sin commits desde 2023-08-28** (16 refs, 4 forks). Se publica **como referencia de API y punto de partida para forkear**, no como dependencia viva — y por la regla `G-L14` de esta KB, dormancia y utilidad son ejes distintos. | 18 | 2023-08-28 |

> ⚠️ **Lectura honesta de esta tabla:** son **dos** filas, no cinco. La capa de artefactos de
> e-discovery **existe** y era invisible para esta KB, pero es **joven y poco poblada en lo
> permisivo**: lo maduro de este plano es copyleft (`raiopdf` GPL-3.0, `legion-pdf` AGPL-3.0,
> `doc_redaction` AGPL-3.0) o propietario (Relativity, Everlaw, Reveal). **Menos filas reales que
> rellenas.**

## 🆕 PASE 9 — **T29: la puerta de salida de la matriz T28, y es la *capa de estándares***

El pase 8 publicó `T28`: de las tres propiedades **{específico del sector, maduro, permisivo}** se
pueden tener **dos**, nunca las tres. Este pase encontró el contraejemplo, y tiene una causa
estructural que lo convierte en regla y no en excepción:

| Activo | Específico | Maduro | Permisivo | ¿Qué es? |
|---|---|---|---|---|
| `pyHanko` | ✅ del **artefacto** (PDF firmado PAdES) | ✅ 6 años, 807★, 121 forks | ✅ MIT | implementación de **estándar** |
| `esig/dss` | ✅ del **artefacto** (firma UE) | ✅ 11 años, 1.051★, 417 forks | 🟡 LGPL débil | implementación de **estándar** |
| `loadfile-tool` | ✅ del **artefacto** (Concordance DAT) | ❌ 8 meses | ✅ MIT | implementación de **estándar** |
| `billcheck` (pase 8) | ✅ del **artefacto** (LEDES 1998B) | ❌ 6 días al hallarse | ✅ MIT | implementación de **estándar** |

> 🔑 **La causa:** una implementación de estándar se publica permisiva **porque su valor es la
> interoperabilidad, no el flujo de trabajo**. Quien implementa PAdES o LEDES quiere que todo el
> mundo lo use; quien construye un despacho entero quiere capturarlo, y elige AGPL. **Por eso el
> plano de estándares escapa a `T28` y el plano de producto no.**
>
> **Regla de arquitectura, y aplica a las doce industrias:** *adoptar la implementación del
> **estándar**, construir el **flujo**.* No forkear el producto copyleft del sector —que es la
> opción que parece ahorrar trabajo y cierra la puerta al entregable comercial— sino montar la
> semántica propia sobre el parser/validador permisivo del formato. Comprobar en las otras once:
> `HL7`/`FHIR` (salud), `ISO 20022` (financiero), `IEC 61850`/`CIM` (energía), `OpenTravel`/`NDC`
> (viajes), `GS1`/`EDIFACT` (retail).

---

## 🆕 PASE 10 (2026-11-25) — **la norma como dato**: Akoma Ntoso, ELI/CELLAR y la ley como código

La capa que esta KB no tenía en ningún fichero: **el texto normativo mismo**, estructurado,
versionado y citable. Censo de entrada: `Akoma Ntoso` 0 · `legislative` 0 · `bill tracking` 0 ·
`parliament` 0 · `regulatory change` 0 · `obligations register` 0 ocurrencias en 7.429 líneas.

### El estándar y su tooling — y aquí **lo permisivo es la excepción**

| Repo | Licencia (leída) | Lenguaje / rol | Descripción | ★ | Último commit |
|---|---|---|---|---|---|
| [oasis-open/legaldocml-akomantoso](https://github.com/oasis-open/legaldocml-akomantoso) | **CC-BY-2.0 (12.545 B)** | XSD normativo | El esquema OASIS LegalDocML. ⚠️ **Documento con licencia Creative Commons, no código**: se implementa, no se enlaza | 87 | 2022-06-02 |
| [laws-africa/bluebell](https://github.com/laws-africa/bluebell) | GPL-3.0 (35.149 B) | Python · parser | Parser AN3 genérico (`act`, `bill`, `debate`, `doc`); garantiza salida **estructuralmente válida** con cualquier entrada | 23 | 2026-07-13 |
| [laws-africa/cobalt](https://github.com/laws-africa/cobalt) | LGPL-3.0 (*stub* 633 B) | Python · lib | Lectura/validación AN 3.0 (esquema estricto o relajado) operando sobre el XML | 29 | 2026-06-18 |
| [laws-africa/slaw](https://github.com/laws-africa/slaw) | **MIT (1.067 B)** | Ruby · parser | ⚠️ **ARCHIVADO** 2022-06-28. **El único permisivo del stack**: referencia de API y base de fork | 28 | 2022-06-28 |
| [bungenix/akomantoso-lib](https://github.com/bungenix/akomantoso-lib) | Apache-2.0 (10.358 B) | Java · JAXB | *Binding* Java generado desde el XSD AN 3.0. ⚠️ **dormante 9,4 años** | 15 | 2017-06-29 |
| [TBI-AI-Incubator/codify](https://github.com/TBI-AI-Incubator/codify) | **Apache-2.0 (11.358 B)** | Python ≥3.12 | PDF/texto/XML → Akoma Ntoso: adquisición, transcripción, **estructuración por anclas**, recuperación y comparación. Commit **de hoy**, creado 2026-09-18 | 15 | 2026-11-25 |

> ⚠️ **`cobalt` e `indigo` traen un `LICENSE` de 633 B que NO es la licencia:** es un *stub* de
> remisión («this program is free software… under the terms of the GNU Lesser General Public…»).
> El texto íntegro de la LGPL no está en esa ruta. `search/repositories` devuelve `NOASSERTION`
> para los dos, **y el clasificador tiene razón**: el fichero no contiene una licencia completa.
> Para un entregable comercial eso no es «sin licencia», es **LGPL declarada sin texto adjunto** —
> hay que resolverlo con el mantenedor antes de enlazar.

### Ley como código — y el mejor activo permisivo específico de toda esta KB

| Repo | Licencia (leída) | Descripción | ★ | Forks | Último commit |
|---|---|---|---|---|---|
| [CatalaLang/catala](https://github.com/CatalaLang/catala) | **Apache-2.0 (11.358 B)** | **Lenguaje para especificar legislación** en *literate programming*: el código se anota contra el texto legal línea a línea, y su *default logic* expresa **la excepción** —la forma nativa de la norma jurídica—. Origen de investigación (INRIA) | **2.453** | 124 | 2026-11-23 |
| [openfisca/openfisca-core](https://github.com/openfisca/openfisca-core) | AGPL-3.0 (34.523 B) | Motor Python que ejecuta legislación socio-fiscal como código. Catalogado en el **EU OSS Catalogue**. 12 años | 252 | 100 | 2026-11-24 |
| [PolicyEngine/policyengine-us](https://github.com/PolicyEngine/policyengine-us) | AGPL-3.0 (**34.519 B**) | Modelo estadounidense sobre OpenFisca | 178 | 224 | 2026-11-24 |
| [BetterRules/openfisca-aotearoa](https://github.com/BetterRules/openfisca-aotearoa) | AGPL-3.0 (**34.519 B**) | **Legislación de Nueva Zelanda como código** — la referencia *rules as code* de APAC. ⚠️ dormante desde 2025-03-13 | 45 | 23 | 2025-03-13 |
| [openfisca/country-template](https://github.com/openfisca/country-template) | AGPL-3.0 (declarada; **sin fichero en 6 rutas**) | La plantilla para **crear el modelo de un país nuevo**. Es el punto de partida del hueco LATAM de abajo | 44 | 20 | 2026-11-23 |

> 🔴 **Aviso AGPL-3.0 — y aquí muerde más que en otras capas.** Las cuatro filas de OpenFisca son
> **copyleft de red**: si el motor de reglas se expone como servicio al cliente, la obligación de
> fuente alcanza al servicio. **Catala (Apache-2.0) es la única base de esta capa empotrable en un
> entregable cerrado**, y además es la más madura. Es una coincidencia afortunada y poco frecuente
> en esta KB: ver `T33` en `repos/trending.md` para la causa.

### Corpus legislativo abierto — por región, y con la licencia del *dato* separada de la del *código*

| Repo | Licencia (leída) | Región | Qué contiene | ★ |
|---|---|---|---|---|
| [unitedstates/congress](https://github.com/unitedstates/congress) | **CC0-1.0 (7.048 B)** | North America | Congreso federal 🇺🇸. **CC0 = dominio público sin atribución exigible** | 1.071 |
| [openstates/people](https://github.com/openstates/people) | **CC0-1.0 (7.048 B)** | North America | Legisladores y cargos de los 50 estados, **en CC0 aunque el código del scraper sea GPL-3.0** | 162 |
| [usgpo/bulk-data](https://github.com/usgpo/bulk-data) | 🔴 **SIN LICENCIA** (6 × 404) | North America | Volcados del **GPO**. 387★ sin fichero de licencia: obra del gobierno de EE. UU. es presunción jurídica, **no un grant escrito** | 387 |
| [SenatoDellaRepubblica/AkomaNtosoBulkData](https://github.com/SenatoDellaRepubblica/AkomaNtosoBulkData) | CC-BY-4.0 (declarada; **sin fichero en 6 rutas**) | EMEA · Italia | **Akoma Ntoso oficial del Senado italiano.** Repo de 2016 con commit **de hoy**: el corpus AN oficial más longevo y más vivo | 42 |
| [maastrichtlawtech/cellar-extractor](https://github.com/maastrichtlawtech/cellar-extractor) | Apache-2.0 (11.357 B) | EMEA · UE | Metadatos de jurisprudencia de **CELLAR** por SPARQL, enriquecidos | 8 |
| [seljaseppala/eu_corpus_compiler](https://github.com/seljaseppala/eu_corpus_compiler) | GPL-3.0 (35.149 B) | EMEA · UE | IDs de CELLAR por SPARQL + descarga XML/HTML. ⚠️ dormante 2021-12-03 | 19 |
| [step21/eurlex](https://github.com/step21/eurlex) | AGPL-3.0 (34.523 B) | EMEA · UE | Cliente Python de Cellar (deriva del paquete R `eurlex`) | 14 |
| [lexml/lexml-parser-projeto-lei](https://github.com/lexml/lexml-parser-projeto-lei) | GPL-2.0 (**18.033 B**) | LATAM · Brasil | **Parser oficial del Senado Federal** de proyectos de ley. Repo de 2013 con commit de hace 8 días | 20 |
| [silegis-mg/editor-articulacao](https://github.com/silegis-mg/editor-articulacao) | LGPL-3.0 (`COPYING` = GPL-3.0) | LATAM · Brasil | Editor de articulación de la **Asamblea Legislativa de Minas Gerais** | 18 |
| [CodeandoGuadalajara/dof-rag](https://github.com/CodeandoGuadalajara/dof-rag) | **MIT (1.077 B)** | LATAM · México | RAG sobre el **Diario Oficial de la Federación** | 25 |
| [cchew/lex-au](https://github.com/cchew/lex-au) | **MIT (1.067 B)** | APAC · Australia | Legislación federal australiana estructurada | 6 |

> 🔑 **El patrón de licencia de esta capa, y es útil:** en **tres** casos independientes
> (`openstates`, `unitedstates`, Senado italiano) **el dato se publica más permisivo que el
> código** — CC0 o CC-BY frente a GPL-3.0. ⇒ **El corpus legislativo abierto es, en general,
> adoptable aunque su tooling no lo sea.** Es la inversión exacta del «grant partido
> código/corpus» que esta KB documentó en el pase 3, donde el código era permisivo y el corpus
> CC-BY-NC-ND. **Las dos mitades hay que leerlas siempre por separado, en los dos sentidos.**

### 🔴 El hueco **real** de esta capa, medido y explicado: no hay un solo modelo *rules as code* de LATAM

| Consulta | `total_count` |
|---|---|
| `openfisca brasil` | **0** |
| `openfisca mexico` | **0** |
| `openfisca colombia` | **0** |
| `openfisca chile` | **0** |
| `legislacion como codigo` | **0** |
| `rules as code latam` | **0** |

Seis consultas, **cero resultados**. Existen modelos de país para Francia, EE. UU., Nueva Zelanda y
Senegal; **ninguno de ningún país de América Latina.** A diferencia del hueco de los pases 6 y 8,
**este no es un artefacto del vocabulario**: se consultó también en español (`legislacion como
codigo`) y con el nombre del motor, y sigue en cero. Y la causa no es técnica —el motor es agnóstico
y `openfisca/country-template` existe precisamente para arrancar un país nuevo— sino de **ausencia
de proyecto**: en Francia es un *commun numérique* mantenido con apoyo estatal, y en LATAM no hay
equivalente institucional que lo sostenga.

⚠️ **Y el aviso que lo acompaña, porque la oportunidad es más estrecha de lo que parece:** el motor
es **AGPL-3.0**, así que un modelo de país construido sobre él hereda copyleft de red. Un `openfisca-mx`
o `openfisca-br` es una **contribución a un bien común y una carta de presentación regional** —no un
activo propietario—. El entregable comercial se construye encima con **Catala (Apache-2.0)** o con
una reimplementación del motor. Receta en `compose/patterns.md` (`P38`).
