---
industry: legal
region: Global
updated: 2026-11-25
---

# 📈 Repos trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. Este fichero cubre **repos e infraestructura**; los agentes van en `agents/trending.md`.

## 🆕 2026-11-25 (pase 12) — la propiedad industrial: **una organización MIT entera**, y la regla de bandas de licencia se cae

El activo estructural del pase no es un repo: es **`patent-dev`**, una organización que publica
clientes Go **MIT** para las oficinas de patentes, y que estaba fuera del alcance de las 21
consultas previas de esta KB porque ninguna contenía la palabra «patent».

### Infraestructura añadida este pase — el espinazo permisivo del plano

| Repo | Licencia (leída) | Región | Qué cubre | ★ | Creado / último commit |
|---|---|---|---|---|---|
| [patent-dev/uspto-odp](https://github.com/patent-dev/uspto-odp) | MIT (1.102 B) | North America | Cliente Go completo del **USPTO Open Data Portal** | 18 | 2026-03-28 / **2026-11-25** |
| [patent-dev/bulk-file-loader](https://github.com/patent-dev/bulk-file-loader) | MIT (1.103 B) | Global | Descarga y gestión de **ficheros masivos** de patentes | 17 | 2025-02-12 / 2026-11-10 |
| [patent-dev/kind-codes](https://github.com/patent-dev/kind-codes) | MIT (1.067 B) | Global | **Códigos *kind* con su significado y su línea temporal.** Dataset de referencia, no librería | 11 | 2024-11-08 / 2024-11-08 |
| [patent-dev/epo-ops](https://github.com/patent-dev/epo-ops) | MIT (1.102 B) | EMEA | Cliente Go de **EPO Open Patent Services** | 10 | 2025-10-23 / **2026-11-25** |
| [patent-dev/epo-bdds](https://github.com/patent-dev/epo-bdds) | MIT (1.102 B) | EMEA | **EPO Bulk Data Distribution** — la vía de *backfill* histórico | 5 | 2025-10-23 / 2026-11-08 |
| [patent-dev/dpma-connect-plus](https://github.com/patent-dev/dpma-connect-plus) | MIT (1.103 B) | EMEA (Alemania) | **DPMA Connect Plus**, registro alemán | 2 | 2025-10-23 / **2026-11-25** |
| [PatentsView/PatentsView-API](https://github.com/PatentsView/PatentsView-API) | BSD-2-Clause (1.293 B) | North America | API del dataset **PatentsView**, financiado por el USPTO | 19 | 2014-09-04 / 2026-04-18 |
| [ropensci/patentsview](https://github.com/ropensci/patentsview) | **MIT vía `DESCRIPTION`** (`LICENSE` = 47 B) | North America | Cliente R de PatentsView, de rOpenSci. Ver `T-P12-7` | 39 | 2017-02-17 / 2026-11-24 |
| [pqaidevteam/pqai](https://github.com/pqaidevteam/pqai) | MIT (1.117 B) | Global | Motor de búsqueda de **estado de la técnica** | 140 | 2020-01-22 / 2026-10-21 |

### 🧮 `T-P12-6` — **la regla de bandas de bytes (932-G1) falla en la mitad de las lecturas y queda degradada a triaje**

Esta KB publicó durante once pases que el tamaño del fichero `LICENSE` identifica la licencia, con
bandas estrechas, y el pase 8 llegó a declarar la banda AGPL **«una constante, no un intervalo:
34.523 B exactos»**. Las **40 lecturas de hoy la refutan en tres sitios distintos**:

| Licencia | Banda publicada | **Medido hoy** | Veredicto |
|---|---|---|---|
| MIT | 1.056–1.090 B | **1.062–1.117 B** (18 lecturas) | `pqai` 1.117 B y los cuatro `patent-dev` 1.102–1.103 B **caen fuera por arriba**. La banda habría marcado cinco MIT limpias como «compuestas» |
| Apache-2.0 | 11.350–11.454 B | **10.173–11.358 B** (5 lecturas) | `python-epo-ops-client` mide **10.173 B** porque su fichero **termina en `END OF TERMS AND CONDITIONS`: no lleva el APPENDIX**. Verificado leyendo la cola |
| AGPL-3.0 | **34.523 B «exactos»** | **34.520 B** en `patzilla` | **La «constante» no lo es.** Tres bytes, pero la afirmación publicada era de igualdad exacta |
| GPL-3.0 | sin banda previa | **35.131 B** (`phpip`) | Banda nueva |
| MIT-0 | sin banda previa | **905 B** (`kipris-cli`) | Banda nueva. *MIT No Attribution* |
| BSD-2-Clause | sin banda previa | **1.293 B** (`PatentsView-API`) | Banda nueva |

**Qué sobrevive de la regla:** el tamaño es un **indicio de triaje** útil para ordenar el trabajo, y
nada más. La evidencia es la **primera línea del fichero**. El error de fondo fue de muestra: las
bandas se derivaron de repos de un mismo nicho, donde todo el mundo copia el `LICENSE` del mismo
sitio, y se publicaron como si fueran propiedades del texto de la licencia.

### 🔴 `T-P12-7` — dos modos de fallo del clasificador de licencias, **en direcciones opuestas**, y el peligroso es el segundo

**(a) El `LICENSE` que es un puntero — y afecta a un ecosistema entero.**
`ropensci/patentsview` tiene un `LICENSE` de **47 bytes** cuyo contenido completo es:

```
YEAR: 2021
COPYRIGHT HOLDER: Christopher Baker
```

GitHub lo clasifica **`NOASSERTION`**. La concesión real está en el manifiesto:
`DESCRIPTION` dice `License: MIT + file LICENSE`. **Es la convención de CRAN**, así que
*todo paquete de R en GitHub se lee mal por este camino*, y una auditoría por bandas de bytes lo
puntúa como «47 B = nada», que es el error máximo posible. **Regla general, aplicable a las doce
industrias: cuando `LICENSE` falta o es un sello, la concesión está en el manifiesto del
empaquetador** — `DESCRIPTION` en R, `pyproject.toml`/`setup.cfg` en Python, `package.json` en Node,
`Cargo.toml` en Rust.

**(b) El clasificador que afirma una licencia que ningún fichero respalda.**
`cantab/patentscope` (18★) aparece en `search/repositories` como **MIT**. Comprobadas **siete** rutas
en `raw.githubusercontent.com` —`LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING`,
`mit-license.txt`, `license.md`— todas **404**; y tampoco hay manifiesto (`pyproject.toml`,
`setup.py`, `package.json`: 404 los tres). Solo `README.md` responde 200, luego `HEAD` resuelve
bien y la ausencia es real.

Los once pases anteriores solo habían cazado el fallo en la dirección *inocua* (API dice
`NOASSERTION`, el fichero dice MIT: se pierde un activo bueno). **Este es el inverso y es el
peligroso, porque se lee como luz verde**: el campo de la API dice «permisivo» y no hay texto que lo
sostenga. Queda **nombrado y no tabulado**, según la regla del pase 6.

### 🧾 Un error propio, detectado antes de publicar

Mi detector de licencias marcó `PatentsView/PatentsView-API` como **ISC** contra el `BSD-2-Clause`
de la API, y estuve a punto de publicar una «discrepancia del clasificador». No existía: el patrón
`ISC` sin límite de palabra estaba casando dentro de **«d·isc·laimer»**, palabra que aparece en toda
licencia BSD. GitHub tenía razón. **Cualquier detector de licencias por `grep` necesita `\b`**, y el
fallo es silencioso porque produce un nombre de licencia plausible.

### 🗑️ Clases de descarte medidas en este plano

- **`DURY-LEGAL/*`** — cuatro repos (`euipo-trademark-application`, `ip-portfolio`,
  `madrid-protocol`, `wipo-trademark`), **0★, sin licencia, los cuatro con fecha 2026-05-03**: son
  documentos de un despacho, no software. Patrón reconocible y descartable en bloque.
- **`pipeworx-io`** — **2.109 repositorios** MCP generados en serie, de 1–11★. `mcp-euipo` (MIT
  1.070 B) y `mcp-usitc-edis` (MIT 1.070 B) son reales y del plano, pero son *inventario*, no
  proyectos curados: se nombran, no se celebran.
- **Raspadores de Espacenet** — seis encontrados (`Scrapy_Espacenet`, `espacenet-scraper`,
  `Espacenet_Patents_Search`, `despacenet`…), **todos de 0–1★ y sin licencia**. Hay dos clientes MIT
  de la API oficial: raspar no tiene justificación técnica ni jurídica.

### 🔌 Estado de los canales — remedido hoy (se reescribe porque cambia entre sesiones)

| Canal | Estado 2026-11-25 | Nota |
|---|---|---|
| `gh api -X GET search/repositories -f q='repo:<slug>'` | **OK** | ★, SPDX, `pushed_at`, `created_at`, `forks`, `archived` en una llamada. 34/34 resolvieron |
| `git ls-remote https://github.com/<slug>` | **OK** | Único canal fiable de existencia. 0 refs = no existe |
| `curl raw.githubusercontent.com/<slug>/HEAD/<ruta>` | **OK** | Único canal de lectura de licencia. 200/404 discrimina |
| `curl -sI https://github.com/<slug>` | **403 para todo** | **Quinto pase consecutivo midiéndolo.** La comprobación de URL que prescribe el brief sigue llevando **cero información** en este entorno |
| `gh api repos/<o>/<n>` | **403** | Acotado por la sesión |
| `WebFetch` a `ip-tools.org` y `projectpq.ai` | **ENOTFOUND** | **Nuevo hoy:** dos directorios del sector fuera de la lista de dominios permitidos de la sesión. Sorteado por el canal GitHub (`org:ip-tools` devolvió los 11 repos) |

## 🆕 2026-11-25 (pase 11) — el plano **acústico**: 113.000★ de infraestructura, **0★** de producto jurídico

El contraste más extremo que esta KB ha medido en once pases. La infraestructura de voz es
permisiva, madura y de altísima actividad; la capa jurídica encima **está vacía**.

### Lo que se movió esta semana (★ y `pushed_at` medidos 2026-11-25)

| Repo | Licencia | ★ | Commit | Señal |
|---|---|---|---|---|
| [ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp) | MIT | 55.504 | **2026-11-25** | Commit de hoy. Inferencia sin Python ni GPU |
| [SYSTRAN/faster-whisper](https://github.com/SYSTRAN/faster-whisper) | MIT | 27.003 | 2026-11-23 | El motor real bajo casi todos los servidores del plano |
| [NVIDIA-NeMo/Speech](https://github.com/NVIDIA-NeMo/Speech) | Apache-2.0 | 18.787 | **2026-11-25** | **Monorepo partido**: `NVIDIA/NeMo` ya no es la dirección |
| [k2-fsa/sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) | Apache-2.0 | 16.223 | 2026-11-24 | Offline en Android/iOS/RISC-V: *appliance* de sala |
| [m-bain/whisperX](https://github.com/m-bain/whisperX) | BSD-2-Clause | 25.661 | 2026-11-21 | `timestamp` por palabra = cita anclada al segundo |
| [pyannote/pyannote-audio](https://github.com/pyannote/pyannote-audio) | MIT (pesos CC-BY-4.0) | 10.841 | 2026-11-24 | Diarización de referencia |
| [speaches-ai/speaches](https://github.com/speaches-ai/speaches) | MIT | 3.782 | **2026-11-25** | API compatible OpenAI ⇒ migración a on-premise sin tocar clientes |
| [MahmoudAshraf97/ctc-forced-aligner](https://github.com/MahmoudAshraf97/ctc-forced-aligner) | BSD-2-Clause | 578 | 2026-11-24 | Alineación forzada permisiva |
| [revdotcom/fstalign](https://github.com/revdotcom/fstalign) | Apache-2.0 | 170 | 2026-11-16 | Medición de WER: la capa sin competencia |
| [gitchrisqueen/hearing-copilot](https://github.com/gitchrisqueen/hearing-copilot) | MIT | **0** | 2026-11-23 | **Único permisivo jurídico-específico del plano** |

### El censo del ecosistema jurídico, con `total_count` a la vista

| Consulta | `total_count` | Utilizable |
|---|---|---|
| `court transcript page line` | **0** | — |
| `hearing transcription judicial` | **0** | — |
| `legal transcript diarization` | 1 | 0 (sin fichero de licencia) |
| `deposition transcript parser` | 1 | 1 (`DepoIndex`, MIT, 0★, del pase 9) |
| `courtroom transcription` | 7 | **1** (`hearing-copilot`, MIT, 0★) |

Diez pases midieron este patrón en la capa de contratos y lo llamaron escasez. Aquí no es escasez:
es **ausencia estructural**, y tiene una causa nombrable — ver `T29`/`T31`.

### `T31` — **`T29` se repite, y esta vez el estándar es de PAGO y el formato es propietario**

`T29` (pase 8): *especificación abierta ≠ implementación disponible, y la distancia es el alcance de
un proyecto.* En el plano acústico la distancia es mayor porque **el artefacto certificado no tiene
especificación abierta en absoluto**:

- La cita de deposición es **`página:línea`** (`Smith Dep. 42:10-17`), con la página **a 25 líneas**
  y numeración consecutiva exigida por reglas procesales (p. ej. la regla californiana de líneas
  numeradas consecutivamente en cada página).
- Los formatos de intercambio del sector son **propietarios**: `PTX` (*E-Transcript Manager*,
  Thomson Reuters), `LEF` (LiveNote, transcript + exhibits + enlaces + vídeo sincronizado), y el
  `ASCII` de *Page Image* que generan los sistemas CAT.
- **Implementaciones permisivas medidas: cero.** Ni un lector de `PTX`, ni uno de `LEF`.
  `docling` (MIT, 70.821★, ya en esta KB) preserva números de página de un PDF, pero **nadie emite
  `página:línea` conforme**.

> **Consecuencia directa para una propuesta:** el stack ASR permisivo entrega *texto con
> timestamps*. El entregable que un litigio consume es **texto paginado y citable**. Ese salto
> —paginador determinista a 25 líneas, numeración, y el índice `página:línea`— es **código a
> escribir, no repo a adoptar**, y es pequeño, determinista y auditable. Es el hueco de producto
> mejor delimitado de los once pases.

### Canales, remedidos hoy (se reescribe porque cambia entre sesiones)

- `gh api -X GET search/repositories -f q='repo:<slug>'` — **OK**. Devuelve ★, SPDX, `pushed_at`,
  `archived` y forks en una llamada. `rate_limit` de búsqueda: 30/30 disponibles, no fue el
  limitante en ningún momento del pase.
- `HTTP 422` en ese canal = **renombrado o mudado**, confirmado 3/3 (`presidio`, `NeMo`,
  más un caso de inexistencia real). **No es un punto ciego del índice** — se formuló esa hipótesis
  y se descartó midiendo.
- `git ls-remote https://github.com/<slug>` — **OK**, sigue redirects, único árbitro de existencia.
- `curl raw.githubusercontent.com/<slug>/HEAD/<ruta>` — **OK**, único canal de lectura de licencia.
- `curl -sI github.com/<slug>` — **403 para todo** a través del proxy. **Quinto pase consecutivo
  midiéndolo:** la comprobación de URL que el brief prescribe sigue aportando **cero información**
  en este entorno, y se sustituye por `ls-remote` + `search/repositories`.
- `eur-lex.europa.eu` — **no resuelve** desde esta sesión (fuera de los dominios permitidos). El
  texto del Reglamento UE de AI de este pase viene de **fuentes secundarias y del *AI Act Service
  Desk* de la Comisión**, y se marca como tal en `intel/market.md`.
## 🆕 2026-11-25 (pase 10) — la **norma como dato**: aquí `T28` se rompe de verdad, y el que la rompe tiene 2.453★

El pase 9 dijo que la capa de estándares «escapa a `T28`» con `pyHanko` (MIT, 807★). Este pase
encuentra un caso **más fuerte y más incómodo**, y además encuentra el contraejemplo del
contraejemplo: la capa de estándares **no** es uniformemente permisiva. Las dos cosas se miden abajo.

### Infraestructura añadida este pase

| Repo | Licencia (leída) | Capa | Por qué es cimiento | ★ | Último commit |
|---|---|---|---|---|---|
| [CatalaLang/catala](https://github.com/CatalaLang/catala) | **Apache-2.0 (11.358 B)** | Ley como código | **Lenguaje de programación para especificar legislación** en *literate programming*: el código se anota línea a línea contra el texto legal, y su lógica por defecto (*default logic*) expresa **la excepción**, que es la forma nativa de la norma. 124 forks, 6 años, commit de hace 2 días | **2.453** | 2026-11-23 |
| [laws-africa/indigo](https://github.com/laws-africa/indigo) | LGPL-3.0 (*stub* 633 B) | Plataforma legislativa | Base de datos de legislación: gestiona, **consolida** y publica normativa en Akoma Ntoso. 38 forks. Es la plataforma vertical de este plano (ficha en `verticals/solutions.md`) | 78 | 2026-11-23 |
| [laws-africa/bluebell](https://github.com/laws-africa/bluebell) | GPL-3.0 (35.149 B) | Parser AN3 | Parser genérico de Akoma Ntoso 3: `act`, `bill`, `debate`, `doc`. Su documentación afirma que **produce siempre AN estructuralmente válido, cualquiera sea la entrada** | 23 | 2026-07-13 |
| [laws-africa/cobalt](https://github.com/laws-africa/cobalt) | LGPL-3.0 (*stub* 633 B) | Lib AN3 | Librería Python ligera: parsea y **valida contra el esquema AN 3.0** (estricto o relajado), operando sobre el XML sin objetos intermedios | 29 | 2026-06-18 |
| [laws-africa/slaw](https://github.com/laws-africa/slaw) | **MIT (1.067 B)** | Parser AN3 (Ruby) | ⚠️ **ARCHIVADO** (último commit 2022-06-28). Importa porque es el **único permisivo de todo el stack Akoma Ntoso**: referencia de API y base de fork, no dependencia | 28 | 2022-06-28 |
| [bungenix/akomantoso-lib](https://github.com/bungenix/akomantoso-lib) | Apache-2.0 (10.358 B) | API Java AN3 | API Java generada con JAXB desde el esquema AN 3.0. ⚠️ **dormante 9,4 años** (2017-06-29): se usa como *binding* de referencia, no como dependencia | 15 | 2017-06-29 |
| [oasis-open/legaldocml-akomantoso](https://github.com/oasis-open/legaldocml-akomantoso) | **CC-BY-2.0 (12.545 B)** | **El esquema** | El XSD normativo de OASIS LegalDocML. ⚠️ **No es código: es un documento con licencia Creative Commons.** 19 forks | 87 | 2022-06-02 |
| [unitedstates/congress](https://github.com/unitedstates/congress) | **CC0-1.0 (7.048 B)** | Datos legislativos 🇺🇸 | Recolector del Congreso federal. **CC0 = dominio público, sin atribución exigible**: la licencia más permisiva posible para un corpus. 228 forks | **1.071** | 2026-10-03 |
| [openstates/openstates-scrapers](https://github.com/openstates/openstates-scrapers) | GPL-3.0 (35.147 B) | Datos legislativos 🇺🇸 | Los 50 estados + DC + Puerto Rico, normalizados. **522 forks** y commit **de hoy**: el repo más vivo de este plano | **929** | 2026-11-25 |
| [openstates/people](https://github.com/openstates/people) | **CC0-1.0 (7.048 B)** | Datos de legisladores 🇺🇸 | El registro de personas y cargos, **separado del código GPL** y en CC0. Commit de hoy | 162 | 2026-11-25 |
| [openfisca/openfisca-core](https://github.com/openfisca/openfisca-core) | AGPL-3.0 (34.523 B) | Motor de reglas | Motor que ejecuta legislación socio-fiscal como código. 100 forks, 12 años, commit de ayer. **AGPL ⇒ ver aviso en `repos/foundations.md`** | 252 | 2026-11-24 |
| [PolicyEngine/policyengine-us](https://github.com/PolicyEngine/policyengine-us) | AGPL-3.0 (**34.519 B**) | Reglas 🇺🇸 | El modelo estadounidense sobre OpenFisca. **224 forks**, commit de ayer | 178 | 2026-11-24 |
| [maastrichtlawtech/cellar-extractor](https://github.com/maastrichtlawtech/cellar-extractor) | Apache-2.0 (11.357 B) | Corpus UE | Extrae metadatos de jurisprudencia de **CELLAR** por SPARQL y los enriquece. Procedencia académica (Maastricht Law & Tech Lab) | 8 | 2026-09-30 |
| [SenatoDellaRepubblica/AkomaNtosoBulkData](https://github.com/SenatoDellaRepubblica/AkomaNtosoBulkData) | CC-BY-4.0 (**sin fichero de licencia en 6 rutas**) | Corpus AN3 oficial 🇮🇹 | Volcado masivo en Akoma Ntoso del **Senado italiano**. Commit **de hoy** sobre un repo de 2016: el corpus AN oficial más longevo y más vivo que existe | 42 | 2026-11-25 |
| [silegis-mg/editor-articulacao](https://github.com/silegis-mg/editor-articulacao) | LGPL-3.0 (`COPYING` = **GPL-3.0, 35.147 B**) | Redacción legislativa 🇧🇷 | Editor de articulación de **la Asamblea Legislativa de Minas Gerais**: redacta el texto normativo con su estructura (artículo, parágrafo, inciso). ⚠️ dormante desde 2024-06-25 | 18 | 2024-06-25 |
| [step21/eurlex](https://github.com/step21/eurlex) | AGPL-3.0 (34.523 B) | Cliente CELLAR | Paquete Python que construye consultas SPARQL contra Cellar y descarga. Deriva del paquete R `eurlex` | 14 | 2026-03-09 |
| [seljaseppala/eu_corpus_compiler](https://github.com/seljaseppala/eu_corpus_compiler) | GPL-3.0 (35.149 B) | Corpus UE | *Pipeline* que recoge IDs de CELLAR por SPARQL y descarga el XML/HTML correspondiente. ⚠️ dormante desde 2021-12-03 | 19 | 2021-12-03 |
| [usgpo/bulk-data](https://github.com/usgpo/bulk-data) | 🔴 **SIN LICENCIA** (null; 6 rutas probadas, 6 × 404) | Datos federales 🇺🇸 | Documentación de los volcados masivos del **Government Publishing Office**. 146 forks, **387★ y ningún fichero de licencia**: obra del gobierno de EE. UU., pero **eso es una presunción jurídica, no un grant** | 387 | 2026-06-11 |

### 🔑 `T33` — `T28` y `T29` eran la misma regla mal enunciada. El discriminante no es la capa: es **si quien publica opera un servicio**

`T28` (pase 8): de {específico, maduro, permisivo} se eligen dos. `T29` (pase 9): la capa de
estándares se escapa «porque su valor es la interoperabilidad». **Este plano rompe las dos**, y en
direcciones opuestas:

| Caso | Específico | Maduro | Permisivo | ¿Encaja en `T28`/`T29`? |
|---|---|---|---|---|
| `CatalaLang/catala` | **Sí** (lenguaje *para* legislación) | **Sí** (2.453★, 124 forks, 6 años, activo) | **Sí** (Apache-2.0) | 🔴 **Rompe `T28`: tiene las tres** |
| `laws-africa/{cobalt,bluebell,indigo}` | Sí | Sí (10 años, activos) | 🔴 **No** (LGPL/GPL) | 🔴 **Rompe `T29`: son implementaciones de estándar y son copyleft** |
| `oasis-open/legaldocml-akomantoso` | Sí | Sí | n/a (**CC-BY**, es un documento) | — |
| `unitedstates/congress`, `openstates/people` | Sí | Sí | **Sí (CC0)** | 🔴 Rompe `T28` |

La regla que explica **los cuatro** casos a la vez:

> **`T33` — Lo que determina la licencia no es la capa (estándar vs. flujo) ni la madurez: es si
> quien publica OPERA UN SERVICIO sobre ese código.** Laws.Africa **opera** una plataforma de
> publicación de legislación africana; sus parsers son su producto, y elige LGPL/GPL aunque sean
> implementaciones de un estándar abierto. Catala es **investigación** (INRIA): su objetivo es que
> la técnica se adopte, y elige Apache-2.0 aunque sea madura y específica. `unitedstates/congress`
> y `openstates/people` son **bienes públicos cívicos**: eligen CC0, la licencia más permisiva que
> existe. La pregunta operativa no es «¿qué capa es?» sino **«¿de qué vive el que lo publica?»** —
> y eso se lee en la organización propietaria, no en el `README`. **Probar en las otras once
> industrias: es la primera regla de esta KB que predice la licencia desde el publicador.**

### 🧮 El checksum de licencias (932-G1) rindió 32/32, **corrigió dos bandas publicadas** y añadió cuatro

| Licencia | Bytes medidos este pase | Estado |
|---|---|---|
| MIT | **1.036** · 1.067 (×4) · 1.069 (×2) · 1.071 · 1.077 · 1.082 | 🔴 **CORRECCIÓN: el suelo baja de 1.062 a 1.036** (`InfoLeg-MCP`). Banda acumulada **1.036–1.090** |
| AGPL-3.0 | **34.519** (×2) · 34.523 | 🔴 **CORRECCIÓN: el pase 8 la declaró «constante 34.523 exactos» y el pase 9 lo confirmó. Es FALSO: es una banda de 34.519–34.523** |
| GPL-3.0 | **35.147** (×2) · 35.149 (×2) | 🔴 **Refinada: no es 35.149, es 35.147–35.149** |
| Apache-2.0 | **10.358** · 11.314 · 11.317 · 11.344 · 11.357 · 11.358 (×2) | 🔴 **Banda muy ensanchada por abajo:** el de 2013 (`akomantoso-lib`) pesa **~1 KB menos** que el clúster moderno |
| **GPL-2.0** | **18.033** | 🆕 **banda nueva** (`lexml-parser-projeto-lei`) |
| **CC0-1.0** | **7.048** (×2, organizaciones independientes) | 🆕 **banda nueva** |
| **CC-BY-2.0** | **12.545** | 🆕 **banda nueva** |
| **LGPL-3.0** (*stub*) | **633** (×2) | 🆕 **banda nueva — y es un *stub*, no el texto:** 633 B de remisión a la LGPL, no la licencia íntegra |
| 🔴 *bespoke* no comercial | **6.732** | 🆕 **«Akoma Noncommercial and Commercial Licence 1.0»** — ninguna banda, marcado como anomalía antes de abrir el fichero |

> ⚠️ **Dos lecciones de método, y la segunda es nueva:**
> **(1)** Una banda «confirmada» por dos pases consecutivos puede seguir siendo falsa: la de AGPL lo
> era. Dos confirmaciones **del mismo valor** no prueban que no exista otro.
> **(2)** 🆕 `G-L21` — **para LGPL hay que leer DOS ficheros.** `silegis-mg/editor-articulacao` es
> LGPL-3.0 según el clasificador, pero su `COPYING` contiene el texto **GPL-3.0** (35.147 B): la
> LGPL-3.0 **se expresa como GPL-3.0 + un suplemento** (`COPYING.LESSER`). Leer sólo `COPYING`
> devuelve «GPL-3.0» y **endurece la licencia por error** — copyleft fuerte donde hay copyleft
> débil, que es *enlazable* desde producto cerrado. El error es conservador, pero descarta activos
> utilizables.

### 🧮 Censo de URLs de este pase

**34/34 direcciones resuelven** (`git ls-remote`, refs > 0). **32/34 licencias leídas byte a byte**;
**2 sin fichero de licencia** en 6 rutas probadas (`usgpo/bulk-data`, `AkomaNtosoBulkData`), ambas
publicadas con el hueco explícito. **2 archivadas, marcadas** (`laws-africa/slaw`,
`diegocaro/leychile`). Barrido de estructura `G-L11`: **0 defectos**, **0 cabeceras como dato**.

### 🔌 Estado de los canales — **una regresión que invalida el instrumento del brief, otra vez y al revés**

`curl -sI github.com/<slug>` ya **no** devuelve 403 (como en los pases 6–9): devuelve
`HTTP/1.1 200 Connection Established`, **la respuesta del CONNECT del proxy**, idéntica para un repo
real y para uno inexistente. ⇒ **La verificación pasó de ciega a engañosa.** Medida correcta:
`curl -s -o /dev/null -w '%{http_code}'`. `git ls-remote` sigue siendo el único canal de existencia
fiable y `raw.githubusercontent.com` el único de lectura de licencia.

---

## 🆕 2026-11-25 (pase 9) — **el caudal no estaba seco: estaba en la capa de estándares**, y ahí el permisivo gana

Tercer pase consecutivo que mide el caudal de creación y tercer pase que encuentra activos fuera del
vocabulario con el que lo midió. Lo de hoy, además, **refuta en parte la matriz `T28` del pase 8**.

### Infraestructura añadida este pase — y son los mejores activos permisivos de la KB

| Repo | Licencia (leída) | Capa | Por qué es cimiento | ★ | Último commit |
|---|---|---|---|---|---|
| [MatthiasValvekens/pyHanko](https://github.com/MatthiasValvekens/pyHanko) | **MIT (1.080 B)** | Conformidad de firma | Firma, sella **y valida** PDF con perfiles **PAdES** (los que la UE exige para firma cualificada). 121 forks, creado 2020-08-06, commit de hace 2 días. **MIT ⇒ empotrable en producto cerrado** | **807** | 2026-11-23 |
| [esig/dss](https://github.com/esig/dss) | LGPL-2.1 (26.530 B) | Conformidad de firma | **La implementación de referencia de la Comisión Europea** (`eu.europa.ec.joinup.sd-dss` en Maven Central). PAdES, XAdES, CAdES, ASiC contra las listas de confianza de la UE. **LGPL = copyleft débil: enlazable desde producto cerrado** | **1.051** | 2026-11-04 |
| [frisk55frisk/loadfile-tool](https://github.com/frisk55frisk/loadfile-tool) | **MIT (1.078 B)** | Interoperabilidad e-discovery | Único permisivo que **valida, convierte e inspecciona** `Concordance DAT`, `OPT`, `LFP`, `DII`: el intercambio de producciones entre plataformas de revisión | 0 | 2026-03-31 |
| [wikkiewikkie/Marisol](https://github.com/wikkiewikkie/Marisol) | **MIT (1.075 B)** | Prueba producible | Numeración **Bates** + estampado + redacción de PDF. ⚠️ **dormante desde 2023-08-28**: referencia de API y base para forkear, no dependencia viva | 18 | 2023-08-28 |
| [JuliusScheuerer/document-anonymizer](https://github.com/JuliusScheuerer/document-anonymizer) | **MIT (1.073 B)** | Redacción / PII | Anonimización **de documentos en alemán** con redacción **física** del PDF (no capa visual encima). 29 refs. **Alemania · EMEA** | 5 | 2026-03-30 |
| [Markonick/greek-pii-redaction](https://github.com/Markonick/greek-pii-redaction) | **MIT (1.071 B)** | Redacción / PII | Detección PII **offline** y redacción real de PDF en **griego** (Presidio + PyMuPDF). **Grecia · EMEA** | 0 | 2026-10-12 |

### 🔑 `T29` — la **capa de estándares** escapa a la matriz `T28`, y tiene causa estructural

`T28` (pase 8) afirma: de **{específico del sector, maduro, permisivo}** se eligen dos. `pyHanko` las
tiene **las tres** (MIT + 807★/121 forks/6 años + específico del artefacto PAdES), y `esig/dss` casi.
No es excepción: **una implementación de estándar se publica permisiva porque su valor es la
interoperabilidad**, mientras quien construye el flujo completo del despacho quiere capturarlo y
elige AGPL. ⇒ **Adoptar el estándar, construir el flujo.** Detalle y tabla en `repos/foundations.md`.

### 🧮 El checksum de licencias (932-G1) rindió 19/19 y añadió **tres bandas nuevas**

| Licencia | Bytes medidos | Estado |
|---|---|---|
| MIT | **1.062 – 1.090** (12 casos) | banda confirmada, la más estable de la KB |
| Apache-2.0 | 11.317 | confirmada |
| **LGPL-2.1** | **26.530** | 🆕 **banda nueva — primer caso en esta KB** |
| **EUPL-1.2** | **13.832** | 🆕 **banda nueva** (licencia pública de la UE, `autogram-portal`) |
| **Unlicense** | **1.211** | 🆕 **banda nueva** — ⚠️ **cae DENTRO del rango alto de MIT**: por bytes **no** se distingue de MIT, sólo por el texto. Primera colisión de bandas que mide esta KB |
| GPL-3.0 | 35.149 | confirmada |
| AGPL-3.0 | 34.523 | confirmada |

> ⚠️ **Y eso acota el propio instrumento:** el checksum de bytes es un *detector de anomalías*, no un
> identificador. `Unlicense` (1.211 B) y `MIT` (hasta 1.090 B) están demasiado cerca. **La regla
> sigue siendo abrir el fichero.**

### 🔴 La capa de redacción confirma `T28` por tercera vez, y conviene verlo junto

| Activo | Licencia | ★ | Lectura |
|---|---|---|---|
| `seanpedrick-case/doc_redaction` | **AGPL-3.0** (34.523 B) | 64 | lo **maduro** de la categoría es copyleft de red |
| `sophia486/pii-gui` | **AGPL-3.0** | 49 | ídem, *local-first*, muy activo |
| `JuliusScheuerer/document-anonymizer` | **MIT** | 5 | lo **permisivo** es regional y pequeño (alemán) |
| `Markonick/greek-pii-redaction` | **MIT** | 0 | ídem (griego) |

**Patrón, cuarta medición consecutiva:** maduro ⇒ copyleft; permisivo ⇒ joven y/o regional. Para un
entregable comercial, las dos filas MIT son el punto de partida **aunque tengan 5★ y 0★**.

### 🧮 Censo de URLs de este pase

**19/19 direcciones resuelven** (`git ls-remote`, refs > 0), **0 archivadas**, **19/19 licencias
leídas byte a byte**. Barrido de estructura `G-L11`: **0 defectos**. **0 cabeceras como dato.**

### 🔌 Estado de los canales en esta sesión

`gh api search/repositories` ✅ · `git ls-remote` ✅ · `raw.githubusercontent.com` ✅ ·
`curl -sI github.com` 🔴 **403 para todo, ciego** · **`WebFetch` a fuentes legales primarias 🔴
`ENOTFOUND`** (`boe.es`, `edomex.quadratin.com.mx` fuera de los dominios permitidos) ⇒ **lo
regulatorio de este pase es de un solo canal y va marcado.**

---

## 🆕 2026-11-22 (pase 8) — el espinazo permisivo del plano de ingresos **existe y es genérico**

El pase 8 abre la capa de facturación, plazos y cuentas de terceros (ver `agents/trending.md` para
los agentes y `G-L17` para el fallo de canal que la mantenía invisible). Por el lado de
**infraestructura** el resultado es inverso al de los agentes: aquí no falta madurez, falta
**semántica legal**.

### Infraestructura añadida este pase — el espinazo sobre el que se construye

| Repo | Licencia (leída byte a byte) | Stars | Último commit | Qué aporta al plano de ingresos |
|---|---|---|---|---|
| [killbill/killbill](https://github.com/killbill/killbill) | **Apache-2.0 (11.357 B)** | 5.862 | 2026-11-21 | Plataforma de facturación y pagos, **14 años de vida**, 990 forks. Catálogos, planes, prorrateos, impuestos, *dunning*, plugins de pago. La base permisiva más madura de toda esta capa |
| [FOSSBilling/FOSSBilling](https://github.com/FOSSBilling/FOSSBilling) | **Apache-2.0 (11.454 B)** | 1.757 | 2026-11-20 | Facturación + clientes + órdenes en PHP, con sistema de módulos. Alternativa más ligera a Kill Bill cuando el despacho es la unidad y no hay volumen de suscripción |
| [InvoicePlane/InvoicePlane](https://github.com/InvoicePlane/InvoicePlane) | **MIT** dentro de fichero compuesto (5.087 B) — GitHub lo da como `NOASSERTION` | 3.290 | 2026-11-18 | Presupuestos → facturas → pagos, autoalojado. Ver abajo: la marca está restringida, **el código no** |
| [kimai/kimai](https://github.com/kimai/kimai) | **AGPL-3.0 (34.523 B)** ⚠️ | 5.173 | **2026-11-22** | El registro de tiempos open source de referencia: *timesheets*, tarifas por proyecto/actividad/usuario, export de facturas, API. ⚠️ Copyleft de red: sirve como **herramienta interna del despacho**, no como componente de un SaaS cerrado |
| [InvoiceShelf/InvoiceShelf](https://github.com/InvoiceShelf/InvoiceShelf) | **AGPL-3.0 (34.523 B)** ⚠️ | 2.075 | 2026-11-22 | Facturación autoalojada (fork mantenido del linaje Crater). Misma advertencia de copyleft |

**Ninguno de los cinco sabe qué es un expediente, un código UTBMS, un plazo procesal ni una cuenta
de terceros.** Esa es exactamente la distancia que hay que construir, y es la razón de que
`P28`–`P30` existan.

### 🧮 El checksum de licencias (932-G1) rindió 11/11, y afinó la banda AGPL a **una constante**

Tres lecturas AGPL-3.0 en repos sin relación —`kimai`, `deedbox-app` y
`DoGood-Studio/legal-deadline-calculator`— dan **34.523 B exactos las tres**. La banda Apache quedó
en 11.350–11.454 B (3 lecturas) y la MIT en 1.056–1.080 B (7 lecturas). Detalle en
`repos/foundations.md`.

### 🔁 `NOASSERTION`, tercera vez consecutiva — y el modo de fallo es nuevo: **el aviso de marca va primero**

`InvoicePlane` abre su `LICENSE.txt` con las restricciones de uso del nombre y el logotipo, y sólo
después incluye el texto MIT íntegro. El clasificador de GitHub lee el principio del fichero y se
rinde. **Restricción de marca ≠ restricción de código:** no se puede redistribuir *bajo el nombre*
InvoicePlane; todo lo demás que MIT permite, se puede. La regla asimétrica de bandas predijo
«compuesto» antes de abrir el fichero (5.087 B ≫ banda MIT) y acertó por tercer pase seguido.

### 🧮 Censo de URLs de este pase

**24 slugs** consultados por `search/repositories` + `ls-remote` + lectura de `LICENSE`:
**21 resuelven**, **1 devuelve 422** (`emirmrkaljevic/awesome-legal-tech`, indexado por el buscador
web y **inexistente** por el canal de GitHub), **2 existen sin fichero de licencia en 5/5 rutas**
(`Iuris-Soft`, `legal-invoice-review-agents` — descartados por ausencia *medida*, que es el único
descarte legítimo según la regla del pase 6). **0 archivados.** 1 dormancia relevante y publicada:
`OpenLawOffice`, Apache-2.0, **sin commits desde 2016-04-10**.

### 🔌 Estado de los canales en esta sesión

Idéntico al medido en los pases 6 y 7, y se vuelve a escribir porque **cambia entre sesiones**:

- ✅ `gh api -X GET search/repositories -f q='repo:<slug>'` — estrellas, SPDX, `pushed_at`,
  `archived` y forks en una llamada. **422 para slug renombrado y para inexistente por igual.**
- ✅ `git ls-remote https://github.com/<slug>` — recuento de refs: el único canal de existencia
  fiable (`0` = no existe) y el único que detecta renombrados por identidad de HEAD.
- ✅ `curl raw.githubusercontent.com/<slug>/HEAD/<ruta>` — 200/404 discrimina correctamente. **Es el
  canal de lectura de licencia**, y el único que distingue `NOASSERTION` de «sin licencia».
- 🔴 `curl -sI https://github.com/<slug>` — **403 para todo** a través del proxy: repos vivos,
  renombrados e inexistentes por igual. **La comprobación de URL que prescribe el brief sigue
  llevando cero información en este entorno.** Cuarto pase consecutivo que lo mide.
- 🔴 `gh api repos/<o>/<n>` — 403 (ámbito de sesión).

## 🆕 2026-11-22 (pase 7) — lo que se movió no fue el caudal de repos nuevos: fue la **licencia de uno viejo**

### El caudal de creación sigue seco, y ahora está medido dos pases seguidos

`gh api search/repositories -f q='legal AI created:>2026-08-01 stars:>=25'` ⇒ **`total_count` = 10**
en casi **cuatro meses**, y de esos 10 **seis ya estaban en esta KB**, dos no son legales
(`revlab` = ingeniería inversa de PE en Windows; `sigillion` = memoria para agentes) y dos se
descartan arriba. **Repos legales nuevos y relevantes por encima de 25★ en 16 semanas: 0.**

Esto **confirma** la conclusión del pase 6 con una ventana más ancha: *una vez pagada la deuda de
descubrimiento, un pase horario no puede producir activos nuevos.* Lo que sí produce, y este pase
lo demuestra, es **corregir la licencia de un activo que la KB llevaba seis pases citando mal**.

### Infraestructura añadida este pase

| Repo | Licencia (leída) | Stars | Último commit | Qué aporta |
|---|---|---|---|---|
| [harveyai/harvey-labs](https://github.com/harveyai/harvey-labs) | **MIT (1.067 B)** | **1.668** | 2026-11-12 | **Harvey LAB**: 2.010 tareas con rúbricas + harness de ejecución con adaptadores multi-modelo. La capa de evaluación permisiva que esta KB no tenía. |
| [HazyResearch/legalbench](https://github.com/HazyResearch/legalbench) | 🔴 **NOASSERTION** · licencia **por tarea** (124 CC BY · 4 MIT · 2 CC BY-SA · **30 NC** · 2 sin concesión) | 663 | 2026-03-30 | Se le da **fila y URL por primera vez**. Estaba citado en tres ficheros **sin ninguna de las dos**, y por eso nunca pasó por el barrido. |

### 🧮 Censo de URLs de este pase — el más completo de los siete

| Control | Resultado |
|---|---|
| Slugs citados en los 8 ficheros | **93** |
| Verificados por **doble canal** (`search/repositories` + `ls-remote`) | **93 / 93** |
| Inexistentes | **0** |
| Archivados | **0** |
| Renombrados | **3**, los tres ya documentados, confirmados hoy por **identidad de HEAD** |
| Bloques de tabla barridos con `P22` | **101**, **0 defectos** |

### 🔌 Estado de los canales en esta sesión (cambia entre sesiones — por eso se escribe)

| Canal | Estado hoy | Nota |
|---|---|---|
| `gh api -X GET search/repositories -f q='repo:<slug>'` | ✅ **funciona** | estrellas + SPDX + `pushed_at` + `archived` en una llamada |
| `git ls-remote https://github.com/<slug>` | ✅ **funciona** | existencia y SHA de HEAD; **el único que detecta renombrados** |
| `curl` a `raw.githubusercontent.com/<slug>/HEAD/<path>` | ✅ **funciona** | 200/404 discrimina bien; es el canal de lectura de licencia byte a byte |
| `curl -sI https://github.com/<slug>` | 🔴 **ciego** | devuelve `HTTP/1.1 200 Connection Established` (es el CONNECT del proxy) **para cualquier cosa**. El chequeo de URL que prescribe el *brief* **no aporta información aquí**; confirmado por tercer pase consecutivo. |
| `curl https://api.github.com/repos/<o>/<n>` | 🔴 **403** | la sesión no tiene ese ámbito |
| `www.damiencharlotin.com` (base de datos de citas alucinadas) | 🔴 **no resuelve** | fuera de los dominios permitidos de la sesión. **Es la fuente primaria del contador de sanciones** que esta KB cita de segunda mano: queda declarado como hueco de canal, no como dato ausente. |

---

## 🆕 2026-11-21 (pase 6, 21:40 UTC) — el caudal no estaba seco: estaba **en portugués**

El pase 5 midió que el flujo de repos legales nuevos se había secado (`legal AI
created:>2026-09-01 stars:>=40` ⇒ `total_count=4`) y concluyó, con razón para lo que medía, que
una pasada horaria ya no puede producir activos nuevos. **Este pase incorpora 6 activos nuevos sin
que esa medición fuera incorrecta** — y la diferencia explica el resto del pase:

> La consulta del pase 5 pedía `stars:>=40` **en el índice de GitHub, en inglés**. Los cuatro MCP
> de fuentes oficiales LATAM tienen **4, 2, 71 y 0 estrellas** y tres se describen en portugués.
> Ninguno habría aparecido. **No era caudal seco: era un instrumento que no apuntaba ahí.**
> Distinguir «flujo de creación» de «deuda de descubrimiento» (pase 5) sigue siendo correcto; lo
> que faltaba es que **la deuda de descubrimiento tiene idioma**.

### Repos de infraestructura nuevos (licencia leída byte a byte, 2026-11-21)

| Repo | Licencia (leída) | Capa | Por qué entra | ★ |
|------|------------------|------|---------------|---|
| [matematicsolutions/br-eli-mcp](https://github.com/matematicsolutions/br-eli-mcp) | Apache-2.0 (11.358 B) | Fuentes oficiales 🇧🇷 | 8 APIs **sin clave**: Câmara, Congresso (+DOU), `normas.leg.br`, DataJud/CNJ, STJ, CARF, TST, TCU. No scrapea Planalto. | 4 |
| [mazulo/leis-mcp](https://github.com/mazulo/leis-mcp) | MIT (1.071 B) | Legislación 🇧🇷 | **1.218.990 normas** + avisos de revogação + validación de vigencia. | **71** |
| [ivancaron/jurismcp](https://github.com/ivancaron/jurismcp) | MIT (1.078 B) | Jurisprudencia 🇧🇷 | STJ/STF/TST/TJES/LexML/BNP-CNJ/TNU/TRF4. Separa portal oficial de agregador. | 2 |
| [BEG-lag/mcp-dof](https://github.com/BEG-lag/mcp-dof) | MIT (1.082 B) | Boletín oficial 🇲🇽 | **DOF** vía API oficial **SIDOF**. Primer activo mexicano de fuente oficial en esta KB. | **0** |
| [daniel-filius/awesome-mcp-brasil](https://github.com/daniel-filius/awesome-mcp-brasil) | **CC0-1.0** (7.048 B) | Índice + canal | 13 entradas *Jurídico/Legislativo* entre 8 secciones. **Dominio público** ⇒ derivable sin atribución. | 0 |
| [rohasnagpal/legal-ai-skills](https://github.com/rohasnagpal/legal-ai-skills) | MIT (1.069 B) | Skills | 244 skills, 17 especialistas + router; India/EE. UU./RU/**Singapur**. Alternativa permisiva a la lista CC-BY-NC-ND. | **214** |

### 🧮 El checksum de licencias (932-G1) rindió 7/7 — y afinó **dos** bandas

- **CC0-1.0 es exacta, no aproximada:** `awesome-mcp-brasil`, `chen-friedman/awesome-legaltech` y
  `General-Legal/legal-templates` miden **7.048 B los tres**. CC0 no lleva línea de titular, así
  que no tiene dispersión ⇒ **cualquier desvío del 7.048 indica fichero modificado**.
- **Apache-2.0 tolera cola, no cabecera:** `apache/ofbiz-framework` mide **11.906 B**, +548 sobre
  la banda, porque incorpora el `NOTICE` **dentro** del fichero. La banda sigue siendo válida como
  clasificador; el desvío por arriba hay que leerlo como *licencia + apéndice*, no como otra
  licencia.
- **Y una refutación de fuente indexada:** una fuente afirma que **iDURAR ERP/CRM** es «fully
  open-source under the MIT license». Es **AGPL-3.0**: `LICENSE` mide **34.230 B**, banda AGPL
  (~34.500). El checksum lo predijo antes de leer el encabezado. Ver `verticals/solutions.md`.

### 🔌 El juego de canales cambió respecto del pase 5, y eso invalida dos instrumentos prescritos

| Canal | Pase 5 | Pase 6 (medido con par conocido-bueno/conocido-malo) |
|-------|--------|------------------------------------------------------|
| `gh api search/repositories` | ✅ ★+SPDX+`pushed_at` | 🔴 **422** salvo repos de la sesión |
| `git ls-remote` (existencia + **renombrado**) | ✅ oráculo prescrito para toda la rotación | 🔴 **0 refs para todo**, repos vivos incluidos |
| `raw.githubusercontent.com/.../HEAD/<f>` | ✅ | ✅ confirmado — oráculo **positivo** (200 = existe; 404 = no concluyente) |
| WebFetch sobre `github.com/<slug>` | no usado | ✅ **★ + licencia + README**: el sustituto de `search/repositories` |

⇒ **Consecuencia honesta para este pase: 83/83 URLs resuelven, pero los renombrados NO están
comprobados** y no hay `pushed_at` para las filas nuevas (van con `n/d ⚠️`, no con fecha
inventada). **Regla:** ningún pase hereda el juego de canales del anterior; se sondea primero.

### ✅ Barrido de integridad del pase 6

83/83 URLs resuelven (0 bajas) · **91 bloques de tabla, 0 defectos** (`P22`/G-L11 aguanta tras
+9 filas) · 7/7 licencias en banda · 0 filas repintadas por deriva de ★ · append-only respetado en
los dos ficheros de tendencias.

## 🆕 2026-11-21 (pase 5, 01:38 UTC) — el caudal de repos legales nuevos se ha secado, y es medible

**Instrumento del pase, barato y reproducible:** en vez de preguntar «¿qué hay de nuevo?» (que
devuelve lo que el ranking quiera), preguntar **cuántos activos legales nuevos han superado un
umbral de señal en una ventana datada**:

```bash
gh api -X GET search/repositories -f q='legal AI created:>2026-09-01 stars:>=40' \
  -f sort=stars -f order=desc --jq '.total_count'
```

**Resultado, 2026-11-21: `total_count = 4`.** Y al leer los cuatro, sólo **dos son legales**:

| Repo | Licencia | Stars | Creado/push | ¿Legal? |
|---|---|---:|---|---|
| [FuturixAI-and-Quantum-Works/Prism-Legal-OS](https://github.com/FuturixAI-and-Quantum-Works/Prism-Legal-OS) | AGPL-3.0 | 226 | 2026-10-03 | ✅ sí — **ya estaba en esta KB** desde el pase 3 |
| [meta-models/legal-agent-workshop](https://github.com/meta-models/legal-agent-workshop) | **MIT** | 73 | 2026-11-06 | ✅ sí — **nuevo, se incorpora** |
| [paveldevyatov/refund-anything-ai-prompt](https://github.com/paveldevyatov/refund-anything-ai-prompt) | MIT | 104 | 2026-10-06 | ❌ no — reclamaciones de consumo, no práctica jurídica |
| [msmahdinejad/iran-bourse-mcp](https://github.com/msmahdinejad/iran-bourse-mcp) | MIT | 42 | 2026-11-15 | ❌ no — bolsa de Teherán; entra por la palabra «legal» en otro contexto |

⇒ **En once semanas, UN solo repo legal nuevo cruzó los 40★.** Compárese con los pases 2 y 3 de
anteayer, que incorporaron 7 filas nuevas cada uno — pero **de repos preexistentes que la KB no
había encontrado**, no de repos nuevos. **Son dos fenómenos distintos y la KB los estaba
confundiendo:** *caudal de creación* (se ha secado) vs *deuda de descubrimiento* (era enorme y se
está pagando). Que los pases encuentren muchas filas nuevas **no** significa que el ecosistema
crezca rápido; significa que la KB venía con retraso.

**Implicación para la rotación, y es la que importa:** una vez pagada la deuda de descubrimiento,
**un pase horario sobre la misma industria no puede producir activos nuevos** — el caudal real es
de ~1 repo relevante al mes. La frecuencia útil de repaso de `agents/top.md` y
`repos/foundations.md` es **semanal o mensual**, no horaria. Lo que sí rinde en cada pase es
**verificación, corrección y cierre de huecos**, que es a lo que este pase dedicó el presupuesto.

### Repos nuevos incorporados en este pase

| Repo | Licencia (leída) | Stars | Push | Capa |
|---|---|---:|---|---|
| [AI4CharityPL/kancelaria-lex](https://github.com/AI4CharityPL/kancelaria-lex) | **MIT** (1.069 B) | 60 | 2026-08-23 | **Expedientes judiciales locales con verificación de cita por construcción** (Polonia). Localidad impuesta por red: 4 segmentos Docker, 3 con `internal: true`. OCR con **marcador permanente** — cada cita derivada de escaneo se muestra como `z OCR`, porque «apunta a un carácter del expediente» y «apunta a un carácter de **la lectura** del expediente» no son lo mismo. **Ninguna otra fila de esta KB hace esa distinción de procedencia.** |
| [boyeesu/Kourti](https://github.com/boyeesu/Kourti) | **MIT** (1.069 B) | 1 | 2026-11-01 | **Practice management permisivo** — cierra el hueco (ver `verticals/solutions.md`). React + Node + PostgreSQL. |
| [meta-models/legal-agent-workshop](https://github.com/meta-models/legal-agent-workshop) | **MIT** | 73 | 2026-11-06 | **Enablement**: capa de verificación ejecutada *fuera* del control del agente, con firma del abogado. |
| [mayan-edms/Mayan-EDMS](https://github.com/mayan-edms/Mayan-EDMS) | **Apache-2.0** (puntero 586 B) | 850 | 2026-05-23 🪦 | DMS con estados de workflow. **Espejo** (sin PRs/issues). |

### 🧮 El checksum de licencias (932-G1) corrigió a GitHub **dos veces en el mismo pase**, una por cada lado de la regla

| Repo | GitHub dice | Bytes | Predicción de la regla | Lectura real |
|---|---|---:|---|---|
| OpenSign | `NOASSERTION` | **35.051** | por encima de la banda AGPL ⇒ **compuesta** | ✅ AGPL-3.0 + carve-out `customRoute` + terceros |
| Mayan EDMS | `NOASSERTION` | **586** | muy por debajo de la banda Apache ⇒ **puntero** | ✅ puntero Apache-2.0 genuino |

**`NOASSERTION` no significa «sin licencia»: significa «el clasificador de GitHub no pudo».** En
los dos casos la licencia era perfectamente utilizable y los bytes lo dijeron antes de leer nada.
🔴 **Esto cambia una práctica de esta KB:** las filas que se descartaron por `NOASSERTION` sin
abrir el fichero deben revisarse. En este pase se revisaron las dos que había, y **las dos eran
adoptables** (una AGPL con carve-out, una Apache-2.0 limpia).

### 🔧 G-L11 — barrido de **estructura** de tabla, no de filas: 86 bloques, 2 defectos

Control nuevo, mecánico y sin red. Los controles de esta KB validan *filas*; ninguno validaba la
**tabla**. Encontró que la tabla principal de `agents/top.md` estaba **partida en dos** por una
línea en blanco, dejando **7 filas sin cabecera** — las mismas 7 que el pase 4 auditó una por una
y declaró correctas. Lo eran: *el defecto estaba en el carácter que las separaba de su cabecera.*

```bash
# exige, por cada bloque de lineas que empiezan por '|':
#   (1) fila separadora |---| en la 2.a posicion   -> si falta, es tabla sin cabecera
#   (2) numero de columnas constante en todo el bloque
python3 - <<'PY'
import re,glob
for f in sorted(glob.glob('*/*.md')):
    L=open(f,encoding='utf-8').read().split('\n'); i=0
    while i<len(L):
        if L[i].lstrip().startswith('|'):
            s=i; blk=[]
            while i<len(L) and L[i].lstrip().startswith('|'): blk.append(L[i]); i+=1
            sep=len(blk)>1 and re.match(r'^\|[\s:|-]+\|?\s*$',blk[1].strip())
            n=[len(re.split(r'(?<!\\)\|',b.strip().strip('|'))) for b in blk]
            if not sep or len(set(n)-{n[0]})>0: print(f'{f}:{s+1} sep={bool(sep)} cols={n}')
        else: i+=1
PY
```

**Resultado tras la reparación: 86 bloques, separadora presente en todos, 0 mismatches de
columnas.** (El propio P22, al ejecutarse sobre esta KB, encontró **2** defectos: la tabla partida
de `agents/top.md` y —al redactar el cuadro que la documenta— una **barra vertical sin escapar
dentro de *inline code***, que en GFM también parte la celda. Documentar el fallo lo reprodujo.) ⇒ **Correr esto en las 12 industrias**: es gratis y detecta pérdida silenciosa de
entidades.

---

## 🆕 2026-11-21 (pase 4) — el censo de nombre: `LawLink` son 113 repos, `docassemble` son 1.444, y significan lo contrario

**Instrumento nuevo de este pase** (`compose/patterns.md` → **P18**): contar cuántos repos comparten
un nombre **antes** de escribir «**el**» seguido de ese nombre.

```
LawLink     in:name → 113        docassemble in:name → 1.444
awesome-legaltech in:name → 5    OpenContracts in:name → 17
```

**Y el control es el hallazgo, no el censo.** `docassemble` tiene **más** homónimos que `LawLink` y
es el mejor activo del fichero. La diferencia está en la **forma**: en `docassemble` **un solo repo
tiene el nombre desnudo con 1.015★** y los 1.443 restantes son **`docassemble-<extensión>`**
(`-AssemblyLine`, `-ALWeaver`, `-docusign`…) ⇒ **ecosistema de paquetes, señal de salud**. En
`LawLink` **muchos repos tienen el nombre idéntico y todos ~0★** ⇒ **comunal de nombre, el nombre no
identifica nada**. Un `total_count` alto **sube** la confianza en el primer caso y la **destruye** en
el segundo. Tabla del discriminador en P18.

### Lo que el censo corrigió en esta KB, en dos sitios a la vez

1. **`verticals/solutions.md`** — el pase 3 escribió que los tres slugs de LawLink eran *«un
   codebase espejado en tres cuentas, ni una bifurcación divergente»*. Hay un **cuarto**:
   **`appleoppa/LawLink`, HEAD `535a3531…` ≠ `4736aa10…`** ⇒ **bifurcación divergente real**, MIT
   1.072 B, mismo titular (叶森 / Sen Ye), **ausente del índice de búsqueda** ⇒ sin estrellas, sin
   `archived`, sin `pushed_at`: **adoptable en licencia, no evaluable en vitalidad.** Y es
   precisamente la que las fuentes secundarias recomiendan («un fork que añade integraciones»).
2. **`repos/foundations.md`** — el pase 3 escribió que `awesome-legaltech` eran *«dos repos distintos
   con nombre idéntico»*. **Son cinco**, y el tercero es un activo nuevo de verdad (abajo).

> 🔧 **G-L7 — una prueba de procedencia sólo es tan completa como el conjunto de candidatos que se
> le pasa, y ese conjunto no sale de una búsqueda web: se censa.** **P16 (identidad de HEAD) es
> ciego al comunal de nombre; P18 (censo) es ciego a los alias no indexados.** Hacen falta los dos,
> y en ese orden.

### Repo nuevo del pase: `apiotrowski-afk/awesome-legaltech-pl` (Polonia)

**CC-BY-4.0 leída, 17.023 B · 14★ · `pushed_at` 2026-11-20** — el más activo de los cinco
`awesome-legaltech`. «Prawo w kodzie»: APIs del **Sejm/ELI, SAOS, CBOSA**, jurisprudencia, servidores
**MCP**, skills de AI y anonimización. **Polonia es jurisdicción nueva en esta KB** (sólo estaba vía
`ContextGem`, que es herramienta, no fuente) ⇒ **EMEA pasa a cinco jurisdicciones con activo propio:
DE, ES, IT, CH, PL.**

**Y es el único índice legal de esta KB que Globant puede derivar:** CC-BY-4.0 permite **uso
comercial y derivados con atribución**, frente a `Vaquill-AI/awesome-legaltech` (**sin licencia**,
273★), `lawve-ai/awesome-legal-skills` (**CC-BY-NC-ND**, 966★) y `chen-friedman` (CC0 pero dormido
desde abril). 🔑 **Se declara con «escala de apertura y control automático de frescura»: automatiza
las dos cosas que esta KB hace a mano cada pase.** Leer su implementación el próximo pase como
**par metodológico**, no como fuente.

### 🔴 G-L9 — el repositorio **VACÍO**: una signatura de canal que ningún control de esta KB detectaba

Descubierto en la verificación final de este pase, sobre una fila que este mismo pase acababa de
publicar como «4 años muerto»: **`JSv4/awesome-legaltech` no está muerto, está vacío.**
**API presente** (4★, `archived=false`, `disabled=false`) · **`size=0`** · **`git ls-remote`
exit 0 con CERO refs** · **`raw` 404** · **`created_at` y `pushed_at` separados por 1 SEGUNDO**.
Creado desde la web, nunca empujado.

**Las dos trampas, en instrumentos que esta KB ya usa:**
1. **`pushed_at` reporta un push que no llevó contenido.** Los tres campos de 932-G6
   (★/`pushed_at`/`archived`) lo publican como *«dormido»*, y dormido **implica algo que forkear**.
   ⇒ **Hace falta `size`, que viaja en el mismo payload y nadie leía** — exactamente el mismo
   patrón de desperdicio que 932-G1 con los bytes de licencia.
2. **`ls-remote` devuelve EXIT 0**, así que es invisible a toda comprobación de error. El script de
   **P16** lo clasifica como *«NO EXISTE (o es privado)»*: **falso en las dos ramas**, y P16
   confunde **tres** estados (inexistente / privado / vacío) en una sola.

**Discriminador gratis: `size == 0` + `created_at == pushed_at`.** Taxonomía de seis estados y
corrección de P16 en `repos/foundations.md` → **G-L9**. **Aplicar en toda la rotación.**

### ⚠️ Corrección a la tabla de bandas del checksum de licencias (932-G1), la primera desde que se importó

La banda heredada de **CC-BY-4.0** era *«~18.650 B»*; este fichero mide **17.023 B** y es CC-BY-4.0
**confirmado por lectura**. ⇒ Banda corregida a **17.000–18.700 B**. Era demasiado estrecha y
**habría producido un falso positivo.** Confirma el caveat del propio método: **los bytes MARCAN, la
lectura DECIDE.** **Propagar a las demás KBs de la rotación.**

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
