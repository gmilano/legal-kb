---
industry: legal
region: Global
updated: 2026-11-04
---

# 🏭 Verticales de partida — Legal Services

> Plataformas verticales existentes customizables con AI.
> Modelo: partir de algo funcional, añadir capa agéntica arriba.
> Última actualización: 2026-11-04
>
> **Nota:** la versión anterior de este fichero contenía una única fila de relleno, con guiones
> en cada celda y el texto "por completar" en la última. Una fila así se compila como entidad
> real. Sustituida por plataformas verificadas. Si en el futuro no hay hallazgos, la tabla va
> **vacía con una frase explicando qué se buscó** — nunca con una fila de relleno.
> (El ejemplo no se reproduce aquí literalmente: una línea con pipes dentro de una nota puede
> ser parseada como fila de tabla, que es precisamente el defecto que este pase corrige.)

## Plataformas recomendadas

| Plataforma | Licencia (leída) | URL | Stack | Caso de uso |
|------------|------------------|-----|-------|-------------|
| OpenContracts | MIT | [JSv4/OpenContracts](https://github.com/JSv4/OpenContracts) | Django + frontend JS | **DMS de contratos + analítica de cláusulas.** El punto de partida cuando el cliente necesita un repositorio contractual con anotación y extracción, no sólo un revisor. 1.5k★ |
| docassemble | MIT | [jhpyle/docassemble](https://github.com/jhpyle/docassemble) | Python + YAML + Markdown | **Entrevistas guiadas y document assembly.** Intake de cliente, cuestionarios condicionales, generación de documentos. Estándar de facto en access-to-justice. 999★ |
| docassemble-AssemblyLine | MIT | [SuffolkLITLab/docassemble-AssemblyLine](https://github.com/SuffolkLITLab/docassemble-AssemblyLine) | Python sobre docassemble | **Formulario judicial en papel → web app guiada paso a paso.** Capa de producción sobre docassemble; proyecto insignia CourtFormsOnline.org. 73★ |
| OLDP (Open Legal Data Platform) | MIT | [openlegaldata/oldp](https://github.com/openlegaldata/oldp) | Django + Elasticsearch, Python 3.12 | **Portal de jurisprudencia y legislación** con API REST y búsqueda. La opción permisiva para montar un corpus nacional consultable. 158★ |
| CourtListener | **AGPL-3.0** ⚠️ | [freelawproject/courtlistener](https://github.com/freelawproject/courtlistener) | Django | **Archivo de datos judiciales buscable** (opiniones, alegatos, jueces, expedientes federales EE. UU.). Excelente backend de investigación; licencia bloqueante para SaaS cerrado. 1.1k★ |
| LawLink | MIT | [lawflow-boop/LawLink](https://github.com/lawflow-boop/LawLink) | Node.js 22 + PostgreSQL 16 | **Gestión de casos y despacho** self-hosted para abogados solos y despachos pequeños. ⚠️ **Verificar procedencia antes de adoptar** — ver aviso abajo. |
| mike | **AGPL-3.0** ⚠️ | [open-legal-products/mike](https://github.com/open-legal-products/mike) | — | "OSS Legal AI Platform", actividad oct 2026. Útil como referencia arquitectónica; AGPL inviable para producto cerrado. |

**7 plataformas reales, las 7 vivas, las 7 licencias leídas del fichero.**

### ⚠️ Aviso de procedencia — LawLink
Existen al menos **tres copias casi idénticas** de LawLink en GitHub bajo cuentas distintas
(`lawflow-boop/LawLink`, `azaj01/LawLink`, `xcxzzx-1/LawLink`), con la misma descripción y el
README en chino. Las tres resuelven vivas; `lawflow-boop` declara `v2.0.0` y su LICENSE es MIT
(1.072 B, leído). **No está establecido cuál es el upstream canónico.** Antes de recomendarlo a
un cliente hay que determinar la autoría real y el estado de mantenimiento. Se publica con el
aviso en lugar de omitirlo, porque es la única opción permisiva de *practice management* hallada.

### Hueco declarado — practice management permisivo
Se buscó explícitamente gestión de despacho / case management open source con licencia MIT o
Apache (`open source legal practice management platform case management MIT Apache self-hosted`).
El resultado real del mercado es escaso: **Litigious** es AGPL-3.0; **LexATT** y **ArkCase**
no declaran licencia en fuentes consultables; **Worklenz** es gestión de tareas genérica, no
legal. Es decir: **no existe hoy un equivalente a Odoo para despachos legales con licencia
permisiva y gobernanza clara.** Eso es un hallazgo, no una ausencia de búsqueda — y es una
oportunidad de producto para Globant (ver `intel/market.md`).

## Cómo customizar con AI

1. **Fork del repo base** y fijar la versión (no seguir `main`).
2. **Insertar Presidio antes de cualquier egreso** — de-identificar PII antes de llamar a un LLM
   externo. Esto es lo que hace el despliegue defendible bajo GDPR / LGPD / EU AI Act.
3. **Añadir la capa de extracción**: ContextGem (Apache-2.0) con *aspects/concepts* tipados y
   trazabilidad al párrafo de origen — el abogado necesita la cita, no sólo la respuesta.
4. **Envolver los flujos existentes con agentes**, con el patrón de *human gates* de lavern:
   ningún hallazgo crítico se entrega sin aprobación humana explícita.
5. **UI conversacional / API** sobre el sistema base, devolviendo siempre la cita de origen.

---
*Verificado 2026-11-04 (ls-remote + lectura de LICENSE). 7 filas reales, 0 placeholders.*
