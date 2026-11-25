---
industry: legal
region: Global
updated: 2026-11-25
---

# 📈 Agentes trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. No se reescribe: la serie temporal *es* el contenido.

## 🆕 2026-11-25 (pase 12) — el plano de la **propiedad industrial**, y **dos trampas de consulta nuevas** que explican por qué estuvo invisible 11 pases

Sexto plano consecutivo que aparece completo al cambiar de vocabulario (factura → prueba → norma →
acústico → **propiedad industrial**). Censo previo: `patente` **0**, `trademark` **0**, `WIPO` **0**,
`EUIPO` **0**, `Espacenet` **0**, `prior art` **0**, `annuity` **0**, `renewal` **0**.
**34 activos nuevos, 0 solapaban.** Pero lo que vale más que los repos es *por qué* no aparecieron
antes, y esta vez la causa es medible.

### Lo nuevo de esta semana (★ y `pushed_at` medidos 2026-11-25)

| Agente | Licencia (leída) | Región | Qué aporta | ★ |
|---|---|---|---|---|
| [RobThePCGuy/Claude-Patent-Creator](https://github.com/RobThePCGuy/Claude-Patent-Creator) | MIT (1.069 B) | Global | Redacción de solicitud completa | 216 |
| [ip-tools/python-epo-ops-client](https://github.com/ip-tools/python-epo-ops-client) | Apache-2.0 (10.173 B) | EMEA | Cliente EPO OPS, commit de hace 4 días | 197 |
| [ThomasMoreAI/legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | Apache-2.0 (11.314 B) | Global | Biblioteca de *skills* legales, 39 jurisdicciones | 143 |
| [PisenAILab/china-patent-figure-skill](https://github.com/PisenAILab/china-patent-figure-skill) | MIT (1.087 B) | APAC | Dibujos de patente para CNIPA, creado hace 4 semanas | 100 |
| [lsj4232/KR_PATENT_SKILL](https://github.com/lsj4232/KR_PATENT_SKILL) | MIT (1.085 B) | APAC | Redacción de patente coreana | 67 |
| [patent-dev/uspto-odp](https://github.com/patent-dev/uspto-odp) | MIT (1.102 B) | North America | Cliente Go de USPTO ODP, **commit de hoy** | 18 |
| [patent-dev/dpma-connect-plus](https://github.com/patent-dev/dpma-connect-plus) | MIT (1.103 B) | EMEA | Registro alemán DPMA, **commit de hoy** | 2 |
| [angela-125/ST26_sequence-xml-generator](https://github.com/angela-125/ST26_sequence-xml-generator) | MIT (1.067 B) | Global | La **única** implementación permisiva de ST.26 | 0 |

### 🔴 `T-P12-1` — **la abreviatura del sector es casi siempre el significado MINORITARIO del token**

Tres trampas medidas, dos nuevas hoy, y juntas forman una regla que se copia a las doce industrias:

| Consulta | `total_count` | Qué devuelve de verdad |
|---|---|---|
| `ST.96` | **2.683** | Pantallas OLED de **0,96 pulgadas** y placas STM32. El punto se descarta en la tokenización y `96` colisiona con medidas de hardware |
| `ST96` | **9** | Nueve repos de prácticas universitarias (`CCSA-St96105`, `CCSA-ST96166`…). **Cero implementaciones** |
| `phpIP` (web) | — | Casi todo **phpIPAM**, gestión de *direcciones IP* de red. El producto jurídico queda sepultado bajo el de redes |
| `LEDES` (pase 8) | 109.739 | La familia **LED** (WLED 19.102, FastLED 7.539) |

La causa es la misma en los tres casos y no es el buscador: **el sector legal comparte
abreviaturas con el hardware y las redes, y siempre es el lado pequeño del token.** `IP` significa
*propiedad intelectual* para el cliente y *dirección de red* para GitHub; hay cuatro órdenes de
magnitud entre ambos usos.

**Y la variante nueva, que `P31` no cubría:** un estándar cuyo nombre **contiene un punto** no es
consultable por su nombre, en ningún motor, porque el punto se descarta y el número queda suelto.
Afecta a toda la familia WIPO (`ST.96`, `ST.26`, `ST.3`, `ST.9`) y a cualquier estándar con
numeración decimal. La consulta que funciona nunca contiene la abreviatura: es el **sustantivo del
artefacto** (`patent docketing`, `trademark renewal`, `sequence listing`). Receta ampliada en
`compose/patterns.md` `P31`/`P48`.

### 🔴 `T-P12-2` — `T29` se confirma por tercera vez, y aparece la **regla de proporcionalidad inversa**

El pase 8 midió **UTBMS = 0 implementaciones**. El pase 9 lo midió en la capa de estándares de
prueba. Hoy, en la capa de estándares de PI:

- **WIPO ST.96 v9.0** (aprobado por el *XML4IP Task Force* el **2025-04-01**), con seis familias de
  componentes —patente, marca, diseño, indicación geográfica, copyright y comunes— y los esquemas
  publicados por WIPO en ZIP: **CERO implementaciones abiertas.** `wipo xml schema patent trademark`
  devuelve `total_count` **0**.
- **WIPO ST.26**, de uso **obligatorio** para listados de secuencias en solicitudes PCT: **UNA**
  implementación permisiva en todo GitHub, `angela-125/ST26_sequence-xml-generator` (MIT 1.067 B,
  **0★**, 2026-05-26).

Enunciada como regla, y es contraintuitiva: **cuanto más obligatorio es el estándar, menos código
abierto lo implementa.** El motivo es estructural, no casual — un estándar obligatorio crea un
mercado de proveedores que venden el cumplimiento, y la implementación nace *dentro* de ellos y se
queda ahí. Un estándar opcional sobrevive solo si alguien lo adopta por voluntad, y para eso tiene
que ser abierto. **Corolario de planificación:** encontrar 0 implementaciones de un estándar
obligatorio no es señal de que el trabajo no haga falta; es la medida exacta de su alcance.

### 🔴 `T-P12-5` — la capa de **renovaciones** es la capa de responsabilidad civil, y está vacía por segunda vez

`patent annuity renewal deadline` devuelve **1** repositorio, **sin licencia**. `patent docketing`
devuelve 11, de los que los permisivos son dos de **0★** creados en octubre.

Es exactamente la forma del hallazgo del pase 8 sobre el plazo procesal, en un plano distinto: el
olvido de una anualidad **abandona la patente de forma irreversible** en la mayoría de
jurisdicciones —no hay restitución, no hay recurso, y el activo caducado era el más caro de la
cartera—. **Dos planos consecutivos en los que la capa del plazo irreversible es la que menos
herramienta abierta tiene.** Ya no se lee como una carencia del sector de PI: se lee como la regla
de que **el riesgo irreversible no genera software abierto, porque quien lo asume compra seguro y
servicio, no biblioteca.**

## 🆕 2026-11-25 (pase 11) — el plano **acústico**, y la primera exclusión de licencia que esta KB mide **por idioma**

Quinto plano consecutivo que aparece completo al cambiar de vocabulario (factura → prueba → norma →
acústico). Censo previo: `whisper` 0, `diariz` 0, `speech` 0, `audiencia` 0, `oralidad` 0,
`estenotip` 0. **28 activos nuevos, 0 solapaban con la KB.**

### Lo nuevo de esta semana (medido 2026-11-25)

| Agente | Licencia (leída) | Región | Qué aporta | ★ |
|---|---|---|---|---|
| [QuentinFuxa/WhisperLiveKit](https://github.com/QuentinFuxa/WhisperLiveKit) | Apache-2.0 | Global | Transcripción en vivo con diarización, local | 11.294 |
| [moonshine-ai/moonshine](https://github.com/moonshine-ai/moonshine) | ⛔ NOASSERTION (14.180 B) | Global | ASR rápido — **pero el modelo español es no-comercial**, ver abajo | 11.598 |
| [MahmoudAshraf97/whisper-diarization](https://github.com/MahmoudAshraf97/whisper-diarization) | BSD-2-Clause | Global | ASR + atribución de locutor ya ensamblado | 5.676 |
| [speaches-ai/speaches](https://github.com/speaches-ai/speaches) | MIT | Global | API compatible OpenAI: la pieza de migración a on-premise | 3.782 |
| [BUTSpeechFIT/DiariZen](https://github.com/BUTSpeechFIT/DiariZen) | MIT | **EMEA** (Brno) | Diarización europea sin pesos con registro | 573 |
| [revdotcom/fstalign](https://github.com/revdotcom/fstalign) | Apache-2.0 | Global | **Mide** la exactitud del transcript contra una referencia humana | 170 |
| [hwdsl2/scribecrate](https://github.com/hwdsl2/scribecrate) | MIT íntegro (2.304 B) | Global | Servidor offline por diseño. Renombrado desde `docker-whisper` | 125 |
| [gitchrisqueen/hearing-copilot](https://github.com/gitchrisqueen/hearing-copilot) | MIT (1.074 B) | Global | **Único permisivo jurídico-específico del plano.** Litigante autorrepresentado | 0 |

### 🔴 Tendencia nueva `T-P11-1` — **la exclusión de licencia de los modelos de voz es geográfica**

Primera vez que esta KB mide una concesión que **se parte por idioma**. `moonshine` libera código y
modelos streaming bajo MIT, pero deja **español (Base), árabe, japonés, coreano, mandarín, ucraniano
y vietnamita** bajo una licencia que tope el uso comercial en **USD 1.000.000 de facturación anual**.
El inglés queda MIT. Consecuencia operativa: **el mismo repositorio es permisivo en Norteamérica y
no utilizable en LATAM, España, Japón o Corea.** Una auditoría de licencia que mire el repo y no el
*idioma del despliegue* no detecta esto. Receta en `compose/patterns.md` `P44`.

### 🔴 Tendencia nueva `T-P11-2` — **nadie vende exactitud certificada**, y el instrumental existe

Eco exacto del hallazgo de la KB de gaming («nadie vende determinismo como servicio»). El tribunal
no necesita una transcripción *buena*: necesita una **medida**. Lo que existe, permisivo y vivo:
`fstalign` (Apache-2.0, 170★, Rev.com), `jitsi/jiwer` (Apache-2.0, 947★),
`pyannote/pyannote-metrics` (MIT, 260★) y `nryant/dscore` (BSD-2, 273★) — WER palabra a palabra y
DER por locutor contra una referencia. **Ningún proveedor del sector publica su WER sobre audio
judicial.** El entregable que falta no es un ASR: es el **informe de exactitud** que acompaña al
acta.

### 🔴 Tendencia nueva `T-P11-3` — APAC **ya desplegó** lo que Occidente está regulando

Invierte el patrón de los diez pases anteriores, donde APAC era la región de la guía blanda:

- **India**: `TERES` da *speech-to-text en vivo* en audiencias de Sala Constitucional del Tribunal
  Supremo, con texto buscable casi en tiempo real **desde 2023**; pilotos de sala híbrida en
  juzgados de distrito graban **declaraciones de testigos**. El *white paper* del Tribunal Supremo
  admite la AI «para transcripción de actuaciones» siempre que *«los resultados se revisen y
  verifiquen manualmente»*. Kerala opera `Adalat AI` a escala estatal con política formal de uso.
- **Singapur**: `iCTS` (*Intelligent Court Transcription System*) desplegado.
- **China**: los *Smart Courts* combinan OCR + ASR + NLP para transcripción automática.

⚠️ Dos salvedades que se publican: la cifra de «−30% en duración media de juicio» (Stimson Center)
la **matiza la propia fuente** y no se ha verificado contra dato primario; y una comprobación del
**2026-11-03** de la página de *Argument Transcripts* del Tribunal Supremo de India devolvió **«No
records found»** (fuente secundaria), así que *desplegado* no equivale a *publicado de forma estable*.

### 🔴 Tendencia nueva `T-P11-4` — la soberanía del audio ya separa a dos judicaturas LATAM

No es una tendencia prospectiva: **las dos arquitecturas están en producción en la misma región**.
Chile ejecuta `JUSTA`, prototipo del laboratorio de innovación del Poder Judicial, **sobre modelos
de OpenAI** (2–3 minutos por audio, actas en segundos), más `Themis` para transcribir y analizar
audio de audiencias. Argentina anunció transcripción automática de audiencias en el Consejo de la
Magistratura **desde el 28 de octubre, corriendo en servidores propios «para que ninguna información
vaya a plataformas externas»**. Mismo problema, misma región, decisión opuesta sobre dónde vive el
audio privilegiado. **Ahí es donde el stack MIT/Apache gana por construcción**, y es el argumento de
venta más limpio del plano.

### Correcciones de método de este pase

- **`T95` CONFIRMADA, y mi hipótesis contraria descartada antes de publicarla.** Tres repos
  devolvieron `HTTP 422` en `search/repositories` siendo `ls-remote` y `raw` correctos
  (`microsoft/presidio`, `NVIDIA/NeMo`, `alphacep/vosk-models`). Llegué a formular que el índice de
  búsqueda tenía un punto ciego. **Falso:** los tres son renombrados/mudados —
  `microsoft/presidio` → **`data-privacy-stack/presidio`** (12.047★, ya registrado por el pase 9 de
  esta KB), `NVIDIA/NeMo` → **`NVIDIA-NeMo/Speech`** (18.787★, el monorepo se partió por dominios),
  y `alphacep/vosk-models` **no existe** (conjetura propia; el real es `alphacep/vosk-api`).
  **Refinamiento real:** `<nombre> in:name org:<dueño-antiguo>` **falla por diseño** cuando el repo
  ha salido de la organización. El canal de resolución es el redirect o la web, nunca la búsqueda
  acotada al dueño viejo.
- **`T74` cobrada una vez más:** `jianfch/stable-ts` (MIT, **2.290★**) está **`archived`**
  (`push` 2026-05-30). Habría entrado en la tabla por estrellas; lo frenó el campo `archived`.
- **Dormido con buena ficha:** `Stage-Whisper/Stage-Whisper` (MIT, 261★) no tiene commits desde
  **2023-04-27**. `kyutai-labs/delayed-streams-modeling` (Apache-2.0, 3.055★), desde 2026-01-26.
- **Copyleft donde menos se espera:** `linto-ai/whisper-timestamped` (**AGPL-3.0**, 2.859★) es el
  recurso más citado para *timestamps* precisos. Sustituto permisivo medido:
  `MahmoudAshraf97/ctc-forced-aligner` (BSD-2-Clause, 578★, commit de ayer).
## 🆕 2026-11-25 (pase 10) — el plano de la **norma como dato**, y el primer plano que **refuta** a los dos anteriores

Censo de entrada sobre los ocho ficheros, hecho **antes** de consultar nada: `Akoma Ntoso` **0**,
`legislative` **0**, `bill tracking` **0**, `parliament` **0**, `regulatory change` **0**,
`obligations register` **0**, `access to justice` **0**, `cap table` **0**, `land registry` **0**.
Nueve términos, cero ocurrencias en 7.429 líneas. El pase 8 encontró el plano de **la factura**, el
pase 9 el de **la prueba**; este encuentra el de **la norma misma**: el texto legislativo como dato
estructurado, versionado y citable. Es el cuarto plano consecutivo que aparece completo al cambiar
de vocabulario, y **ya no es un hallazgo sobre la industria: es un hallazgo sobre el método.**

### Agentes y clientes nuevos (licencia byte a byte + `ls-remote` + `search/repositories`)

| Agente | Licencia (leída) | Región | Por qué entra | ★ | Último commit |
|---|---|---|---|---|---|
| [CodeandoGuadalajara/dof-rag](https://github.com/CodeandoGuadalajara/dof-rag) | **MIT (1.077 B)** | **LATAM** (México) | RAG sobre el **Diario Oficial de la Federación**. 10 forks, colectivo cívico de Guadalajara. El activo LATAM más maduro de este plano | 25 | 2026-11-02 |
| [lexml/lexml-parser-projeto-lei](https://github.com/lexml/lexml-parser-projeto-lei) | GPL-2.0 (18.033 B) | **LATAM** (Brasil) | **El parser oficial del Senado Federal**. La KB citaba LexML como *fuente que un MCP consulta*; su propio código nunca entró. Activo: commit de hace 8 días sobre un repo de 2013 | 20 | 2026-11-17 |
| [alvarosdev/lex-chile-mcp](https://github.com/alvarosdev/lex-chile-mcp) | **MIT (1.069 B)** | **LATAM** (Chile) | MCP sobre la ley chilena. Llega **11 días antes** de que la Ley 21.719 entre en vigor (ver `intel/market.md`) | 2 | 2026-11-14 |
| [ejaircastillo/InfoLeg-MCP](https://github.com/ejaircastillo/InfoLeg-MCP) | **MIT (1.036 B)** | **LATAM** (Argentina) | MCP sobre **InfoLeg**, el repositorio normativo nacional argentino. ⚠️ Su `LICENSE` son **1.036 B**: por debajo de la banda MIT que esta KB publicaba (1.062–1.090) | 0 | 2026-05-20 |
| [diegoparras/notarum](https://github.com/diegoparras/notarum) | **MIT (1.069 B)** | **LATAM** (Argentina) | Boletín Oficial argentino. Único resultado de los **19** que devolvió su categoría | 2 | 2026-11-20 |
| [LibreCodeCoop/dou-collector](https://github.com/LibreCodeCoop/dou-collector) | **MIT (1.071 B)** | **LATAM** (Brasil) | Recolector del **Diário Oficial da União**, de una cooperativa de software libre. ⚠️ **dormante desde 2024-11-13**: base para forkear, no dependencia viva | 11 | 2024-11-13 |
| [cyanheads/eur-lex-mcp-server](https://github.com/cyanheads/eur-lex-mcp-server) | Apache-2.0 (11.317 B) | **EMEA** | Legislación UE, jurisprudencia del TJUE y grafo **CELLAR** por MCP, **sin API key**. Endpoint sobreescribible ⇒ apunta a un espejo Virtuoso propio | 13 | 2026-11-18 |
| [elconcept/mcp-eu-sparql](https://github.com/elconcept/mcp-eu-sparql) | **MIT (1.082 B)** | **EMEA** | SPARQL de la Oficina de Publicaciones + 57k sentencias del TJUE. **Devuelve CELEX y ECLI en cada cita** ⇒ la cita es verificable por construcción | n/d | n/d |
| [tseidl/eurlex-builder](https://github.com/tseidl/eurlex-builder) | **MIT (1.067 B)** | **EMEA** | CLI que construye *datasets* de EUR-Lex y los enriquece con **ELI**, fechas de adopción y descriptores **EuroVoc** | 9 | 2026-10-17 |
| [cchew/lex-au](https://github.com/cchew/lex-au) | **MIT (1.067 B)** | **APAC** (Australia) | Legislación australiana estructurada. **La plaza de Australia** en el patrón «plantilla por jurisdicción» (`agents/top.md`) | 6 | 2026-11-22 |
| [TBI-AI-Incubator/codify](https://github.com/TBI-AI-Incubator/codify) | Apache-2.0 (11.358 B) | **EMEA** (UK) | Convierte un **corpus legal completo** (PDF, texto o XML) en Akoma Ntoso: adquisición, transcripción, estructuración por anclas, recuperación y comparación. Commit de **hoy** | 15 | 2026-11-25 |
| [portable-genai/obligation-register-kit](https://github.com/portable-genai/obligation-register-kit) | Apache-2.0 (11.344 B) | Global | Descompone una fuente normativa en **obligaciones atómicas** y las mapea a políticas, controles y evidencia en un registro **versionado y append-only**. Commit de hace 2 días | 0 | 2026-11-23 |

### 🔴 `G-L20` — LA LICENCIA QUE EL BUSCADOR AFIRMA Y EL FICHERO NIEGA: primer caso de **licencia bespoke no comercial** de esta KB

El índice de búsqueda web describió [`hendrillara/akoma`](https://github.com/hendrillara/akoma)
—legislación federal brasileña por artículo, para agentes— con la frase literal **«its code is
MIT-licensed»**. Su `LICENSE` son **6.732 B** y empieza así:

```
Akoma Noncommercial and Commercial Licence 1.0
```

No es MIT. No es ninguna licencia OSI. Es un **texto bespoke con frontera comercial**, y
`search/repositories` lo clasifica como `NOASSERTION`, que es exactamente lo que debe hacer. Los dos
canales que esta KB considera fiables acertaron; **el que falló es el que no verifica**.

> **La regla que esto confirma por cuarta vez, y ahora con el peor modo de fallo posible:** una
> afirmación de licencia en prosa —de un buscador, de un *awesome list*, de un README ajeno— **no
> es un dato de licencia**. 6.732 B no caen en ninguna banda conocida: el checksum lo marcó como
> anomalía *antes* de abrir el fichero. Y el daño de confiar aquí no es un enlace roto, es un
> entregable comercial construido sobre material que prohíbe el uso comercial.

### 🧮 Censo de este pase

- **34 direcciones verificadas** antes de escribir: **34/34 existen** (`ls-remote`, refs > 0),
  **32/34 con licencia leída byte a byte**, **2 sin fichero de licencia en ninguna de las 6 rutas
  probadas** (`usgpo/bulk-data` y `SenatoDellaRepubblica/AkomaNtosoBulkData`).
- **2 archivadas, y las dos importaban:** `laws-africa/slaw` (MIT, 28★ — el **único** permisivo del
  stack Akoma Ntoso) y `diegocaro/leychile` (MIT, Chile). Ambas se publican **marcadas como
  archivadas**, no se retiran: siguen siendo referencia de API y base de fork.
- **0 cabeceras como dato, 0 placeholders, 0 columnas descuadradas.**
- **1 anomalía de metadato registrada:** `ejaircastillo/InfoLeg-MCP` declara `pushed_at`
  (2026-05-20) **anterior** a `created_at` (2026-05-22). Ocurre con historia importada. Se publica
  `pushed_at` tal cual se midió y no se deriva antigüedad de él.

### 🔌 Estado de los canales en esta sesión

`gh api search/repositories` ✅ · `git ls-remote` ✅ · `raw.githubusercontent.com` ✅ ·
`gh api search/code` ✅ (no usado este pase) · **`curl -sI github.com` — ⚠️ CAMBIO RESPECTO DE LOS
PASES 6–9:** ya **no** devuelve 403, pero devuelve `HTTP/1.1 200 Connection Established`, que es la
respuesta **del CONNECT del proxy**, no el estado HTTP del recurso. **Es un falso positivo
universal: devuelve «200» también para repos inexistentes.** Hay que medirlo con
`curl -s -o /dev/null -w '%{http_code}'`. ⇒ **La comprobación de URL que prescribe el brief pasó de
ciega (403 para todo) a engañosa (200 para todo). La segunda es peor.** `ls-remote` sigue siendo el
único canal de existencia fiable.

---

## 🆕 2026-11-25 (pase 9) — el plano de la **prueba**: seis categorías con cero menciones, cinco con activos dentro

**Nueve agentes nuevos, todos MIT o Apache-2.0.** Y el pase no los encontró buscando mejor: los
encontró **buscando otras palabras**. El pase 8 descubrió que esta KB consultaba con el vocabulario
del producto jurídico y no con el de la factura. Este pase encuentra el mismo error en un tercer
plano: **el de la prueba** — lo que se conserva, se numera, se redacta, se produce y se certifica.

### 🔴 Lo que estaba declarado cerrado, y no lo estaba

El **pase 2** escribió que el hueco de e-discovery quedaba **cerrado** con `shmsoft/FreeEed`, y dejó
la medición que lo justificaba: `ediscovery OR e-discovery` → 56 repos *«y casi todos son falsos
positivos»*. Esa frase es la prueba del fallo: **se consultó el nombre de la categoría, no sus
artefactos.**

| Término del plano | Menciones previas en la KB | `total_count` | Permisivo dentro |
|---|---|---|---|
| `bates` | **0** | 150 | ✅ 3 (MIT / Unlicense) |
| `load file` / Concordance DAT | **0** | 5 | ✅ 1 (MIT) |
| `legal hold` · `custodian` | **0** | 3 | ✅ 1 (MIT) |
| `deposition` · `transcript` | **0** | 15 | ✅ 3 (MIT) |
| `PAdES` | **0** | 676 | ✅ `pyHanko` 807★ MIT + DSS de la Comisión Europea |
| `privilege log` | **0** | 902 | ❌ **irrecuperable** |
| `ESI protocol` | **0** | **0** | ⚠️ vacía de verdad (medido) |

> 🔑 **Un hueco cerrado con UN activo encontrado por el nombre de la categoría no está cerrado.**
> Está cerrado **el nombre**. Y esta KB tiene más huecos cerrados así: hay que releerlos todos.

### 🔧 G-L18 — `total_count` tiene **dos** patologías opuestas (la tabla completa está en `agents/top.md`)

`G-L17` (pase 8) cubría el caso sobre-restringido: un dígito ⇒ quitar el calificador. Falta el
opuesto: **centenares y todo irrelevante ⇒ el término es un HOMÓNIMO**, y el arreglo es añadir un
sustantivo **del mismo plano**, nunca el nombre del sector. Medido en cuatro casos: `LEDES`→LED,
`bates`→apellido, **`PAdES`→«signature pad»** (676, 7 de los 12 primeros son widgets de firma
táctil), **`privilege log`→escalada de privilegios** (902, `win-brute-logon` 1.174★).

### 🔴 La categoría que NO se pudo rescatar — y es la que el mercado declara en expansión

`privilege log`: 902 resultados, **cero relevantes**. Arreglo intentado:
`privileged document review redaction` → **`total_count` = 0**. Ningún calificador lo recupera.

Y el pronóstico de sector para 2026 nombra **el privilege log** expresamente entre los flujos de
e-discovery que más se automatizan este año. **El flujo que el mercado declara en expansión no tiene
un solo activo abierto localizable.** Hueco **del ecosistema**, medido por dos vías, y se publica
**abierto**.

### Agentes nuevos con señal real (licencia byte a byte + `ls-remote` + `search/repositories`)

| Agente | Licencia | Región | Por qué entra | ★ |
|---|---|---|---|---|
| [cyanheads/courtlistener-mcp-server](https://github.com/cyanheads/courtlistener-mcp-server) | Apache-2.0 (11.317 B) | North America | El **docket** federal vía MCP (opiniones, dockets, jueces, redes de citación). La KB tenía CourtListener como *corpus* (AGPL) y no como acceso procesal | 4 |
| [Decikingship/legal-agent-skills](https://github.com/Decikingship/legal-agent-skills) | MIT (1.081 B) | **China** · APAC | **La plaza de China en el patrón «plantilla por jurisdicción»**: 60 skills + 33 flujos expertos, **con evaluaciones** | 23 |
| [jordanteague/judgment-compiler](https://github.com/jordanteague/judgment-compiler) | MIT (1.070 B) | Global | Compila criterio experto en playbooks validados: **el humano fija la regla, la AI la ejecuta** | 12 |
| [GSkuza/AI-Legal-SkillsPL](https://github.com/GSkuza/AI-Legal-SkillsPL) | MIT (1.063 B) | **Polonia** · EMEA | Segundo activo polaco permisivo tras `kancelaria-lex` | 7 |
| [TaylorLegalEngineering/deposition-contradiction-analysis](https://github.com/TaylorLegalEngineering/deposition-contradiction-analysis) | MIT (1.086 B) | North America | Contradicciones en actas de deposición, salida citada a línea | 2 |
| [noamrazbuilds/legal-hold-manager](https://github.com/noamrazbuilds/legal-hold-manager) | MIT (1.090 B) | North America | **Primer activo de *legal hold*** de la KB: la obligación anterior al e-discovery | 1 |
| [Mermiges/depo-summarizer](https://github.com/Mermiges/depo-summarizer) | MIT (1.070 B) | Global | Resumen de deposición **con LLM local** (testimonio bajo juramento no sale del despacho) | 0 |
| [crowaltz24/DepoIndex](https://github.com/crowaltz24/DepoIndex) | MIT (1.062 B) | Global | Índice por temas y testigos para preparar juicio | 0 |
| [juraj-jumic/eidas-validator](https://github.com/juraj-jumic/eidas-validator) | MIT (1.068 B) | **UE** · EMEA | Validación eIDAS **en lenguaje llano** sobre la capa `pyHanko`/DSS | 0 |

### 🧮 Censo de este pase

- **19 direcciones verificadas** antes de escribir: 19/19 existen (`ls-remote` refs > 0), **0
  archivadas**, 19/19 con licencia leída byte a byte.
- **Checksum de licencias (932-G1), 19/19 coherente:** banda MIT **1.062–1.090 B** (12 casos),
  Apache-2.0 **11.317 B**, GPL-3.0 **35.149 B**, AGPL-3.0 **34.523 B**, **LGPL-2.1 26.530 B
  (banda nueva, primer caso de esta KB)**, EUPL-1.2 **13.832 B (banda nueva)**, Unlicense **1.211 B
  (banda nueva)**.
- **Un caso de título engañoso:** `DepoIndex/LICENSE.md` empieza en `Copyright (c) 2025` **sin** la
  línea `MIT License`; cuerpo MIT íntegro. El clasificador acertó, el título engaña.
- **0 filas de cabecera como dato, 0 placeholders, 0 columnas descuadradas** (barrido `G-L11`:
  **142 bloques de tabla, 0 defectos**).

### 🔌 Canales: una pérdida nueva que afecta a todo lo regulatorio

`curl -sI github.com` sigue devolviendo **403 para todo** (ciego, como en los pases 6–8). **Nuevo:
`WebFetch` a fuentes legales primarias falla con `ENOTFOUND`** — `boe.es` y
`edomex.quadratin.com.mx` están fuera de los dominios permitidos de la sesión. ⚠️ **Por tanto las
normas citadas en `intel/` de este pase están verificadas por UN canal (el índice de búsqueda) y NO
contra el texto oficial. Se publican marcadas.**

---

## 🆕 2026-11-22 (pase 8) — el caudal **no estaba seco**: estaba en un plano que esta KB nunca consultó

**Tres agentes MIT nuevos, los tres en facturación legal, y los tres creados en las últimas 12
semanas:** `billcheck` (2026‑11‑19, hace **tres días**), `aderant-legal-billing` (2026‑11‑06),
`billing-lint` (2026‑08‑31). Los tres con **0★**.

### 🔴 Y eso refuta una tendencia que esta KB publicó y confirmó tres pases seguidos

`T-P5-1` dice, con medición: *«el caudal de activos legales nuevos se ha secado»* — `legal AI
created:>2026-09-01 stars:>=40` → 4 repos; `legal AI created:>2026-08-01 stars:>=25` → 10, de los
que 0 eran incorporaciones netas. Medido otra vez hoy, sigue siendo cierto. **Y aun así el caudal
no estaba seco.**

Las dos consultas comparten dos supuestos que no son del ecosistema, sino del instrumento:

1. **El término `legal`.** Un repo que implementa LEDES 1998B no necesita decir «legal»: el nombre
   del estándar ya lo dice. Filtrar por `legal` no mide pertinencia, mide **si el autor fue
   redundante**.
2. **Un umbral de estrellas.** `stars:>=25` elimina por definición a los tres hallazgos de hoy, que
   tienen cero. Es `G-L10` otra vez —filtro de precisión usado como filtro de cobertura— pero ahora
   con una causa añadida: en el plano de ingresos **no hay público que estrelle**. Quien factura
   horas no navega GitHub; el repo no tiene demo viral ni modelo que probar.

> 🔑 **La conclusión correcta, y hay que corregirla en los dos sitios donde está escrita:** lo que
> tres pases midieron no es *«el ecosistema legal dejó de producir»*, sino **«el vocabulario de esta
> KB dejó de producir»**. Una serie temporal estable es una propiedad del instrumento hasta que se
> cambia el instrumento. `T-P5-1` queda **acotada**, no retirada: es cierta *dentro del plano del
> producto jurídico*, y falsa fuera de él.

### 🔧 G-L17 — AÑADIR LA PALABRA DEL SECTOR AL NOMBRE DE UN ESTÁNDAR SECTORIAL **ES UN FILTRO, NO UNA ACLARACIÓN**

El hallazgo de método del pase, y se mide con tres llamadas:

| Consulta | `total_count` | ¿Aparece `billcheck`, el mejor activo (MIT)? |
|---|---|---|
| `LEDES` | 109.739 | ❌ sepultado — el tokenizador lo solapa con la familia `led` (`WLED` 19.102★, `FastLED` 7.539★) |
| **`LEDES invoice`** | **26** | ✅ **sí** — y con él `ruhee-g/LEDES98B`, `bkattenburg/ledes-invoice-generator`, `roipatents/CrispLEDES` |
| `LEDES legal billing` | 6 | ❌ **no** — y tampoco ninguno de los otros cinco |

La consulta que **el propio brief prescribe** (`{estándar} {industria} {función}`) devuelve el
conjunto más pequeño y **pierde el único activo permisivo de la categoría**. El punto óptimo es
`{estándar} + {sustantivo del artefacto}`: `LEDES` + `invoice`, no `LEDES` + `legal`.

> **Regla para las doce industrias, porque todas tienen estándares con esta propiedad:** *cuando el
> término de búsqueda es el nombre de un estándar sectorial, **no se le añade el nombre del
> sector**; se le añade el artefacto que el estándar describe.* Aplica igual a `HL7`/`FHIR` +
> *record* (salud), `ISO 20022` / `SWIFT MT` + *payment* (financiero), `EDIFACT` + *order*
> (retail), `IEC 61850` + *substation* (energía), `OpenTravel`/`NDC` + *booking* (viajes). Y el
> síntoma de que se ha caído en la trampa es exactamente el de hoy: **un `total_count` de un solo
> dígito que parece confirmar que la categoría no existe.**

### Agentes nuevos con señal real (verificados por tres canales: licencia byte a byte, `ls-remote`, `search/repositories`)

| Agente | Licencia | Por qué entra |
|---|---|---|
| [unhingedpanda/billcheck](https://github.com/unhingedpanda/billcheck) | MIT (1.080 B) | Único parser/constructor/validador **LEDES 1998B** permisivo. Cero dependencias de runtime. Validador local **por construcción**: sin endpoint de subida, sin analítica, servidor atado a `127.0.0.1`, CSP que bloquea conexiones salientes |
| [itsoumya-d/aderant-legal-billing](https://github.com/itsoumya-d/aderant-legal-billing) | MIT (1.071 B) | **Cuentas de terceros** — la salvedad que el pase 6 anotó entre paréntesis y nadie buscó. Libros de cliente que no pueden quedar en descubierto, WIP, tarifarios, export LEDES |
| [kirillsakhin/billing-lint](https://github.com/kirillsakhin/billing-lint) | MIT (1.070 B) | Linter determinista de pre-factura sobre CSV/XLSX/LEDES, **incluida validación de códigos UTBMS** |
| [oktopeak/mycase-mcp](https://github.com/oktopeak/mycase-mcp) | MIT (1.065 B) | Puente MCP al practice management que el despacho **ya paga**. 6★ |

### 🧪 Y un dato de ingeniería que vale más que los cuatro repos juntos

`billing-lint` documenta, en su propio README, por qué su arquitectura pone las reglas antes que el
modelo: **la revisión por LLM en lote es inconsistente** — *«el mismo defecto se marca en la entrada
3 y pasa callado en la entrada 47, y dos ejecuciones del mismo extracto se contradicen; revisar 400
entradas en un solo prompt lo empeora, no lo mejora»*.

> Es la primera afirmación **operativa y específica del sector** sobre no determinismo que entra en
> esta KB, y encaja con lo que el pase 3 ya había registrado por el lado de la calidad (la
> trazabilidad desplaza a la fluidez). En facturación el efecto es económico y directo: un defecto
> que pasa en la entrada 47 **se factura**, llega al cliente y vuelve como ajuste. De ahí el orden
> correcto: **reglas deterministas primero, modelo sólo donde cabe un juicio.**

### ⚠️ Lo que este pase NO midió, y hay que decirlo

- **Ningún activo del plano de ingresos está anclado en LATAM.** Se buscó (`LEDES`, `UTBMS`,
  facturación y cuentas de terceros) y no aparece ninguno con origen en la región. Ver `intel/market.md`
  para por qué el hueco importa **menos** de lo que parece y dónde está el trabajo real.
- **Los tres activos MIT tienen un solo autor y cero forks.** Son bases de referencia y de lectura,
  no proyectos con comunidad. Lo que se promete a un cliente es **el código leído**, no el mantenimiento.
- `billcheck` tiene **tres días de vida**. Se publica por función verificada (`P23`), con la fecha a
  la vista y sin ninguna afirmación sobre su continuidad.

## 🆕 2026-11-22 (pase 7) — el líder comercial publicó su banco de pruebas en MIT, y esta KB lo tenía perdido desde mayo

**`harveyai/harvey-labs` — Harvey LAB, «Legal Agent Benchmark». MIT (1.067 B byte a byte), 1.668★,
último commit 2026-11-12, 258 refs.** Lo publica **Harvey**, la compañía de 11.000 M USD que esta
KB usa como referencia del competidor cerrado. Contiene **2.010 tareas** sobre **24 áreas de
práctica + contratación in-house**, con rúbricas, **más el harness de ejecución** (sandbox,
adaptadores de Anthropic/OpenAI/Google/Meta/xAI, *grader* con juez LLM, informes y *sweeps*),
empaquetado como librería `lab-core`.

Lo relevante como *trending* no es la novedad —se lanzó en **mayo de 2026**— sino **la velocidad
y el hecho de que seis pases de esta KB no lo vieran**:

| Hito | Tareas | Fuente |
|---|---|---|
| Lanzamiento (mayo-2026) | >1.200 · 24 áreas · >75.000 criterios de rúbrica | anuncio de Harvey |
| Leaderboard de Mercor | 1.749 · +100.000 criterios | Mercor APEX |
| **Medido hoy (2026-11-22)** | **2.010** | badge del `README` del repo |

**+67% de tareas en seis meses.** Un benchmark que crece así es infraestructura mantenida.

### 🔴 Y el hallazgo que lo acompaña: la capa de evaluación que esta KB **sí** citaba estaba mal atribuida

`LegalBench` aparecía en tres ficheros como base de evaluación «MIT». **No lo es:** no tiene
fichero de licencia (5/5 → 404) y la licencia va **por tarea**. Enumeradas las 162: **124 CC BY
4.0, 4 MIT, 2 CC BY-SA, 30 NonCommercial y 2 sin concesión** ⇒ **32 tareas (19,8%) no son
utilizables en un entregable comercial**. Detalle, lista de exclusión por prefijo y receta
reproducible en `repos/foundations.md` y `compose/patterns.md` (`P26`).

### 🗑️ Candidatos descartados este pase, con la medición que lo justifica

| Candidato | Medición | Por qué no entra |
|---|---|---|
| [`sdpong/legal-debate-agents`](https://github.com/sdpong/legal-debate-agents) | **0★**, NOASSERTION, 2026-09-23 | Apareció en un agregador (Trendshift) como legal-AI trending. Sistema de debate multi-modelo con cadena de auditoría sobre reglas de disputas de la OMC: **temáticamente encaja**, pero **0 estrellas y sin concesión de licencia**. Se registra como candidato a re-test, no como fila. |
| `coasty-ai/coasty-legal-docket-research` | **422** en `search/repositories` | Citado por un agregador. 422 **no distingue** renombrado de inexistente, y no hay slug canónico que verificar. Sin segundo canal, no entra. |
| [`mattwang1230/legal-paper-framework-humanizer-zh`](https://github.com/mattwang1230/legal-paper-framework-humanizer-zh) | 53★, MIT, 2026-08-18 | MIT limpio, pero su función es **quitar «sabor AI» a artículos académicos de derecho en chino**. Es escritura académica, no trabajo jurídico: lo rechaza la puerta de relevancia `P15`. |
| [`cakho6179/AI_RAG_LEGAL`](https://github.com/cakho6179/AI_RAG_LEGAL) | 71★, **NOASSERTION**, 2026-08-10, **sin `description`** | Tracción real pero **sin descripción declarada**: no se puede afirmar qué hace. Candidato a auditar (mismo tratamiento que `Paparusi/legal-ai-agent`). |

> ⚠️ **Nota de método sobre los agregadores.** Tres de los cuatro candidatos de arriba llegaron por
> agregadores de *trending*, y **tres de los cuatro no pasaron la verificación**. El pase 6 añadió
> los agregadores como canal independiente y acertó; este pase mide su **precisión**: dan nombres
> útiles, y **la tasa de acierto es baja**. Son un canal de *cobertura*, nunca de *verdad*.

---

## 🆕 2026-11-21 (pase 6, 21:40 UTC) — cuatro MCP de fuentes oficiales LATAM que esta KB declaraba inexistentes, y el motivo del falso negativo

**El pase 5 cerró escribiendo qué faltaba hacer:** *«STILL PENDING: el hueco más citado de esta KB,
"no LATAM official-source MCP", nunca se buscó fuera de GitHub.»* Se buscó hoy. **El hueco no
existía.** Cuatro activos permisivos, licencia leída byte a byte, en **una sola búsqueda**:

| Activo | Licencia (leída) | País | Qué cubre | ★ |
|--------|------------------|------|-----------|---|
| [matematicsolutions/br-eli-mcp](https://github.com/matematicsolutions/br-eli-mcp) | Apache-2.0 (11.358 B) | 🇧🇷 Brasil | 8 APIs oficiales **sin clave**: Câmara, Congresso (+ publicación en DOU), `normas.leg.br`, **DataJud/CNJ**, **STJ**, **CARF**, **TST**, **TCU** | 4 |
| [mazulo/leis-mcp](https://github.com/mazulo/leis-mcp) | MIT (1.071 B) | 🇧🇷 Brasil | **1.218.990 normas** con fuente oficial y **avisos de revogação**; valida vigencia contra normas.leg.br + Senado | **71** |
| [ivancaron/jurismcp](https://github.com/ivancaron/jurismcp) | MIT (1.078 B) | 🇧🇷 Brasil | **Jurisprudencia**: STJ, STF, TST, TJES, **LexML** (`urn:lex`), **BNP/CNJ**, TNU, TRF4 | 2 |
| [BEG-lag/mcp-dof](https://github.com/BEG-lag/mcp-dof) | MIT (1.082 B) | 🇲🇽 **México** | **Diario Oficial de la Federación** sobre la **API oficial SIDOF**: ediciones diarias, decretos íntegros, FIX/UDIS/TIIE | **0** |

Y dos más del mismo barrido:

| Activo | Licencia (leída) | Por qué entra | ★ |
|--------|------------------|---------------|---|
| [daniel-filius/awesome-mcp-brasil](https://github.com/daniel-filius/awesome-mcp-brasil) | **CC0-1.0** (7.048 B) | Directorio auto-verificado de MCP y skills **de Brasil**: *Jurídico/Legislativo* **13 entradas**, Dados públicos 24, Fiscal 7, Pix 8, Eleições 7, Skills BR 5, Guias PT 6. **CC0 = dominio público: derivable para material de cliente sin atribución.** Es, además, **un canal de descubrimiento** que esta KB no tenía. | 0 |
| [rohasnagpal/legal-ai-skills](https://github.com/rohasnagpal/legal-ai-skills) | MIT (1.069 B) | **244 skills legales permisivas** bajo 17 especialistas + Managing Partner que enruta; *Jurisdiction Counsel* para India, EE. UU., RU y **Singapur (18 skills locales)**. Alternativa usable a `lawve-ai/awesome-legal-skills` (CC-BY-NC-ND, 966★). | **214** |

### 🔴 El hallazgo del pase: el fallo no fue de rigor, fue de **independencia de canal** (G-L12)

Esta KB escribió «verificado por los dos canales». Los dos canales eran `search/repositories`
(índice de GitHub) y lectura de `LICENSE` en `raw.githubusercontent.com` (ficheros de GitHub).
**Para descubrir, son un solo canal.** Dos consultas al mismo índice comparten su sesgo de idioma
y dan un falso negativo con la misma confianza que una.

Y la causa concreta **no es la tracción**: `leis-mcp` tiene **71★**, más que 9 filas que esta KB ya
recomendaba. Es el **idioma del sustantivo**: la KB buscó los *flujos* en portugués (*agente
jurídico*, *assistente*) pero las *fuentes* sólo en inglés. Faltaban `legislação`,
`jurisprudência`, `Diario Oficial`. Detalle completo y las dos reglas nuevas en `agents/top.md`
→ PASE 6.

### 🟡 Y el que se registra para que no se confunda con los cuatro

[mcp-dir/jusbrasil-mcp](https://github.com/mcp-dir/jusbrasil-mcp) (MIT, 1.093 B) es un **agregador
de terceros** — se describe como «alternativa a Escavador y Jusbrasil» — **no fuentes oficiales**.
Su posicionamiento lo pone primero en cualquier búsqueda de «MCP jurídico Brasil», así que un pase
futuro lo encontrará **antes** que a los oficiales. Para citación defendible no sirve. Nótese que
`jurismcp` hace esta misma distinción por su cuenta: marca Jurisprudencias.ai como agregador y lo
deja **opt-in**.

### ⚠️ Lo que este pase NO pudo medir, y hay que decirlo

- **Renombrados: no comprobados.** El oráculo que el pase 3 prescribió para toda la rotación
  (identidad de HEAD por `git ls-remote`) **devuelve 0 refs para todo en esta sesión**, y
  `search/repositories` responde **422**. Las 83 URLs resuelven, pero `raw` sigue redirects de
  renombrado ⇒ **vivas sí, comprobadas contra renombrado no.**
- **`pushed_at`: no medido.** Sin `search/repositories` no hay fecha de último commit para las
  filas nuevas; van con `n/d ⚠️` en vez de con una fecha inventada.
- ⇒ **Regla nueva:** el juego de canales **cambia entre sesiones**. Primera acción de cada pase:
  sondear cada canal con un par conocido-bueno / conocido-malo. Tabla comparativa pase 5 vs pase 6
  en `agents/top.md`.

### ✅ Integridad

83/83 URLs resuelven · 86→88 bloques de tabla, **0 defectos** (`P22` aguanta) · 7/7 lecturas de
licencia dentro de banda del checksum 932-G1 · 0 filas repintadas por deriva de estrellas
(anti-churn del pase 5) · append-only respetado.

## 🆕 2026-11-21 (pase 5, 01:38 UTC) — tres agentes MIT nuevos, y el hueco que esta KB declaraba abierto estaba cerrado desde el 1 de noviembre

**Quinto pase sobre `legal` en 28 horas** (22:01, 22:55, 00:01, 00:53 y este). Los cuatro anteriores
no avanzaron `rotation.json`, así que la rotación reincidió cinco veces en la misma industria.
**Corregido en este pase.** Consecuencia metodológica: las métricas tenían **una hora** de vida, así
que este pase **no las reescribió** — las midió, confirmó que no había deriva, y gastó el
presupuesto en lo que faltaba.

### 📏 Primero, la medición que justifica no haber reescrito nada

Barrido completo de las **75 URLs de GitHub** de la KB por `search/repositories`:

| Resultado | Cuenta |
|---|---:|
| Resuelven con metadatos frescos | **72** |
| Devuelven 422 (y los 3 son los renombrados ya documentados: `microsoft/presidio`, `JSv4/OpenContracts`, `lowtidebuild/contract-review-agent`) | **3** |
| Filas de la tabla actual con deriva de estrellas **> +1** | **0** |
| Repos marcados `archived` | **0** |

⇒ **Confirma las mediciones del pase 4 una hora después.** La deriva máxima observada en filas
vigentes fue **+1★** (6 filas). Reescribir 6 números para sumar 1 estrella cada uno habría sido
churn: *un pase que sólo repinta cifras frescas no añade información, y oculta que no añadió nada.*

### Agentes nuevos con señal real (los tres MIT, verificados por los dos canales)

| Agente | Repo | Licencia (leída) | Región | Por qué entra | Stars |
|---|---|---|---|---|---:|
| **kancelaria-lex** | [AI4CharityPL/kancelaria-lex](https://github.com/AI4CharityPL/kancelaria-lex) | **MIT** (1.069 B) | **Polonia** · EMEA | **El mejor activo del pase.** Localidad **impuesta por arquitectura** (4 segmentos Docker, 3 con `internal: true`: no hay ruta a la pasarela) + **integridad de cita por construcción** (reconstrucción del texto desde el documento fuente y comparación **carácter a carácter**). Declara **0 citas inconsistentes con la fuente en todas las corridas** y >80% de precisión, contra el **17–34%** de fabricación de las comerciales. | 60 |
| **Kourti Legal** | [boyeesu/Kourti](https://github.com/boyeesu/Kourti) | **MIT** (1.069 B) | **Nigeria** · EMEA | **Cierra el hueco de practice management permisivo** y es el **primer activo africano** de esta KB. 524 refs, React+Node+PostgreSQL, CI, self-hosting documentado. ⚠️ 1★. | 1 |
| **legal-agent-workshop** | [meta-models/legal-agent-workshop](https://github.com/meta-models/legal-agent-workshop) | **MIT** | Global | **Enablement ejecutable**: construye un agente legal y luego **la capa de verificación que corre FUERA del control del agente** (checklist contra verdad de base + reglas del memo), con rechazos, escalado y **firma del abogado**. Caso de trabajo incluido. | 73 |

### 🔴 El hallazgo del pase: el pase 4 declaró inexistente un repo que existe, y el hueco llevaba 20 días cerrado

El pase 4 escribió, en negrita: *«**«Kourti Legal» no existe.** (…) **No hay tal repo.**»* — citando
a la vez el slug correcto, `boyeesu/Kourti`, y su licencia MIT. **El repo existe desde antes del
1-nov-2026.** Lo que el pase 4 midió fue **1★**, y de ahí concluyó inexistencia.

| Canal | Qué dice de `boyeesu/Kourti` |
|---|---|
| Contador de estrellas | 1★ ⇒ *parece* nada |
| `git ls-remote` | **524 refs**, ramas de release y de remediación CodeQL ⇒ código real |
| `raw` + bytes | MIT, **1.069 B** ⇒ licencia genuina |
| README | matters, documentos, clientes, plazos; React+Node+PostgreSQL; `docker compose`; `SECURITY.md` |

⇒ **G-L10, y aplica a toda la rotación:** las estrellas y la `description` son filtros de
**precisión**, no de **cobertura**. Usarlos para decidir *qué mirar* produce falsos negativos
silenciosos; usarlos para *declarar un hueco* convierte un falso negativo en una conclusión
publicada. **Todo hueco de la forma «no existe X permisivo» debe releerse como «no existe X
permisivo con señal social».** El gate de pertinencia **P15** de esta KB **rechaza** a `Kourti`,
porque el repo no tiene `description` ni `topics`: el control más citado de esta KB es el que lo
habría descartado.

### 🧮 Dos corroboraciones del checksum de licencias (932-G1), una por cada lado de la regla asimétrica

| Repo | Licencia declarada | Bytes | Lado de la regla | Qué se encontró al leerla |
|---|---|---:|---|---|
| [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | GitHub: `NOASSERTION` | **35.051** | **por encima** de la banda AGPL (~34.500) ⇒ «compuesta» | ✅ **Compuesta**: AGPL-3.0 + carve-out de `apps/OpenSignServer/cloud/customRoute` + terceros |
| [mayan-edms/Mayan-EDMS](https://github.com/mayan-edms/Mayan-EDMS) | GitHub: `NOASSERTION` | **586** | **muy por debajo** de la banda Apache (11.300–11.400) ⇒ «puntero, sigue el puntero» | ✅ **Puntero Apache-2.0** genuino. **GitHub se equivoca; la regla acierta.** |

**La regla predijo el contenido de los dos ficheros antes de abrirlos, y en los dos casos corrigió
la clasificación de GitHub.** Vale la pena repetirlo porque es el lado útil: `NOASSERTION` **no**
significa «sin licencia», significa «el clasificador no pudo».

### ⚠️ Un no-hallazgo que sigue haciendo falta registrar: la desinformación sobre `openclaw` ya está indexada

El pase 3 descartó `openclaw` como proyecto **no legal** (colisión de substring: «openc-**law**»).
Hoy, una búsqueda de «github trending legal AI 2026» devuelve un artículo de prensa tecnológica que
afirma que **openclaw es un proyecto de legal AI open source que desbancó a React como repo más
estrellado de GitHub**. **Es falso en la parte legal.** ⇒ El descarte del pase 3 no sólo sigue
vigente: **ahora hay una fuente indexada que empujaría a cualquier pase futuro a readoptarlo.**
El gate de pertinencia P15 se queda.

---

## 🆕 2026-11-21 (pase 4) — las 7 filas del pase 3 resisten la auditoría, y aparece un modo de fallo que los tres controles de esta KB no ven

**Este pase audita al pase 3, que a su vez auditaba al pase 2.** Y encuentra la asimetría
estructural de la rotación: **cada pase revalida al anterior y publica sin revalidar lo que añade.**
Las **7 filas nuevas del pase 3 no las había comprobado nadie.** Comprobadas hoy por los dos
canales: **7/7 confirmadas, 0 errores de dato.** Primer pase de esta KB que audita y no corrige
nada — la señal de que el método de dos canales ya está estabilizado.

### 🔴 Lo que sí aparece: *embudo de venta* (G-L8)

`zubair-trabzada/ai-legal-claude`, **1.852★**, era *«el segundo repo de agente legal más estrellado
tras `claude-for-legal`»*. Su `description` **termina en** *«If you want to learn how to sell this
to real businesses, check out the **Skool community**»*: **el repo es el gancho de captación de una
comunidad de pago.** Sin fichero de licencia, 8 meses sin commits.

**Lo que esto obliga a cambiar:** el embudo **pasa los tres controles que esta KB ya tiene**
(existencia ✓, pertinencia ✓ —habla de contratos y NDAs en sus propias palabras—, estrellas ✓).
Falta un **cuarto**: *¿por qué tiene estas estrellas?* ⇒ Leer la `description` **completa** buscando
llamada a la acción comercial; el patrón firma es **estrellas altas + sin licencia + dormido**.
**No tiene nada de legal: aplicar en todas las industrias de la rotación.**

### Mediciones del pase (todas por `search/repositories` + lectura de LICENSE)

| Repo | Medido hoy | Cambio desde el pase 3 |
|------|-----------|------------------------|
| `anthropics/claude-for-legal` | Apache-2.0, **10.054★**, 2026-11-19 | sin cambio |
| `stella/stella` | Apache-2.0 (11.358 B ✓ banda), ★282, **`pushed_at` 2026-11-21** | **commit de hoy otra vez** — segundo día consecutivo |
| `open-legal-products/mike` | AGPL-3.0, **4.504★**, 2026-11-19 | sin cambio |
| `Lethe044/hermes-legal` | MIT, ★26, 2026-10-10 | **dato nuevo**: corre con *free tiers* de Groq/Gemini **o totalmente offline, sin API key** |
| `Paparusi/legal-ai-agent` | MIT, ★214, 2026-03-21 | **`description` vacía confirmada por API**: la cautela del pase 3 era correcta |
| `CSlawyer1985/contract-review-pro` | **NONE**, ★311, 2026-08-14 | sin licencia confirmado |
| `FuturixAI…/Prism-Legal-OS` · `JustVugg/judicex` | AGPL-3.0 ★226 · Apache-2.0 ★69 🪦 | sin cambio |

**Ningún agente legal nuevo relevante entró esta hora.** Las consultas globales de agentes
devolvieron **listas de agentes de propósito general** (OpenClaw, OpenHands, CrewAI, LangChain,
OpenCode) — el mismo ruido de categoría que el pase 3 nombró como *blanqueo de categoría* (G-L5).
**Se registra como medición, no como ausencia de búsqueda.**

## 🆕 2026-11-21 (pase 3) — los cuatro laboratorios frontera ya tienen vertical legal, y el repo legal nuevo más estrellado no tiene licencia

**Este pase es una auditoría del pase 2, no una reescritura.** Las 33 filas del pase 2 se
revalidaron una por una (★, `pushed_at`, `archived`, licencia byte a byte) y **se confirman**, con
desviación máxima de +1★. Lo que cambia son **un slug muerto, un diagnóstico de método y tres
campos de una fila** — más 7 filas nuevas. Detalle en `agents/top.md`.

### 🔴 El movimiento de mercado del pase: cuatro verticales legales en seis meses

| Producto | Lab | Fecha | Forma |
|----------|-----|-------|-------|
| **Claude for Legal** | Anthropic | **2026-05-12** | Suite de skills/plugins + despliegue por Managed Agents API. **Y es el único con repo open source: `anthropics/claude-for-legal`, Apache-2.0, 10.054★.** |
| **Gemini Enterprise for Legal** | Google Cloud | **2026-08-25** (preview) | Plataforma gobernada. Clientes de lanzamiento: Cleary, Freshfields, Weil, Williams & Connolly. Integra iManage, NetDocuments, DocuSign, Everlaw, RelativityOne, HighQ, **CourtListener**, Harvey, Legora. |
| **Astra for Law** | OpenAI | **sep-2026**, GPT-6 Astra → hoy GPT-6.2 | Abierto a **todos los clientes de ChatGPT Enterprise** (ampliación de ~18-nov-2026). Reclama la mejor puntuación en un benchmark de agentes legales **de Harvey** — es afirmación de parte, no resultado independiente. |
| **Copilot for Legal** | Microsoft | **oct-2026** | **20+ skills legales dentro de Word** y Cowork: revisión de contratos, redacción, seguimiento de obligaciones. |

**Los cuatro tienen la misma arquitectura:** un paquete de *skills/agentes legales* + un juego de
*conectores* hacia los productos que el abogado ya usa. **Ninguno trae corpus jurisdiccional
propio.**

⇒ **Consecuencia directa para Globant, y es la lectura comercial más importante del pase:**
«construimos un asistente legal» **dejó de ser diferenciador en seis meses** — los cuatro
laboratorios lo regalan con la licencia de empresa. Lo que **no** traen, y es exactamente donde
están los activos verificados de esta KB: **fuentes oficiales por jurisdicción** (`korean-law-mcp`,
`mcp-legal-it`, `ayunis-legal-mcp`, `opencaselaw`, `devnors-data-mcp`, `mcp-taiwan-legal-db`),
**despliegue self-hosted con residencia de datos** (`CaseCite`, `doc-haus`, `stella`) y **derecho
no anglosajón**. Ver `intel/market.md` → posicionamiento.

> 📌 **Dos señales dentro de la tabla que conviene no pasar por alto.**
> 1. **Google integra `CourtListener`** — un proyecto AGPL-3.0 de esta misma KB — como conector de
>    primera clase. El corpus abierto ya no es «la alternativa barata»: es **infraestructura dentro
>    del producto del hiperescalador.**
> 2. **Microsoft mete 20+ skills legales dentro de Word.** Esta KB sostiene desde el primer pase
>    que *el canal decisivo es Word*; ahora el canal lo ocupa Microsoft en persona. La contraparte
>    permisiva de la KB (`Vaquill-AI/ms-word-addin`, Apache-2.0, 81★) pasa de «cierra un hueco» a
>    **«compite con el dueño del procesador de textos»**: sigue siendo la opción correcta cuando el
>    cliente necesita control del add-in y de los datos, no cuando sólo quiere la función.

### Agentes nuevos con señal real (verificados por los tres canales)

| Agente | Licencia (leída) | Región | Señal | Stars |
|--------|------------------|--------|-------|-------|
| [stella/stella](https://github.com/stella/stella) | Apache-2.0 (11.358 B) | Global | Workspace legal permisivo **con commit de hoy**, bajo cuenta de organización. El candidato vivo del pase. | 282 |
| [FuturixAI…/Prism-Legal-OS](https://github.com/FuturixAI-and-Quantum-Works/Prism-Legal-OS) | AGPL-3.0 ⚠️ (34.523 B) | India · APAC | Contratos + research + litigio en un sistema. 2.º activo legal de India en la KB. | 226 |
| [JustVugg/judicex](https://github.com/JustVugg/judicex) | Apache-2.0 (11.357 B) | Global | «Respuestas verificables» y redacción fundada en evidencia — el vocabulario de la tendencia dominante, permisivo. 🪦 6 meses dormido. | 69 |
| [Lethe044/hermes-legal](https://github.com/Lethe044/hermes-legal) | MIT (1.065 B) | Global | Puntúa riesgo y **emite recomendación de firmar/negociar**: la decisión de negocio como salida, no el análisis. | 26 |

### 🔴 Y la advertencia del pase: ~2.500★ de material legal nuevo sin licencia

Los tres repos legales **nuevos** con más tracción **no tienen fichero de licencia** (verificado
por dos canales, cinco nombres de fichero):
`zubair-trabzada/ai-legal-claude` (**1.852★**), `Ramseygithub/ai-legal-compliance-assistant` (342★)
y `CSlawyer1985/contract-review-pro` (311★). Sin licencia expresa el default es **todos los
derechos reservados**. Los tres son *skills/prompt packs*, no librerías: **el formato nuevo del
sector trae un déficit sistemático de licencia**, y las estrellas no miden adoptabilidad.
Detalle y regla operativa en `agents/top.md`.

### ⚠️ Y un no-hallazgo que importa igual: `openclaw` NO es un proyecto legal
Un medio de este mes describe `openclaw/openclaw` como *«proyecto open source de AI legal»* y el
repo más estrellado de GitHub. **Existe, es MIT y tiene 394.928★ — las tres comprobaciones pasan
limpias — y no es legal**: su propia descripción es *«The AI that really does things. Any OS. Any
Platform. The lobster way. 🦞»*, sin un solo término jurídico. **Queda registrado como rechazo
explícito** para que un pase futuro no lo «descubra» por las estrellas. La verificación de
existencia no detecta errores de pertinencia: ver G-L5 en `agents/top.md` y **P15** en
`compose/patterns.md`.

---

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
