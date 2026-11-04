---
industry: legal
region: Global
updated: 2026-11-04
---

# 📡 Tendencias — Legal Services

> Última actualización: 2026-11-04

## Las ocho tendencias de este pase

### 1. De piloto a infraestructura
El salto de GenAI en despachos de **28% → 41%** en un año (Thomson Reuters) y de **23% → 47%** en
departamentos in-house marca el fin de la fase demo. Lo que se compra ahora es despliegue
empresarial: exactitud, compliance y formación.

### 2. La AI agéntica ya está dentro, en el 15%
**15% de los profesionales legales ya usa AI agéntica** (Thomson Reuters 2026). No es futuro;
es el segmento temprano al que se le puede vender orquestación hoy.

### 3. El déficit de gobernanza es la oportunidad comercial, no un obstáculo
**54% de los despachos no ofrece formación en AI** y **43% no tiene política de gobernanza**
(Clio reporta 53% sin política formal). Mientras el uso individual llega al 79%, la institución
no tiene control. Vender *governance-first* es vender a un dolor ya existente.

### 4. La trazabilidad desplaza a la fluidez como criterio técnico
El diferenciador en 2026 no es que el modelo redacte bien, sino que **cada afirmación tenga cita
al párrafo de origen**. ContextGem lo implementa como propiedad del framework (extracción con
referencia a párrafo/oración y justificación opcional) y además **no usa retrieval para elegir
chunks**: lee todos los párrafos, de modo que no se pierde una cláusula por quedar mal rankeada.
Para contratos, donde la cláusula que importa suele ser la rara, esto es una decisión
arquitectónica, no un detalle.

### 5. El redline en DOCX es el formato que decide la adopción
Los abogados negocian con *tracked changes* en Word. `contract-review-agent` pasó de informes
JSON/Markdown (v1-alpha) a **DOCX con tracked changes, comentarios al margen y recomendaciones**
(v1-beta). La lección de producto: la salida tiene que entrar en el flujo existente del abogado.

### 6. Los human gates se vuelven parte de la arquitectura
`lavern` (Apache-2.0) formaliza lo que será estándar: **gates humanos obligatorios** — los
hallazgos críticos no se auto-entregan sin aprobación u *override* explícito — más verificación
en 10 pasos. Converge con el Artículo 50 del EU AI Act: si el agente interactúa con personas,
hay obligaciones de transparencia.

### 7. La regulación deja de ser un capítulo legal y pasa a ser requisito de arquitectura
2026 es el año en que los calendarios se vuelven concretos y **divergentes**: EU AI Act en
aplicación desde el 2-ago-2026; Texas TRAIGA y California SB 53 desde el 1-ene-2026; Colorado
reemplazada por SB 189 el 14-may-2026; Corea del Sur con AI Basic Act desde ene-2026; Japón
promocional sin sanciones; Singapur con exigencia de facto vía AI Verify; Brasil todavía en
trámite. Un producto legal global necesita que la jurisdicción sea **configuración**, no una rama
de código.

### 8. La ventaja de la soberanía del dato
En EMEA y LATAM el argumento de venta se invierte: alojamiento local, sin entrenamiento sobre
datos del cliente y de-identificación previa (Presidio) pasan de "requisito incómodo" a
diferenciador frente a los SaaS norteamericanos cerrados.

## Repos con actividad real relevante (verificados 2026-11-04)

Todos comprobados vivos con `git ls-remote` y con licencia leída del fichero:

- [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) — Apache-2.0, 2.1k★ —
  extracción tipada con trazabilidad; lee vía Docling. El hallazgo más reutilizable del pase.
- [JSv4/OpenContracts](https://github.com/JSv4/OpenContracts) — MIT, 1.5k★ — "DMS for the
  agentic world". ⚠️ Corrección: fuentes secundarias lo listaban como GPL-3; **su LICENSE es MIT**
  (1.073 B, leído).
- [AnttiHero/lavern](https://github.com/AnttiHero/lavern) — Apache-2.0, 320★ — 67 agentes,
  human gates, verificación de 10 pasos.
- [lowtidebuild/contract-review-agent](https://github.com/lowtidebuild/contract-review-agent) —
  Apache-2.0, 41★ — redline DOCX local-first.
- [open-legal-products/mike](https://github.com/open-legal-products/mike) — ⚠️ AGPL-3.0 —
  plataforma legal AI, actividad oct-2026.
- [docling-project/docling](https://github.com/docling-project/docling) — MIT, 70.1k★ — la capa
  de parsing por defecto del sector.

## Corrección de datos de pases anteriores

- **`mahdyet1845/Consultor-Tributario-AI` se retira de este fichero: la URL está muerta.**
  `git ls-remote` no resuelve a 2026-11-04. Estaba publicada como "repo más activo de la semana".
- Los demás repos que este fichero listaba como "más activos" (`arin`, `legal-mitra`,
  `uspto_fpd_mcp`) **sí existen**, pero tienen entre 1 y 6 estrellas y ninguna señal de
  actividad o adopción. Permanecen en el histórico de `repos/trending.md` por ser append-only,
  pero **no son tendencia** y no deben compilarse como hallazgos.

## Huecos declarados

- 🔴 **No se hallaron datos de adopción de AI legal en LATAM ni en APAC** — sólo regulación.
  Las búsquedas regionales devolvieron marcos normativos y protección de datos; cero cifras de
  uptake por despachos o tribunales. Es el pendiente principal de investigación.
- 🔴 **No existe practice management open source con licencia permisiva y procedencia clara**
  (ver `verticals/solutions.md`). Hueco de mercado, no de búsqueda.
- ⚠️ El calendario de alto riesgo del EU AI Act (ago-2026 vs. ago-2028) **está en conflicto entre
  fuentes** y no se resolvió en este pase.

---
*v2026-11-04 — primer pase de investigación real. Fuentes: Thomson Reuters 2026, Clio 2026,
8am Legal Industry Report 2026, Comisión Europea, FPF, Baker McKenzie, White & Case AI Watch.*
