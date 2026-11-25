---
industry: legal
region: Global
updated: 2026-11-25
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
| 🆕 **Kourti Legal** | **MIT** (1.069 B) | [boyeesu/Kourti](https://github.com/boyeesu/Kourti) | React + Node + **PostgreSQL**, `docker compose` | 🆕 **La primera base permisiva de *practice management* de esta KB: matters, documentos, clientes y plazos.** Cierra el hueco que el pase 4 declaraba abierto (y que concluyó erróneamente que no existía — ver abajo). CI, `SECURITY.md`, guía de self-hosting con endurecimiento explícito. ⚠️ **1★: proyecto joven, se forkea y se asume mantenimiento.** Sin trust accounting ni control de conflictos. | 1 |
| 🆕 **kancelaria-lex** | **MIT** (1.069 B) | [AI4CharityPL/kancelaria-lex](https://github.com/AI4CharityPL/kancelaria-lex) | Docker (4 segmentos, 3 `internal: true`) + Tesseract | 🆕 **Expedientes judiciales con localidad IMPUESTA POR ARQUITECTURA y verificación de cita por construcción** (comparación carácter a carácter contra el documento fuente; 0 citas inconsistentes en todas las corridas, >80% de precisión). Polonia, pero el patrón es replicable a cualquier jurisdicción. **El mejor candidato de esta KB para un despliegue EMEA soberano.** | 60 |
| 🆕 **Mayan EDMS** | **Apache-2.0** (⚠️ puntero de **586 B**) | [mayan-edms/Mayan-EDMS](https://github.com/mayan-edms/Mayan-EDMS) | Django/Python | 🆕 DMS libre: almacenamiento, metadatos, OCR y **estados de workflow** — capa de gestión documental bajo un flujo legal, no un CLM. 🧮 **GitHub dice `NOASSERTION` y se equivoca:** su LICENSE son 586 B, muy por debajo de la banda Apache (11.300–11.400), porque es un **puntero** («Licensed under the Apache License, Version 2.0»), no el texto completo. La regla 932-G1 lo predijo. ⚠️ Es un **espejo** (sin PRs ni issues) y 🪦 **6 meses sin push** (2026-05-23). | 850 |

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

## 🟢 HUECO CERRADO EN EL PASE 5 — practice management permisivo, y **corrigiendo la conclusión del pase 4**

> 🔴 **Corrección a lo que este fichero afirmaba hace una hora.** Decía, en negrita:
> *«**«Kourti Legal» no existe.** (…) **No hay tal repo.** Bajo ese nombre: `boyeesu/Kourti` (MIT,
> **1★**) (…) El dato de la fuente **no se sostiene**; no se publica como hallazgo.»*
> **El repo existe, es MIT, y tiene código real.** El pase 4 lo tuvo delante —lo citó por su slug
> exacto y leyó su licencia— y concluyó «no existe» **a partir del contador de estrellas**.

**Lo medido en el pase 5 sobre `boyeesu/Kourti`:**

| Comprobación | Canal | Resultado |
|---|---|---|
| Existencia | `git ls-remote` | **524 refs** (ramas `chore/oss-release-prep`, `agent/codeql-remediation`, `386i4l-codex/update-supabase-query-for-cases-and-contracts`) |
| Licencia | `raw` byte a byte | **MIT, 1.069 B** — dentro de la banda MIT (1.050–1.150) del checksum 932-G1 |
| Alcance | lectura del README | «The open-source workspace for **matters, documents, clients, and deadlines**» |
| Stack | README | React + API Node + **PostgreSQL**, `docker compose up --build`, healthcheck en `/health`, CI en GitHub Actions, `SECURITY.md` |
| Self-hosting | README | documentado, con advertencia de endurecimiento: `AUTH_MODE=custom`, secretos JWT distintos, TLS, CORS restringido, BD y almacenamiento de objetos de producción |
| Aviso profesional | README | «Kourti Legal is software, not legal advice. AI-generated content can be inaccurate and must be reviewed by a qualified professional» |
| Tracción | API de búsqueda | **1★**, `pushed_at` 2026-11-01, **sin `description` ni `topics`** |

**Por qué el pase 4 se equivocó, y es un error de clase, no de dato.** Confundió *«no tiene señal
social»* con *«no existe el artefacto»*. El escepticismo hacia el **agregador** estaba justificado
—presentaba Kourti como producto consolidado, lo cual es falso— pero la afirmación verificable que
ese agregador hacía (**código fuente MIT en GitHub**) era **cierta**, y se descartó junto con el
resto. Ver `agents/top.md` → **G-L10**.

⇒ **El «Odoo de los despachos legales» con licencia permisiva ya tiene un candidato real.** Lo que
hay que decirle a un cliente, sin adornos:

- ✅ **Licencia limpia** (MIT genuino, verificado byte a byte) y **alcance correcto** (matters,
  documentos, clientes, plazos — el vocabulario de practice management, no de DMS genérico).
- ✅ **Arranca**: stack contenedorizado y documentado, sin pasos manuales de reconstrucción.
- ⚠️ **Proyecto joven y sin comunidad**: 1★. No hay ecosistema, ni releases que fijar con
  confianza, ni garantía de continuidad. **Se forkea y se asume mantenimiento** — es una base de
  partida, no un proveedor.
- ⚠️ **Sin auditar**: este pase verificó licencia, existencia y alcance. **No** auditó seguridad,
  calidad del código ni cobertura de tests. Antes de una propuesta, auditar (hay rama
  `agent/codeql-remediation`, señal de que el propio autor pasó CodeQL).

**Lo que sigue abierto, ahora acotado de verdad:** no existe practice management permisivo con
**trust accounting** ni **control de conflictos de interés** — las dos piezas que un colegio de
abogados mira primero. `Kourti` cubre el workspace; esas dos no las declara. El candidato con
trust accounting (**Kosmos**) es **AGPL-3.0**.

**Candidatos revalidados y descartados** (se mantienen, seguían siendo correctos):

- **Litigious** — AGPL-3.0 (según su propio sitio). Sin repo GitHub localizable por búsqueda.
- **J-lawyer** — se describe como open source para despachos, pero **ninguna fuente consultable
  declara su licencia** y no aparece en la búsqueda de GitHub.
- **createrivabu/Iuris-Soft** — existe (26★) pero **sin fichero de licencia** y **sin commits
  desde 2025-12-03**. No es base recomendable.
- **ArkCase / LexATT** — no declaran licencia en fuentes consultables.
- **Genéricos adaptables** (no legales): Apache OFBiz (Apache-2.0, CRM+ERP en Java), Krayin CRM
  (MIT), iDURAR ERP/CRM (MIT), Dolibarr (GPL). Adaptables a flujos de despacho, **pero ninguno
  conoce el dominio legal**: matters, conflictos de interés, trust accounting, plazos procesales.

## 🟢 Hueco cerrado este pase: e-discovery

Los pases anteriores no declararon este hueco porque **no se había mirado la capa**. Queda
cerrado con `FreeEed` (Apache-2.0, activo). Se deja constancia de que el hueco existió sin
declararse: *una capa que nadie buscó se parece mucho a una capa que no hace falta.*

## 🔴 Segundo hueco: firma electrónica permisiva — **CONFIRMADO, y ahora medido en los tres mayores**

El pase 4 lo declaró sobre un solo candidato. El pase 5 lo midió sobre **los tres proyectos de
e-signature open source más grandes que existen**, y el resultado es unánime:

| Plataforma | Repo | Licencia (medida) | Stars | Último push |
|---|---|---|---|---|
| DocuSeal | [docusealco/docuseal](https://github.com/docusealco/docuseal) | **AGPL-3.0** | **19.110** | 2026-11-19 |
| Documenso | [documenso/documenso](https://github.com/documenso/documenso) | **AGPL-3.0** | **15.841** | 2026-11-20 |
| OpenSign | [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | **AGPL-3.0 + carve-out** (GitHub: `NOASSERTION`) | 7.316 | 2026-11-20 |
| LibreSign | — | **AGPL-3.0** | — | sólo dentro de Nextcloud |

🧮 **Y OpenSign corrobora la regla asimétrica del checksum 932-G1, por el lado «por arriba».** Su
LICENSE mide **35.051 B**, por encima de la banda AGPL-3.0 (~34.500). La regla dice: *bytes por
encima de la banda ⇒ licencia compuesta, hay que leerla*. Se leyó, y **es compuesta**: el texto
AGPL va precedido de tres cláusulas que excluyen el directorio
`apps/OpenSignServer/cloud/customRoute` (licencia propia) y los componentes de terceros. Por eso
GitHub no puede clasificarla y devuelve `NOASSERTION`. **La regla predijo «compuesta» antes de
abrir el fichero.**

⇒ **Conclusión reforzada, no cambiada: no existe e-signature open source permisiva.** Los tres
líderes son copyleft de red, lo que para un SaaS cerrado es inviable. **Para un entregable cerrado
esta capa se compra; para un despliegue interno del cliente, DocuSeal o Documenso son viables**
(AGPL no contamina si no hay distribución ni servicio a terceros). La decisión es de modelo de
negocio, no técnica.

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

---

## 🆕 PASE 6 (2026-11-21) — la vía «Odoo»: bases ERP/CRM permisivas para construir el despacho encima

Este fichero ha buscado siempre **plataformas legales** permisivas, y el pase 5 cerró el hueco de
*practice management* con `boyeesu/Kourti` (MIT, 1★, sin contabilidad fiduciaria ni control de
conflictos). Falta la otra vía, la que el resto de la rotación usa de serie: **no buscar la
plataforma vertical, sino una base ERP/CRM horizontal madura y poner el vertical legal encima** —
el patrón Odoo/OpenMRS/Moodle. Medido este pase:

| Plataforma | Licencia (leída) | URL | Stack | Caso de uso legal | Stars |
|------------|------------------|-----|-------|-------------------|-------|
| 🟢 **Apache OFBiz** | Apache-2.0 (**11.906 B**, incluye `NOTICE` en el fichero) | [apache/ofbiz-framework](https://github.com/apache/ofbiz-framework) | Java, entidad-motor + motor de servicios | 🟢 **La base más defendible de las tres, y la menos cómoda.** Framework de automatización empresarial de la **Apache Software Foundation**: gobernanza de fundación, no de autor individual — en este sector eso es la señal de continuidad que casi ningún activo legal tiene. Su modelo de datos genérico (partes, acuerdos, facturación por tiempo) mapea bien a *matter / cliente / contrato / horas*. Coste real: hay que construir el vertical legal entero. | n/d |
| 🟢 **Krayin CRM** | MIT (1.078 B) | [krayin/laravel-crm](https://github.com/krayin/laravel-crm) | Laravel + PHP, MySQL | 🟢 **La vía corta para el lado cliente del despacho**, no para el expediente. MIT limpio (Webkul): leads, contactos, actividades, presupuestos, flujos de trabajo. Sirve como capa de **CRM de despacho e intake** — y el *intake* es precisamente donde Clio mide que **46% de los consumidores consultaría una AI antes de llamar a un abogado**. No tiene ni expediente ni plazos procesales: eso se añade. | n/d |
| 🔴 **iDURAR ERP/CRM** | **AGPL-3.0** ⚠️ (**34.230 B**) | [idurar/idurar-erp-crm](https://github.com/idurar/idurar-erp-crm) | MERN (Node + React + Mongo) | 🔴 **SE REGISTRA COMO CORRECCIÓN, NO COMO RECOMENDACIÓN.** Una fuente indexada lo describe como *«fully open-source under the MIT license»*. **Es AGPL-3.0**, leído byte a byte: 34.230 B, banda AGPL (~34.500), encabezado `GNU AFFERO GENERAL PUBLIC LICENSE Version 3`. El checksum 932-G1 lo predijo **antes** de abrir el encabezado. Copyleft de red ⇒ inviable como base de SaaS cerrado. | n/d |

### Lo que esta vía cambia, y lo que no

- **Sí resuelve** la objeción de madurez: OFBiz y Krayin tienen años de producción y comunidad, al
  contrario que los activos legales verticales permisivos de esta KB, que son casi todos de un solo
  autor y pocas estrellas.
- **No resuelve** lo específicamente legal: ni plazos procesales, ni **contabilidad fiduciaria**
  (*trust accounting*), ni control de conflictos de interés, ni privilegio abogado-cliente en el
  modelo de permisos. Esas cuatro son las que hacen que un ERP genérico no sea un sistema de
  despacho, y las cuatro siguen siendo trabajo de Globant en cualquiera de las dos vías.
- **Recomendación:** para un engagement de despacho, **Krayin (MIT) para intake/CRM + Kourti (MIT)
  para expediente + la capa MCP de fuentes oficiales** del país (ver `repos/foundations.md` → pase
  6) es hoy la combinación permisiva de punta a punta más corta. OFBiz sólo se justifica si el
  cliente ya es Java y quiere un único ERP.

### 🗑️ Descartado en esta capa, con la medición

- `createrivabu/Iuris-Soft` (26★) — sistema de gestión legal con el alcance correcto (contactos,
  societario, litigios, documentos, tareas, facturación, contratos) y **sin licencia**: 404 medido
  en `LICENSE`, `LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING`, `LICENSE-MIT` sobre `HEAD`, y
  sin entrada *License* en la barra lateral. Sin licencia expresa no hay derecho de uso ni
  derivado. **Es el candidato a vigilar**: si publica MIT/Apache, entra directo.
- `j-lawyer` — descrito por una fuente indexada como practice management libre (Alemania, EMEA).
  **Ningún slug verificable:** `j-lawyer-org/j-lawyer` y `j-lawyer-org/j-lawyer-server` dan 404.
  No entra sin slug.


## 🆕 PASE 7 (2026-11-22) — la capa vertical no cambió; lo que cambió es **qué se puede prometer sobre ella**

Este pase no añade plataformas: el barrido de creación (`legal AI created:>2026-08-01 stars:>=25`)
dio **10 repos en cuatro meses** y **ninguno** es una plataforma vertical nueva. Lo que sí se midió
es la **actividad** de todo lo que ya estaba, y eso cambia la conversación con el cliente.

### ✅ Las 14 plataformas de esta capa, verificadas hoy por doble canal

**93 slugs citados en los ocho ficheros de esta KB → 93 resuelven, 0 archivados, 0 inexistentes,
3 renombrados (los tres ya documentados).** Ninguna de las plataformas de esta capa ha muerto,
cambiado de nombre ni sido archivada desde el pase 6.

### 📏 Y la medición que importa para una propuesta: **estrellas y actividad son ejes distintos**

| Plataforma | Licencia | Stars | Último commit | Qué se puede prometer |
|---|---|---|---|---|
| [stella/stella](https://github.com/stella/stella) | Apache-2.0 | 282 | **2026-11-22** | Commit **de hoy**. Base de despliegue de cliente con mantenimiento demostrable. |
| [boyeesu/Kourti](https://github.com/boyeesu/Kourti) | MIT | **1** | 2026-11-01 | *Practice management* permisivo. **1 estrella y 3 semanas desde el último commit**: viable como base a bifurcar, **no** como producto con comunidad detrás. La promesa es «lo mantenemos nosotros», no «lo mantiene el upstream». |
| [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | MIT | 1.016 | 2026-11-13 | El maduro de la capa, y sigue vivo. |
| [SuffolkLITLab/docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | MIT | 75 | 2026-11-20 | 75★ y commit de hace dos días: **bajo en señal social, alto en actividad.** |
| [mayan-edms/Mayan-EDMS](https://github.com/mayan-edms/Mayan-EDMS) | NOASSERTION → **puntero Apache-2.0** (586 B) | 850 | 2026-05-23 | 🪦 **6 meses sin commits.** Sigue siendo el EDMS de referencia, pero no se ofrece soporte apoyado en el upstream. |
| [OpenSignLabs/OpenSign](https://github.com/OpenSignLabs/OpenSign) | NOASSERTION → **AGPL-3.0 + carve-out** (35.051 B) | **7.320** | 2026-11-20 | Firma electrónica. ⚠️ AGPL: despliegue interno de cliente sí, producto SaaS cerrado no. |
| [docusealco/docuseal](https://github.com/docusealco/docuseal) · [documenso/documenso](https://github.com/documenso/documenso) | **AGPL-3.0** ⚠️ | 19.118 · 15.862 | 2026-11-19 · 2026-11-22 | Las dos mayores de firma electrónica, **las dos AGPL**. |

> 🔴 **El hueco de firma electrónica permisiva sigue CONFIRMADO, y ahora con la cuarta medición
> consecutiva:** DocuSeal **19.118★ AGPL-3.0**, Documenso **15.862★ AGPL-3.0**, OpenSign
> **7.320★ AGPL-3.0 + carve-out**, LibreSign AGPL-3.0. **4 de 4 copyleft de red.** Esto es
> **estructural, no accidental**: en firma electrónica el valor es la confianza y el cumplimiento,
> y la AGPL es exactamente lo que impide que un proveedor SaaS te bifurque el producto. No esperar
> que aparezca una alternativa MIT; **planificar el despliegue interno o la licencia comercial.**

### 🎯 Y la consecuencia comercial del eje de actividad (`G-L14`)

Esta capa tiene plataformas de **7.320★ paradas desde mayo** y plataformas de **1★ tocadas este
mes**. Para una propuesta eso se traduce en **dos frases distintas, y hay que elegir la correcta**:

- **Alta señal + alta actividad** (`stella`, `docassemble`, `documenso`): *«partimos de una base
  con comunidad; el upstream absorbe parte del mantenimiento»*.
- **Baja señal + alta actividad** (`Kourti`, `AssemblyLine`, los MCP de LATAM): *«partimos de una
  base viva pero poco conocida; el mantenimiento lo asumimos nosotros, y a cambio no hay
  competidor que haya partido de aquí»*. **Esta es la posición más defendible comercialmente** —
  ventaja de entrada real, sin esperar a que nadie construya nada.
- **Alta señal + baja actividad** (`Mayan-EDMS`, y en `agents/top.md` `lawyer-llama` con 1.003★ y
  dos años parado): *«lo usamos como patrón o como corpus, no como dependencia mantenida»*.

**La columna que decide qué se promete es `pushed_at`. Las estrellas sólo deciden el orden en que
se lee la lista.**

---

## 🆕 PASE 8 (2026-11-22) — la vertical que faltaba no es jurídica: es **el back office que cobra**

Las 14 plataformas de esta capa cubren el **trabajo** del despacho (expediente, documento, firma,
investigación). Ninguna cubre el **cobro**. Y el cobro es donde esta KB acaba de medir el hueco más
grande de las ocho pasadas: 17 de 19 términos del vocabulario de facturación, plazos, cuentas de
terceros y conflictos daban **cero ocurrencias** en los ocho ficheros (detalle en `agents/top.md`).

### Plataformas de partida para el plano de ingresos — verificadas 2026-11-22

Igual que Odoo es la base ERP sobre la que se construye una vertical, estas son las bases de
**facturación y registro de tiempos** sobre las que se construye el back office del despacho. Son
genéricas **a propósito**: la capa específica del sector no tiene ninguna opción permisiva madura.

| Plataforma | Repo | Licencia (leída) | Madurez | Para qué sirve en legal | Lo que **no** trae |
|---|---|---|---|---|---|
| **Kill Bill** | [killbill/killbill](https://github.com/killbill/killbill) | **Apache-2.0 (11.357 B)** | 5.862★ · 990 forks · 14 años · commit 2026-11-21 | Motor de facturación y pagos con catálogo, impuestos, prorrateo, reintentos y plugins de pago. **La base permisiva más sólida de toda la capa** | Expediente, tarifario por abogado, UTBMS, cuenta de terceros |
| **FOSSBilling** | [FOSSBilling/FOSSBilling](https://github.com/FOSSBilling/FOSSBilling) | **Apache-2.0 (11.454 B)** | 1.757★ · 374 forks · commit 2026-11-20 | Facturación + clientes + órdenes en PHP con módulos. Alternativa ligera para despacho pequeño sin volumen de suscripción | Lo mismo, y menos extensible que Kill Bill |
| **InvoicePlane** | [InvoicePlane/InvoicePlane](https://github.com/InvoicePlane/InvoicePlane) | **MIT** en fichero compuesto (5.087 B; GitHub dice `NOASSERTION`) | 3.290★ · 888 forks · commit 2026-11-18 | Presupuesto → factura → pago, autoalojado, muy simple de desplegar | ⚠️ **La marca sí está restringida**: no se redistribuye bajo el nombre «InvoicePlane» |
| **Kimai** | [kimai/kimai](https://github.com/kimai/kimai) | **AGPL-3.0 (34.523 B)** ⚠️ | 5.173★ · 895 forks · commit **2026-11-22** | Registro de tiempos de referencia: *timesheets*, tarifas por proyecto/actividad/usuario, export, API | ⚠️ Copyleft de red ⇒ **herramienta interna del despacho**, no componente de un SaaS cerrado |
| **InvoiceShelf** | [InvoiceShelf/InvoiceShelf](https://github.com/InvoiceShelf/InvoiceShelf) | **AGPL-3.0 (34.523 B)** ⚠️ | 2.075★ · 428 forks · commit 2026-11-22 | Facturación autoalojada, linaje Crater, mantenida | Misma advertencia de copyleft |

### 🪦 Y por qué no se recomienda la opción que parecería obvia

Existe **un** sistema de gestión de despacho Apache-2.0 —
[NodineLegal/OpenLawOffice](https://github.com/NodineLegal/OpenLawOffice), 38★, 27 forks, «case
management, billing, tasking and more»— y **no tiene un commit desde el 10 de abril de 2016**. Diez
años y medio. Es la respuesta a la pregunta que todo arquitecto hace al ver este hueco («¿seguro que
nadie lo ha hecho ya en permisivo?»): sí, alguien lo hizo, y no se sostuvo.

Y las opciones **vivas** y específicas del sector son todas copyleft:
`deedbox-maintainers/deedbox-app` (AGPL-3.0, 34.523 B), `4csolutions/casecentral` (GPL-3.0, 25★, 29
forks, commit 2026-11-14), `Litigious` (AGPL-3.0), y el módulo Odoo
`MohamedESalem/legal_practice_management` (AGPL-3.0) que extiende la app de Proyectos a expedientes.

> **La decisión de arquitectura, y es la inversa de la que esta KB recomienda para el producto
> jurídico:** en el plano del trabajo legal hay base permisiva madura y se **adopta**. En el plano de
> ingresos no la hay y se **construye**: semántica legal (expediente, tarifario, UTBMS, cuenta de
> terceros, plazo) **encima de un espinazo genérico Apache-2.0**. Forkear el producto legal AGPL es
> la opción que parece ahorrar trabajo y es la que cierra la puerta al entregable comercial.

### Cómo customizar con AI esta capa — y dónde NO poner el modelo

El orden importa y está medido, no supuesto (`billing-lint` lo documenta en su README y esta KB lo
recoge en `agents/trending.md`): **la revisión por LLM en lote es inconsistente** — el mismo defecto
se marca en una línea y pasa callado en otra, y dos ejecuciones se contradicen.

1. **Determinista primero.** Aritmética, formato LEDES 1998B, códigos UTBMS, topes y tarifas: reglas.
   Reproducible al céntimo, ejecutable en CI, sin coste por token. → `billcheck` + `billing-lint`.
2. **NLP clásico para cribar.** Clasificadores calibrados y NER contra el listado de personal del
   despacho reducen a una fracción las líneas que merecen juicio.
3. **El modelo sólo donde cabe un juicio**, y **siempre citando la entrada literal**; un verificador
   descarta toda decisión cuya cita no se compruebe. → receta completa en `P29`.
4. **La persona decide.** *Block billing*, narrativa vaga, trabajo administrativo: propuestas, nunca
   ajustes automáticos. Es el mismo *human gate* que esta KB ya exige en el plano del producto.

---

## 🆕 PASE 9 (2026-11-25) — la vertical de la **prueba**: el escritorio del litigante, y por qué aquí el copyleft gana

El pase 8 añadió la vertical del back office que cobra. Esta es la del **documento que se convierte
en prueba**: numerarlo (Bates), redactarlo, producirlo y certificar su firma. Es una vertical real
—los despachos la compran hoy a Relativity, Everlaw y Reveal— y en abierto está **partida en dos
por la licencia**, de forma más nítida que ninguna otra capa de esta KB.

### Plataformas de partida, verificadas 2026-11-25 (licencia byte a byte + `ls-remote` + API)

| Plataforma | Licencia (leída) | Repo | Stack | Qué resuelve y qué hay que saber | ★ |
|---|---|---|---|---|---|
| 🆕 **Autogram Portal** | **EUPL-1.2** (13.832 B) | [slovensko-digital/autogram-portal](https://github.com/slovensko-digital/autogram-portal) | Java / web | **Portal de firma de documentos con firmas cualificadas eIDAS, en producción en un Estado miembro de la UE** (ecosistema digital eslovaco). 483 refs: software real. ⚠️ **EUPL-1.2** es copyleft con cláusula de compatibilidad: lo publicado se mantiene libre, pero **es la licencia que la propia UE prefiere en contratación pública**, lo que en EMEA es ventaja y no obstáculo | 3 |
| 🆕 **RaioPDF** | **GPL-3.0** (35.149 B) | [Macrify-LLC/raiopdf](https://github.com/Macrify-LLC/raiopdf) | Escritorio, **100% local** | Suite PDF **para despachos**: OCR, organización de páginas, redacción y **estampado Bates**. 468 refs, commit de hace 6 días. **Totalmente local** ⇒ encaja con la tendencia nº1 de esta KB. ⚠️ **GPL-3.0: útil como herramienta interna del despacho, inviable como base de producto cerrado** | 6 |
| 🆕 **doc_redaction** | **AGPL-3.0** (34.523 B) | [seanpedrick-case/doc_redaction](https://github.com/seanpedrick-case/doc_redaction) | Python / GUI | **La redacción más madura en abierto**: PDF, imágenes, Word, CSV/XLSX con interfaz gráfica. 315 refs, muy activo. ⚠️ **AGPL-3.0 (copyleft de red)**: inviable para SaaS cerrado | **64** |
| 🆕 **pii-gui** | **AGPL-3.0** (34.523 B) | [sophia486/pii-gui](https://github.com/sophia486/pii-gui) | Escritorio *local-first* | Detecta y redacta PII en PDF, Markdown y texto **sin que el documento salga de la máquina**. 56 refs, 7 forks, commit de hace 2 días. ⚠️ AGPL-3.0 | 49 |
| 🆕 **legion-pdf** | **AGPL-3.0** (34.524 B) | [CasusBelli1337/legion-pdf](https://github.com/CasusBelli1337/legion-pdf) | Escritorio | Editor PDF **para abogados de litigio**: estampado Bates y formatos exigidos por tribunal. ⚠️ **0★, creado 2026-11-18 (hace 7 días), 5 refs: se registra como señal de categoría, NO como plataforma adoptable todavía** | 0 |

### 🔴 La lectura comercial de esta tabla, y es incómoda pero es la útil

**Las cinco plataformas de esta vertical son copyleft. Las cinco.** No hay una sola base permisiva de
*plataforma* en el plano de la prueba — y eso, lejos de ser un callejón sin salida, **indica dónde
está el trabajo**:

| Capa | Licencia disponible | Qué se puede prometer a un cliente |
|---|---|---|
| **Plataforma** (escritorio/suite completa) | GPL / AGPL / EUPL únicamente | Herramienta **interna** del despacho, o despliegue con el derivado liberado. **No** producto cerrado |
| **Estándar / biblioteca** | **MIT / LGPL** (`pyHanko`, `loadfile-tool`, `Marisol`) | **Producto cerrado, entregable comercial, empotrable** |

> 🔑 **Conclusión de arquitectura para esta vertical (y es `T29` aplicado):** el escritorio del
> litigante **no se forkea**, se **compone** sobre las bibliotecas permisivas. `pyHanko` (MIT) firma y
> valida, `Marisol` (MIT) numera y redacta, `loadfile-tool` (MIT) exporta la producción — y la capa de
> flujo, cliente y semántica la pone Globant. Forkear `doc_redaction` o `raiopdf` parece ahorrar seis
> meses y **convierte el entregable en software libre obligatorio**.

### ⚠️ Y un hueco de esta vertical que se publica ABIERTO

**El *privilege log* no tiene plataforma ni biblioteca abierta localizable** — ni permisiva ni
copyleft. Medido: `privilege log` → 902 resultados, **cero relevantes** (colisión con «escalada de
privilegios» en seguridad); `privileged document review redaction` → **0**. Es, según los pronósticos
de sector de 2026, **uno de los flujos de e-discovery que más se automatiza este año**. Para un
engagement, eso es un hueco de producto; para esta KB, un hueco que **no se cierra con una fila
inventada**.

---

## 🆕 PASE 10 (2026-11-25) — plataformas de **legislación**: la vertical que faltaba, y es «el Odoo» de este plano

Este fichero tenía plataformas de **despacho** (practice management, e-discovery, firma). No tenía
ninguna del lado **del que produce la norma**: parlamento, asamblea, ministerio, regulador. Es el
comprador público, y en LATAM es el comprador más grande que existe.

| Plataforma | Licencia (leída) | Qué es | Customizable con AI en | ★ | Último commit |
|---|---|---|---|---|---|
| [laws-africa/indigo](https://github.com/laws-africa/indigo) | **LGPL-3.0** (*stub* 633 B) | **Plataforma de publicación de legislación**: gestiona, **consolida** (aplica las enmiendas al texto vigente) y publica en Akoma Ntoso. Django + Django REST. 38 forks, 11 años, commit de hace 2 días. Es lo más cercano a un «Odoo de la legislación» que existe | Consolidación asistida (proponer el texto resultante de una enmienda y dejar que un humano lo apruebe), detección de derogaciones, control de vigencia, extracción de referencias cruzadas | 78 | 2026-11-23 |
| [openfisca/openfisca-core](https://github.com/openfisca/openfisca-core) + [country-template](https://github.com/openfisca/country-template) | 🔴 **AGPL-3.0** (34.523 B) | **Motor de reglas socio-fiscales**: ejecuta legislación como código, con *reforms* para simular cambios normativos. En el **EU OSS Catalogue** | Traducir el texto del artículo a la fórmula del motor (con el humano validando), explicar en lenguaje llano por qué un caso da el resultado que da, simulación de impacto de una reforma | 252 | 2026-11-24 |
| [PolicyEngine/policyengine-us](https://github.com/PolicyEngine/policyengine-us) | 🔴 **AGPL-3.0** (34.519 B) | El modelo de EE. UU. sobre OpenFisca, con **224 forks**: la prueba de que el patrón «modelo de país» se adopta | Ídem, con línea base real para medir | 178 | 2026-11-24 |
| [CatalaLang/catala](https://github.com/CatalaLang/catala) | **Apache-2.0 (11.358 B)** | No es plataforma, es **lenguaje** — se incluye aquí porque es la única base **permisiva** de esta vertical y por tanto la única empotrable en producto cerrado. 2.453★, 124 forks | Asistir la *anotación* del texto legal contra el código (que es trabajo humano experto y lento), y generar los casos de prueba que el jurista revisa | **2.453** | 2026-11-23 |

### ⚠️ Lectura de licencia para esta vertical — **y es la inversa de la del despacho**

En `practice management` (pase 5) la conclusión fue: **hay base permisiva madura, el producto se
adopta**. Aquí no:

- **Indigo** es LGPL-3.0 con el texto declarado pero **no adjunto** (*stub* de 633 B). LGPL es
  copyleft **débil** —enlazable desde producto cerrado— pero una plataforma Django no se «enlaza»:
  se despliega modificada, y ahí la frontera es discutible. **Para un cliente público no suele
  importar** (el entregable es del Estado y publicarlo es coherente con su misión); para un
  producto cerrado de Globant, sí importa.
- **OpenFisca y PolicyEngine** son **AGPL-3.0**: copyleft de **red**. Exponer el motor como servicio
  arrastra la obligación de fuente al servicio.
- **Catala** es Apache-2.0 y es lo único de esta tabla que se empotra sin condiciones.

> 🔑 **Regla de encuadre comercial, y es la más clara que ha salido de esta vertical:** en este plano
> **el comprador natural es público**, y para un comprador público el copyleft **no es un defecto,
> es un argumento de venta** (garantiza que el Estado no queda capturado por el proveedor). ⇒
> **Indigo y OpenFisca se proponen tal cual en un engagement de gobierno**, y el margen está en la
> implantación, los datos y la capa agéntica, no en la licencia. El reflejo de «evitar AGPL» viene
> del producto SaaS y **aquí se aplica al revés**.

### 🔴 Lo que NO existe en esta vertical, y se consultó

No hay plataforma de **gestión del cambio normativo para la empresa** (el otro lado: no producir la
norma sino rastrear la que te obliga) con licencia permisiva y madurez. Lo medido:
`portable-genai/obligation-register-kit` (Apache-2.0, **0★**, creado 2026-08-22) descompone una
fuente en obligaciones atómicas y las versiona en registro *append-only* — **es la primitiva
correcta y no es una plataforma**. Por encima de ella, lo maduro es propietario o AGPL. ⇒ Categoría
**abierta**, y es la que conecta este plano con el comprador corporativo del `P29` (pase 8).

## 🆕 PASE 11 (2026-11-25) — la vertical del **acta**: aquí la plataforma a customizar es **pública**, no comercial

Los diez pases anteriores buscaron la vertical como *producto que se licencia* (Odoo para el ERP,
Docassemble para el documento, Kourti para el practice management). En el plano acústico ese encuadre
falla, y el dato es que **las plataformas que ya están en producción las opera una judicatura**:

### Sistemas de transcripción judicial **ya desplegados** (el «Odoo» de este plano es un tribunal)

| Sistema | Jurisdicción | Región | Estado medido | Naturaleza |
|---|---|---|---|---|
| **TERES** | India (Tribunal Supremo) | **APAC** | *Speech-to-text* **en vivo** en Salas Constitucionales; texto buscable casi en tiempo real **desde 2023**; pilotos de sala híbrida en juzgados de distrito para **declaraciones de testigos** | Operado por el tribunal, con verificación humana obligatoria por su propio *white paper* |
| **Adalat AI** | India (Kerala) | **APAC** | Transcripción a escala estatal **con política formal** de uso por el personal | Estatal |
| **iCTS** | Singapur | **APAC** | *Intelligent Court Transcription System* desplegado | Estatal |
| *Smart Courts* | China | **APAC** | OCR + ASR + NLP para transcripción automática, incl. tribunales de internet | Estatal |
| **JUSTA** | Chile (Poder Judicial) | **LATAM** | Prototipo del laboratorio de innovación: **2–3 min por audio**, actas en segundos. ⚠️ **Sobre modelos de OpenAI** ⇒ el audio sale de la institución | Estatal, nube externa |
| **Themis** | Chile (Poder Judicial) | **LATAM** | Transcripción y **análisis** de audio de audiencias | Estatal |
| *(sin nombre público)* | Argentina (Consejo de la Magistratura) | **LATAM** | Transcripción automática de audiencias **desde el 28 de octubre**, en **servidores propios**, declarando que *«ninguna información va a plataformas externas»* | Estatal, **on-premise** |

> 🟢 **El hallazgo comercial de la vertical.** Chile y Argentina resolvieron el mismo problema en la
> misma región con **arquitecturas opuestas sobre el dato más sensible que produce un tribunal**.
> Eso convierte la pregunta de compra en una sola: *¿sale el audio de la institución?* Y es
> precisamente la pregunta que un stack **MIT/Apache autoalojado** contesta sin negociación
> contractual. **No hay que vender AI: hay que vender el lugar donde se ejecuta.**

### Lo comercial del plano, y por qué no es la vertical a customizar

Los sistemas de grabación y transcripción de sala que dominan el mercado —**JAVS**, **For The
Record**, **Verbit**— son **cerrados**: no hay capa que extender ni API abierta que envolver. La
mayoría de las cifras públicas de este plano **provienen de sus blogs**, y se marcan como fuente de
parte en `intel/market.md`.

### El stack permisivo equivalente, ensamblable hoy (todo verificado en `repos/foundations.md`)

| Función de la plataforma cerrada | Sustituto permisivo | Licencia |
|---|---|---|
| Captura y servidor de sala | [hwdsl2/scribecrate](https://github.com/hwdsl2/scribecrate) · [ahmetoner/whisper-asr-webservice](https://github.com/ahmetoner/whisper-asr-webservice) | MIT |
| Transcripción en vivo | [QuentinFuxa/WhisperLiveKit](https://github.com/QuentinFuxa/WhisperLiveKit) · [collabora/WhisperLive](https://github.com/collabora/WhisperLive) | Apache-2.0 · MIT |
| Motor offline embarcado | [k2-fsa/sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) · [ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp) | Apache-2.0 · MIT |
| Atribución de locutor | [pyannote/pyannote-audio](https://github.com/pyannote/pyannote-audio) · [BUTSpeechFIT/DiariZen](https://github.com/BUTSpeechFIT/DiariZen) | MIT |
| Anclaje al segundo | [m-bain/whisperX](https://github.com/m-bain/whisperX) · [MahmoudAshraf97/ctc-forced-aligner](https://github.com/MahmoudAshraf97/ctc-forced-aligner) | BSD-2-Clause |
| **Informe de exactitud** (nadie lo vende) | [revdotcom/fstalign](https://github.com/revdotcom/fstalign) · [jitsi/jiwer](https://github.com/jitsi/jiwer) · [pyannote/pyannote-metrics](https://github.com/pyannote/pyannote-metrics) | Apache-2.0 · MIT |
| Anonimización del acta | [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) | MIT |
| Migración sin tocar clientes | [speaches-ai/speaches](https://github.com/speaches-ai/speaches) | MIT |

### 🔴 El hueco de la vertical, delimitado

**Lo que ninguna pieza de la tabla hace: emitir el acta certificable.** Falta el paginador
determinista (25 líneas por página, numeración consecutiva, índice `página:línea`), la plantilla
procesal de cada foro y el gate de certificación humana. No hay implementación permisiva de `PTX`
ni de `LEF` (ver `T31` en `repos/trending.md`). **Es código a escribir y es pequeño** — y es lo
único que separa «texto con timestamps» de «documento que un juzgado acepta».
