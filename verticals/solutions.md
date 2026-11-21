---
industry: legal
region: Global
updated: 2026-11-21
---

# 🏭 Verticales de partida — Legal Services

> Plataformas verticales existentes customizables con AI.
> Modelo: partir de algo funcional, añadir capa agéntica arriba.
> Última actualización: 2026-11-20
>
> **Nota histórica:** la versión de julio de este fichero contenía una única fila de relleno con
> guiones en cada celda y el texto "por completar". Una fila así se compila como entidad real.
> Si en el futuro no hay hallazgos, la tabla va **vacía con una frase explicando qué se buscó** —
> nunca con una fila de relleno.

## Plataformas recomendadas

| Plataforma | Licencia (leída) | URL | Stack | Caso de uso | Stars |
|------------|------------------|-----|-------|-------------|-------|
| **CaseCite** | Apache-2.0 (11.358 B) | [thomasunise/casecite](https://github.com/thomasunise/casecite) | Self-hosted, BYOK | **Nuevo y la plataforma más completa del pase.** Legal RAG privado: nueve herramientas tras un login sobre el mismo corpus — research con citas verificadas contra el pasaje, deep research con plan editable, revisión de contratos con export de redline, **revisión tabular de cientos de contratos** con cada valor atado a su pasaje, export a Excel/CSV/JSON. Sin telemetría; las claves de modelo son del cliente. Conectores Drive/OneDrive/Box/Dropbox/Filevine/Clio (iManage y NetDocuments experimentales). | 286 |
| **OpenSign** | **AGPL-3.0** ⚠️ (35.051 B) | [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | Node + MongoDB (rama **`staging`**) | **Nuevo, y cubre un hueco que esta KB nunca tuvo: la firma electrónica.** Alternativa open source a DocuSign — plantillas, orden de firmantes, pista de auditoría. Ningún flujo legal termina sin firma, y hasta hoy la KB no tenía nada en esa capa. ⚠️ AGPL-3.0: ver aviso. | **7.315** |
| OpenContracts | MIT (1.073 B) | [Open-Source-Legal/OpenContracts](https://github.com/Open-Source-Legal/OpenContracts) | Django + frontend JS | **DMS de contratos + analítica de cláusulas.** El punto de partida cuando el cliente necesita un repositorio contractual con anotación y extracción, no sólo un revisor. ⚠️ **Renombrado** desde `JSv4/OpenContracts`. | 1.550 |
| docassemble | MIT | [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | Python + YAML + Markdown (rama **`master`**) | **Entrevistas guiadas y document assembly.** Intake de cliente, cuestionarios condicionales, generación de documentos desde plantilla determinista. Estándar de facto en access-to-justice. | 1.015 |
| docassemble-AssemblyLine | MIT | [SuffolkLITLab/docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | Python sobre docassemble | **Formulario judicial en papel → web app guiada paso a paso.** Capa de producción sobre docassemble; proyecto insignia CourtFormsOnline.org. | 75 |
| OLDP (Open Legal Data Platform) | MIT | [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | Django + Elasticsearch, Python 3.12 | **Portal de jurisprudencia y legislación** con API REST y búsqueda. La opción permisiva para montar un corpus nacional consultable. | 164 |
| CourtListener | **AGPL-3.0** ⚠️ | [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | Django | **Archivo de datos judiciales buscable** (opiniones, alegatos, jueces, expedientes federales EE. UU.). Excelente backend de investigación; licencia bloqueante para SaaS cerrado. CaseCite lo usa como fuente externa. | 1.076 |
| mike | **AGPL-3.0** ⚠️ | [open-legal-products/mike](https://github.com/open-legal-products/mike) | Self-hosted + app alojada | "OSS Legal AI Platform" estilo Harvey. **4.504★ y commit de ayer: es la plataforma legal AI open source más grande que existe.** Referencia arquitectónica y *benchmark competitivo*; AGPL inviable para producto cerrado. | **4.504** |
| LawLink | MIT (1.072 B) | [lawflow-boop/LawLink](https://github.com/lawflow-boop/LawLink) | Node.js 22 + PostgreSQL 16 | **Gestión de casos y despacho** self-hosted para abogados solos y despachos pequeños. ⚠️ **Verificar procedencia antes de adoptar** — ver aviso abajo. | 110 |
| 🆕 **FreeEed** | Apache-2.0 (12.177 B) | [shmsoft/FreeEed](https://github.com/shmsoft/FreeEed) | Java/JVM, procesamiento distribuido | **E-discovery — la capa que esta KB no cubría en ningún fichero.** Ingesta de contenedores de evidencia (PST, ZIP, imágenes forenses), deduplicación, extracción de metadatos, culling y producción. **Activa desde 2011 con commits de hoy**: la única opción open source de la capa con continuidad demostrada. | 155 |
| 🆕 **opencaselaw** | **MIT código + CC0 datos** | [jonashertner/opencaselaw](https://github.com/jonashertner/opencaselaw) | MCP + REST + CLI + Parquet | **Portal de jurisprudencia nacional listo para agentes, y el único con datos en dominio público.** 1M+ sentencias suizas de 26 cantones (1875–hoy), 21k leyes, grafo de citas de 10M de aristas, trilingüe. **Es la plantilla de referencia** si el engagement pide montar el equivalente para otro país. | 80 |
| 🆕 **Vaquill MS Word add-in** | Apache-2.0 (11.340 B) | [Vaquill-AI/ms-word-addin](https://github.com/Vaquill-AI/ms-word-addin) | Office.js task pane | **Revisión de contratos dentro de Word, con licencia permisiva.** Playbooks, redacción e investigación legal en el task pane. Cierra con Apache-2.0 el canal que esta KB declara decisivo para la adopción: el abogado no cambia de herramienta. | 81 |
| 🆕 doc-haus | **GPL-3.0** ⚠️ (35.149 B) | [sure-scale/doc-haus](https://github.com/sure-scale/doc-haus) | Fork de OpenCode (rama **`dochaus`**) | **Redline local con tracked changes reales en Word**, sin que el documento salga del disco. Fork de OpenCode. ⚠️ GPL-3.0: viable para despliegue interno en el cliente, bloqueante para producto cerrado redistribuido. | 83 |
| 🆕 mcp-taiwan-legal-db | MIT (1.092 B) | [lawchat-oss/mcp-taiwan-legal-db](https://github.com/lawchat-oss/mcp-taiwan-legal-db) | Servidor MCP | **Fuentes oficiales de una jurisdicción como backend de agente.** Sentencias del Yuan Judicial + base nacional de normativa de Taiwán. La opción **permisiva** frente a `tw-legal-rag` (ELv2 en v2+) para la misma jurisdicción. | 234 |

**9 plataformas reales, las 9 verificadas hoy, las 9 licencias comprobadas.**

### ⚠️ Aviso AGPL-3.0 — afecta a tres de las catorce
`OpenSign`, `CourtListener` y `mike` son AGPL-3.0 (leído del fichero). Si el cliente **expone el
servicio por red**, debe ofrecer el código fuente del derivado. Para OpenSign esto es
especialmente relevante porque la firma suele integrarse *dentro* del producto del cliente: ahí la
obligación es de red y aplica. **Alternativas:** no se encontró firma electrónica open source con
licencia permisiva (buscado explícitamente, ver hueco abajo). Si el entregable debe ser cerrado,
la firma se resuelve con un proveedor comercial por API, no con OpenSign forkeado.

> 🔍 **Cómo se detectó:** la API de GitHub reporta `NOASSERTION` para OpenSign. Leído el fichero:
> **35.051 B con 16 menciones a "Affero"** ⇒ AGPL-3.0 inequívoco. `NOASSERTION` es un detector de
> licencia compuesta o no reconocida, **no una ausencia de licencia**. Publicar OpenSign como
> «licencia sin determinar» habría escondido un copyleft de red en la capa de firma.

### ✅ Procedencia de LawLink — MEDIDA EN EL PASE 3, Y EL RIESGO ERA MUCHO MENOR DEL PUBLICADO

El pase 2 encontró **tres slugs casi idénticos** (`lawflow-boop/LawLink`, `azaj01/LawLink`,
`xcxzzx-1/LawLink`) y concluyó: *«no está establecido cuál es el upstream canónico; antes de
recomendarlo hay que determinar la autoría real»*. Eso dejó **la única opción permisiva de
practice management de la KB aparcada detrás de una advertencia** — y la advertencia era más
grande que el hecho. Medido:

| Slug | HEAD (`git ls-remote`) | `LICENSE` | Titular del copyright |
|------|------------------------|----------:|-----------------------|
| `lawflow-boop/LawLink` (★110, el único indexado) | `4736aa10…` | 1.072 B MIT | 叶森 (Sen Ye) |
| `azaj01/LawLink` | `4736aa10…` | 1.072 B MIT | 叶森 (Sen Ye) |
| `xcxzzx-1/LawLink` | `4736aa10…` | 1.072 B MIT | 叶森 (Sen Ye) |

**Los tres son el mismo árbol de commits, byte por byte, con el mismo titular declarado.** No son
tres proyectos compitiendo ni una bifurcación divergente: es **un codebase espejado en tres
cuentas**.

⇒ **Lo que esto cambia en la práctica:**
- **No hay riesgo técnico en la elección**: los bits son idénticos, se clone el que se clone.
- **No hay riesgo de atribución**: MIT exige conservar el aviso de copyright, y el aviso **nombra
  al mismo autor en los tres**, así que la obligación es cumplible sin resolver cuál es el espejo.
- **El único riesgo que queda es de cadena de suministro, y es el que importa**: no se sabe qué
  cuenta controla el autor, y por tanto **a quién se le está confiando el siguiente commit**.
  ⇒ Mitigación estándar y suficiente: **fijar un tag/SHA** (no seguir `main`) y mirrorizar.


### 🔴 CORRECCIÓN DEL PASE 4 — SÍ EXISTE UNA BIFURCACIÓN DIVERGENTE, Y EL NOMBRE ES UN COMUNAL DE 113 REPOS

El párrafo de arriba afirma, en palabras del pase 3: *«No son tres proyectos compitiendo **ni una
bifurcación divergente**: es un codebase espejado en tres cuentas.»* **Las dos mitades de esa frase
se han medido hoy por separado y una es falsa.**

**(a) Hay un cuarto slug, y es el único que NO es el mismo repo.**

| Slug | HEAD (`git ls-remote`) | `LICENSE` | Titular | En índice de búsqueda |
|------|------------------------|----------:|---------|-----------------------|
| `lawflow-boop/LawLink` | `4736aa10…` | 1.072 B MIT | 叶森 (Sen Ye) | **sí** — ★110, MIT, `pushed_at` 2026-11-02 |
| `azaj01/LawLink` | `4736aa10…` | 1.072 B MIT | 叶森 (Sen Ye) | no |
| `xcxzzx-1/LawLink` | `4736aa10…` | 1.072 B MIT | 叶森 (Sen Ye) | no |
| 🔴 **`appleoppa/LawLink`** | **`535a3531…`** ⇒ **ÁRBOL DISTINTO** | 1.072 B MIT | 叶森 (Sen Ye) | no |

`appleoppa/LawLink` **no apareció en el pase 3 y es precisamente el caso interesante**: mismo
titular y misma licencia, **pero otro HEAD**, así que es una **bifurcación real con código que
nadie de esta KB ha leído**. Las fuentes secundarias la describen como *«un fork que añade
integraciones opcionales»* — es decir, **el repo del que un lector se sentiría tentado de partir
es justo el que no está medido**: sin índice, no tiene estrellas, ni `archived`, ni `pushed_at`.
⇒ **Adoptable en licencia (MIT 1.072 B legible, titular conservado), no evaluable en vitalidad.**

**(b) Y el hallazgo que cambia el método: `LawLink` no es un nombre, es un comunal.**

```
gh api -X GET search/repositories -f q='LawLink in:name' --jq '.total_count'
→ 113
```

**113 repositorios independientes se llaman LawLink.** De los 20 primeros por relevancia:
`lawflow-boop/LawLink` es **el único con licencia Y estrellas Y actividad**; el resto son 0–1★ sin
fichero de licencia (proyectos de bootcamp y TFG: `Mayank-Arya`, `dvjsharma`, `chitrakshtarun`,
`haxybaxy`, `Smokehim`, `AditiDhoni`, `SoumithReddy7`, `Paras2611`, `salvationchinedu`…). La única
otra con licencia, **`NovaLynk/LawLink` (MIT, 1★)**, está **muerta desde 2023-12-01**.

⇒ **Dos poblaciones distintas, y hacen falta dos instrumentos distintos:**

| Población | Qué comparten | Único instrumento que las encuentra |
|-----------|---------------|-------------------------------------|
| **Comunal de nombre** (113) | el **nombre**, nada más | `q='<nombre> in:name'` + `total_count` |
| **Alias del repo real** (4) | el **HEAD** (o divergen de él) | `git ls-remote` (P16) |

**P16 responde a la segunda y es ciego a la primera.** El pase 3 alimentó P16 con **tres slugs
sacados de una sola búsqueda web** y concluyó «procedencia resuelta». Era una conclusión sobre los
tres slugs que tenía, presentada como una conclusión sobre LawLink. ⇒ Receta nueva:
`compose/patterns.md` → **P18**.

> 🔧 **G-L7 — UNA PRUEBA DE PROCEDENCIA SÓLO ES TAN COMPLETA COMO EL CONJUNTO DE CANDIDATOS QUE SE
> LE PASA, Y EL CONJUNTO NO SE OBTIENE DE UNA BÚSQUEDA WEB: SE CENSA.** Antes de escribir «**el**»
> seguido de un nombre de repo, correr el censo. `total_count = 113` significa que **el nombre
> desnudo no identifica nada** y no debe aparecer nunca sin su owner. Y el corolario asimétrico:
> un `total_count` alto **no** desacredita al candidato — `lawflow-boop/LawLink` sigue siendo un
> activo MIT legítimo —, lo que desacredita es **haber dicho «el» LawLink sin haber contado**.

**Lo que NO cambia:** LawLink sigue siendo la única opción de *practice management* con licencia
permisiva de esta KB, con 110★ y en estado temprano declarado. La mitigación del pase 3 (**fijar
tag/SHA y mirrorizar, no seguir `main`**) era correcta y ahora está **mejor fundada**: con una
bifurcación divergente confirmada en circulación, clonar «el LawLink» sin fijar owner+SHA puede
traer un árbol distinto del que se auditó.

> 📌 **Esto es el modo de fallo inverso al del `contract-review`, y conviene verlos juntos.** Allí
> una advertencia *insuficiente* («activo») dejó pasar un repo dormido con el slug muerto. Aquí una
> advertencia *excesiva* («autoría sin determinar») congeló un activo utilizable. **Una cautela mal
> calibrada cuesta en las dos direcciones**, y las dos se corrigen con el mismo instrumento de
> dos líneas: identidad de HEAD + titular del `LICENSE`.

### 🆕 Plataformas añadidas en el pase 3

| Plataforma | Licencia (leída) | URL | Stack | Caso de uso | Stars |
|------------|------------------|-----|-------|-------------|-------|
| 🆕 **stella** | Apache-2.0 (11.358 B) | [stella/stella](https://github.com/stella/stella) | Workspace legal | **El candidato permisivo más vivo del pase: commit de hoy mismo.** «Open-source legal workspace» bajo cuenta de organización, no de autor individual — en un sector donde casi todo es repo personal, eso es la señal de continuidad más fiable disponible. Entra como **candidato a base de despliegue de cliente**, pendiente de auditoría funcional. | 282 |
| 🆕 **Prism-Legal-OS** | **AGPL-3.0** ⚠️ (34.523 B) | [FuturixAI-and-Quantum-Works/Prism-Legal-OS](https://github.com/FuturixAI-and-Quantum-Works/Prism-Legal-OS) | Plataforma legal integrada (India) | **Análisis de contratos + investigación jurídica + litigio en un solo sistema**, que es justo la forma de producto que el mercado está comprando (ver `intel/trends.md`). ⚠️ AGPL-3.0: **válida para despliegue interno en el cliente, bloqueante para producto cerrado redistribuido.** Referencia de arquitectura para APAC. | 226 |
| 🆕 **mon-entreprise** | MIT (1.074 B) | [betagouv/mon-entreprise](https://github.com/betagouv/mon-entreprise) | `publicodes`, mantenido por el Estado francés | **Ley como código, no ley como prompt.** Derecho laboral/fiscal/societario francés en reglas ejecutables y auditables. **El patrón de referencia para cualquier cálculo normativo que tenga que ser defendible ante un regulador** — y la contraparte europea exacta del argumento «plantilla determinista» de docassemble. | 337 |

## 🔴 Hueco declarado — practice management permisivo (ahora con un candidato refutado)

Se volvió a buscar hoy: `legal practice management self-hosted matters invoicing MIT`,
`open source platform legal practice management ERP CRM MIT Apache`, y una búsqueda nominal del
único candidato prometedor.

**El hueco sigue abierto, y ahora está mejor caracterizado:**

- ⚠️ **«Kourti Legal» no existe.** Una fuente lo describía como plataforma de practice management
  legal **MIT y self-hostable** — exactamente lo que falta. **No hay tal repo.** Bajo ese nombre:
  `boyeesu/Kourti` (MIT, **1★**), `kourti2026/kourti` (0★) y cuatro cuentas personales homónimas.
  El dato de la fuente **no se sostiene**; no se publica como hallazgo.
- **Litigious** — AGPL-3.0 (según su propio sitio). Sin repo GitHub localizable por búsqueda.
- **J-lawyer** — se describe como open source para despachos, pero **ninguna fuente consultable
  declara su licencia** y no aparece en la búsqueda de GitHub.
- **createrivabu/Iuris-Soft** — existe (26★) pero **sin fichero de licencia** y **sin commits
  desde 2025-12-03**. No es base recomendable.
- **ArkCase / LexATT** — no declaran licencia en fuentes consultables.
- **Genéricos adaptables** (no legales): Apache OFBiz (Apache-2.0, CRM+ERP en Java), Krayin CRM
  (MIT), iDURAR ERP/CRM (MIT), Dolibarr (GPL). Adaptables a flujos de despacho, **pero ninguno
  conoce el dominio legal**: matters, conflictos de interés, trust accounting, plazos procesales.

**Conclusión, que es un hallazgo y no una ausencia de búsqueda: no existe hoy un «Odoo de los
despachos legales» con licencia permisiva y gobernanza clara.** Dado que Clio publica adopción de
AI del 75–86% en despachos pequeños y medianos, **el segmento existe y no tiene base abierta.**
Es la oportunidad de producto más clara de esta KB (ver `intel/market.md`).

## 🟢 Hueco cerrado este pase: e-discovery

Los pases anteriores no declararon este hueco porque **no se había mirado la capa**. Queda
cerrado con `FreeEed` (Apache-2.0, activo). Se deja constancia de que el hueco existió sin
declararse: *una capa que nadie buscó se parece mucho a una capa que no hace falta.*

## 🔴 Segundo hueco: firma electrónica permisiva
Lo único relevante que apareció es OpenSign, y es AGPL. **No se encontró ninguna plataforma de
e-signature open source con licencia MIT/Apache/BSD.** Para un entregable cerrado, esta capa hoy
se compra; no se forkea.

## Cómo customizar con AI

1. **Fork del repo base** y fijar la versión (no seguir `main`). **Comprobar primero la rama por
   defecto real** — OpenSign está en `staging`, docassemble y databunker en `master`.
2. **Verificar las DOS licencias**: la del software y la del corpus que incorpore. En legal no son
   la misma (ver `repos/foundations.md` → grant partido código/corpus).
3. **Insertar Presidio antes de cualquier egreso** — de-identificar PII antes de llamar a un LLM
   externo. Esto es lo que hace el despliegue defendible bajo GDPR / LGPD / EU AI Act. Si además
   hay que *custodiar* la PII y no sólo redactarla, **Databunker** (MIT) es la pieza complementaria.
4. **Añadir la capa de extracción**: ContextGem (Apache-2.0) con *aspects/concepts* tipados y
   trazabilidad al párrafo de origen — el abogado necesita la cita, no sólo la respuesta.
5. **Verificar la cita contra la fuente oficial**, no sólo contra el documento: es lo que hacen
   korean-law-mcp (법제처) y CaseCite. Con alucinación reportada del 17–33% en research legal,
   esta es la diferencia entre una demo y un entregable.
6. **Envolver los flujos existentes con agentes**, con el patrón de *human gates* de lavern:
   ningún hallazgo crítico se entrega sin aprobación humana explícita.
7. **Partir de `anthropics/claude-for-legal`** (Apache-2.0, 10.054★) cuando el encargo sea
   «flujos legales con agentes» y no «plataforma»: ahorra el andamiaje y ya tiene adaptaciones por
   jurisdicción que sirven de plantilla (Alemania, España).

---
*Verificado 2026-11-20 por doble canal (API de búsqueda + lectura de LICENSE). 9 filas reales,
0 placeholders. 2 huecos declarados con lo que se buscó y qué faltó.*
