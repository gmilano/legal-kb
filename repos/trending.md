---
industry: legal
region: Global
updated: 2026-11-22
---

# 📈 Repos trending — Legal Services

> **Fichero APPEND-ONLY.** Cada pase añade una sección datada arriba y conserva el histórico
> debajo. Este fichero cubre **repos e infraestructura**; los agentes van en `agents/trending.md`.

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
