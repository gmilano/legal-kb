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
