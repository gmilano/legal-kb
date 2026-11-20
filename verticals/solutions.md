---
industry: legal
region: Global
updated: 2026-11-20
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

**9 plataformas reales, las 9 verificadas hoy, las 9 licencias comprobadas.**

### ⚠️ Aviso AGPL-3.0 — afecta a tres de las nueve
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

### ⚠️ Aviso de procedencia — LawLink
Existen al menos **tres copias casi idénticas** de LawLink en GitHub bajo cuentas distintas
(`lawflow-boop/LawLink`, `azaj01/LawLink`, `xcxzzx-1/LawLink`), con la misma descripción y el
README en chino. `lawflow-boop` declara `v2.0.0` y su LICENSE es MIT (1.072 B, leído; **en banda
MIT**). **No está establecido cuál es el upstream canónico.** Antes de recomendarlo a un cliente
hay que determinar la autoría real y el estado de mantenimiento. Se publica con el aviso en lugar
de omitirlo, porque es la única opción permisiva de *practice management* hallada.

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
