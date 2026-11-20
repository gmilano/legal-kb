---
industry: legal
region: Global
updated: 2026-11-20
---

# 📡 Tendencias — Legal Services

> Última actualización: 2026-11-20

## Las tendencias de este pase

### 1. La verificación de cita pasa de buena práctica a obligación con firma detrás
Es el cambio más importante del pase. Con alucinación reportada del **17–33%** en research legal,
y con la regla de **Indiana (Trial Rule 11, en vigor 1-ago-2026)** estableciendo que **la firma del
abogado certifica que la autoridad citada es auténtica** —y cubriendo expresamente los escritos
asistidos por AI—, verificar la cita deja de ser un diferenciador técnico y pasa a ser una
**transferencia de riesgo personal al socio firmante**. La política interina del **New York UCS**
apunta en la misma dirección: AI de propósito general restringida, uso limitado a herramientas
aprobadas.

La oferta ya existe y es nueva en esta KB:
- **`korean-law-mcp`** (MIT, 2.904★) contrasta la cita contra el texto oficial del 법제처.
- **`CaseCite`** (Apache-2.0) comprueba **cada afirmación contra el pasaje que cita**, y en la
  revisión tabular cada celda queda atada a su pasaje de soporte.
- **`ContextGem`** (Apache-2.0) da trazabilidad al párrafo como propiedad del framework.

### 2. De piloto a infraestructura
El salto de GenAI en despachos de **28% → 41%** en un año (Thomson Reuters) y de **23% → 47%** en
departamentos in-house marca el fin de la fase demo. Lo que se compra ahora es despliegue
empresarial: exactitud, compliance y formación.

### 3. El open source legal dejó de ser marginal — y el líder era invisible para esta KB
Hasta este pase, la KB presentaba el open source legal como un conjunto de proyectos de autor
individual con decenas o cientos de estrellas. Medido hoy: **`anthropics/claude-for-legal`
(Apache-2.0, 10.054★)** y **`mike` (AGPL-3.0, 4.504★)**, ambos con commits de esta semana.
Consecuencia comercial directa: **en una conversación de cliente, el incumbente ya no se compara
sólo contra otro incumbente.** Y consecuencia de método: la KB coronaba `lavern` (326★) y `mike`
como referencias agénticas mientras el líder real, **permisivo y 30× más grande**, no estaba en
ningún fichero.

### 4. La plantilla por jurisdicción es el patrón de producto del año
Ha aparecido una forma repetible, y se ha repetido: **tomar `claude-for-legal` (Apache-2.0) y
adaptarlo a un ordenamiento nacional**. Lo han hecho Alemania (`claude-fuer-deutsches-recht`,
1.866★) y España (`claude-para-abogados`, 49★, con atribución explícita a Anthropic). En paralelo,
**el servidor MCP que envuelve las fuentes legales oficiales de un país**: Corea (2.904★), Italia
(200+ herramientas), Singapur, EE. UU., y servidores de nicho para derecho tributario coreano.
**No existe ninguna de las dos cosas para Brasil ni México** (ver `intel/market.md`).

### 5. El déficit de gobernanza es la oportunidad comercial, y en la UE ya tiene nombre de artículo
**54% de los despachos no ofrece formación en AI** y **43% no tiene política de gobernanza** (Clio
reporta 53% sin política formal), mientras el uso individual llega al 70–83%. En EMEA esto deja de
ser un argumento de venta blando: **el Art. 4 del EU AI Act exige que el personal que usa AI tenga
comprensión adecuada de ella** ⇒ la formación es compliance, no RR. HH.

### 6. La trazabilidad desplaza a la fluidez como criterio técnico
El diferenciador en 2026 no es que el modelo redacte bien, sino que **cada afirmación tenga cita al
párrafo de origen**. ContextGem lo implementa como propiedad del framework y además **no usa
retrieval para elegir chunks**: lee todos los párrafos, de modo que no se pierde una cláusula por
quedar mal rankeada. Para contratos, donde la cláusula que importa suele ser la rara, esto es una
decisión arquitectónica, no un detalle.

### 7. El redline en DOCX sigue siendo el formato que decide la adopción
Los abogados negocian con *tracked changes* en Word. `contract-review-agent` progresó de v1-beta a
**v1.0.0** manteniendo DOCX con tracked changes, comentarios al margen y recomendaciones; CaseCite
exporta redline y comparación cláusula a cláusula. La lección de producto no ha cambiado: **la
salida tiene que entrar en el flujo existente del abogado.**

### 8. Los human gates se vuelven parte de la arquitectura — y en Perú, del reglamento
`lavern` (Apache-2.0) formaliza lo que será estándar: **gates humanos obligatorios** más
verificación en 10 pasos. Converge con el **Art. 50** del EU AI Act. Y ya no es sólo convergencia
de diseño: **el reglamento peruano de la Ley 31814, publicado en sep-2025, exige supervisión
humana para usos de alto riesgo.** El patrón es requisito legal en al menos una jurisdicción.

### 9. La regulación es requisito de arquitectura, y los calendarios divergen más que nunca
2026 consolida la divergencia: EU AI Act con transparencia desde el 2-ago-2026 y **marcado de
contenido ya en mercado hasta el 2-dic-2026** (alto riesgo retrasado a dic-2027 / ago-2028 por el
Digital Omnibus); Texas TRAIGA y las dos leyes de California desde el 1-ene-2026; Colorado con
fecha en disputa; **Corea en vigor 22-ene-2026 pero con 2026 como periodo piloto de facto**;
**Vietnam en vigor 1-mar-2026, primer régimen integral del sudeste asiático**; Taiwán desde
dic-2025; Japón promocional sin sanciones; Singapur con exigencia de facto vía AI Verify; Brasil
todavía en trámite; Perú con reglamento vigente. **Un producto legal global necesita que la
jurisdicción sea configuración, no una rama de código.**

### 10. El alcance extraterritorial invierte quién compra compliance europeo
El **Art. 2(1)(c) del EU AI Act** alcanza a proveedores y deployers de terceros países **cuando el
output se usa en la Unión**. El comprador de "EU readiness" no está sólo en Europa: está en Seúl,
Singapur y São Paulo. Simétricamente, la **Korea AI Basic Act es extraterritorial**, así que un
estudio europeo o latinoamericano que sirva a Corea queda alcanzado.

### 11. En legal, la licencia del software no es la licencia del entregable
Tendencia de fondo que este pase midió por primera vez: los repos de datos legales **licencian el
código y excluyen explícitamente el corpus**. `lexifina/global-law` (CC0 para el árbol de
jurisdicciones, las herramientas y los tests — **no para la ley**, que vive en submódulos con
licencia propia) y `mhfed/vn-law-check` (MIT + nota de que *«no puede licenciar los textos legales
vietnamitas subyacentes»*). Para un entregable de cliente, **«el repo es MIT» no responde la
pregunta que importa**, que es si el corpus se puede redistribuir.

### 12. La ventaja de la soberanía del dato se consolida
En EMEA y LATAM el argumento de venta se invierte: alojamiento local, sin entrenamiento sobre
datos del cliente y de-identificación previa (Presidio) + custodia (Databunker) pasan de
"requisito incómodo" a diferenciador frente a los SaaS norteamericanos cerrados. **CaseCite** es
la prueba de que el mercado open source ya lo está construyendo: BYOK, sin telemetría, índice y
chat en infraestructura del cliente.

## Repos con actividad real relevante (verificados 2026-11-20)

Todos comprobados por API de búsqueda (existencia, estrellas, `archived`, `pushed_at`) **y** con
licencia leída del fichero:

- [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) — Apache-2.0,
  **10.054★**, commit 2026-11-19 — el hallazgo más importante del pase.
- [open-legal-products/mike](https://github.com/open-legal-products/mike) — ⚠️ AGPL-3.0,
  **4.504★**, commit 2026-11-19 — la plataforma legal AI open source más grande.
- [chrisryugj/korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp) — MIT, **2.904★**,
  commit 2026-11-20 — 42 APIs del 법제처 en 10 herramientas MCP + verificación de cita.
- [shcherbak-ai/contextgem](https://github.com/shcherbak-ai/contextgem) — Apache-2.0, 2.095★.
- [Klotzkette/claude-fuer-deutsches-recht](https://github.com/Klotzkette/claude-fuer-deutsches-recht)
  — Apache-2.0, **1.866★**, commit 2026-11-20 — primer activo EMEA de peso en esta KB.
- [Open-Source-Legal/OpenContracts](https://github.com/Open-Source-Legal/OpenContracts) — MIT,
  1.550★ — ⚠️ **renombrado** desde `JSv4/OpenContracts`.
- [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio) — MIT, **11.989★**
  — ⚠️ **renombrado** desde `microsoft/presidio`.
- [docling-project/docling](https://github.com/docling-project/docling) — MIT, **70.821★** — la
  capa de parsing por defecto del sector.
- [thomasunise/casecite](https://github.com/thomasunise/casecite) — Apache-2.0, 286★ — legal RAG
  self-hosted con verificación de cita y revisión tabular.
- [lawglance/lawglance](https://github.com/lawglance/lawglance) — Apache-2.0, 343★ — India.
- [AnttiHero/lavern](https://github.com/AnttiHero/lavern) — Apache-2.0, 326★ — human gates.

## Corrección de datos de pases anteriores

1. ⚠️ **La API de GitHub NO está bloqueada en este entorno.** Tres ficheros de esta KB lo
   afirmaban. Se reprobó hoy y funciona. Por creerla bloqueada, esta KB **nunca había medido
   `archived` ni `pushed_at`**, y así se le escaparon dos renombrados, un repo muerto y cuatro
   dormancias. **Un canal declarado bloqueado se vuelve a probar, nunca se hereda.**
2. ⚠️ **`microsoft/presidio` → `data-privacy-stack/presidio`** y
   **`JSv4/OpenContracts` → `Open-Source-Legal/OpenContracts`**. Firma del renombrado: `repo:`
   da 422 mientras `raw` sobre el slug viejo da 200. Presidio confirmado por **LICENSE idéntico
   (1.084 B, MD5 `edb1b1745226`) en ambos slugs**.
3. ⚠️ **`TheAtticusProject/cuad` ya no existe** (antes descartado por «vivo, sin LICENSE»).
   CUAD sigue siendo válido como concepto de benchmark; el puntero de GitHub está muerto.
4. ⚠️ **Razonamiento refutado:** `repos/trending.md` afirmaba que «el payload AGPL es prácticamente
   constante porque no interpola ningún nombre» citando 35.140 / 34.519 / 34.523 B. **Las tres
   cifras refutan la afirmación en el mismo renglón** (617 B de diferencia): courtlistener lleva un
   **preámbulo de copyright antepuesto** al texto AGPL canónico. Y su fichero es **`LICENSE.txt`**,
   no `LICENSE` — el procedimiento publicado no reproducía el resultado publicado.
5. ⚠️ **Cuatro dormancias no declaradas**, medidas por primera vez: Blackstone **28 meses**,
   lawyer-llama **27**, lexnlp **30**, DISC-LawLLM **18**, fuzi.mingcha **16**. Los dos últimos
   eran, textualmente, «los dos activos de APAC» de esta KB.
6. ⚠️ **`OpenSign` es AGPL-3.0**, no «licencia sin determinar»: la API dice `NOASSERTION`, el
   fichero son 35.051 B con 16 menciones a Affero.
7. ⚠️ **El índice equivocado estaba coronado:** `Vaquill-AI/awesome-legaltech` (273★) es 8× el
   `chen-friedman/awesome-legaltech` (34★) que esta KB usaba, y cubre servidores MCP. Mismo nombre
   de repo, dueños distintos — no es un renombrado. Se publican los dos, con su compromiso:
   Vaquill es más completo pero **sin licencia**; chen-friedman es pequeño pero **CC0**.
8. ⚠️ **«Kourti Legal» refutado.** Una fuente lo describía como practice management legal MIT y
   self-hostable — justo el hueco declarado de esta KB. **No existe.** Lo que hay: `boyeesu/Kourti`
   (MIT, 1★) y cuentas homónimas. El hueco sigue abierto, ahora con candidato nombrado y refutado.
9. ✅ **Dos conflictos de fuentes RESUELTOS** (ver `intel/market.md`): el calendario de alto riesgo
   del EU AI Act (**Digital Omnibus: Anexo III 2-dic-2027, Anexo I 2-ago-2028**; las fuentes que
   dicen ago-2026 son pre-enmienda) y la exigibilidad de la ley coreana (**el MSIT indica que 2026
   funciona de hecho como periodo piloto**).
10. ⚠️ **Conflicto NUEVO abierto:** Colorado. El pase anterior escribió «derogada y reemplazada por
    SB 189 (14-may-2026)»; las fuentes de hoy dicen que sigue viva con aplicación movida al
    **30-jun-2026 por SB 25B-004**, cubriendo servicios legales como alto riesgo. Sin resolver.

## Huecos declarados

- 🔴 **No se hallaron datos de adopción de AI legal en LATAM ni en APAC** — tercer pase
  consecutivo. Las búsquedas regionales devuelven marcos normativos y, ahora, oferta técnica; cero
  cifras de uptake por despachos o tribunales. **No inferir adopción a partir de regulación ni del
  número de repos.** Es el pendiente principal de investigación de esta KB.
- 🔴 **Oferta open source legal de origen LATAM: cero con señal**, medido hoy con vocabulario es/pt
  (4 búsquedas, resultados de 0–3★ listados en `intel/market.md`). ⚠️ Y `claude-para-abogados`, el
  único activo en castellano con tracción, es **derecho de España — EMEA, no LATAM**.
- ✅ **CERRADO el hueco «sin repos de origen EMEA/APAC».** El pase anterior lo declaró en dos
  ficheros. **Era un artefacto de búsqueda, no un hecho de mercado:** el canal `topic:` de GitHub
  devuelve activos alemanes, italianos, franceses, rumanos, coreanos, vietnamitas, taiwaneses,
  indios y chinos. **Lección de método: un hueco hallado con búsquedas en inglés sobre blogs no es
  un hueco de mercado hasta haberlo buscado en el índice de la plataforma.**
- 🔴 **No existe practice management open source permisivo con procedencia clara**, ni **firma
  electrónica open source permisiva** (OpenSign es AGPL-3.0). Huecos de mercado, no de búsqueda.
- 🔴 **eur-lex sigue inalcanzable desde este entorno** — el registro primario del EU AI Act continúa
  sin leer. Las resoluciones de arriba se apoyan en fuentes secundarias concordantes, incluidas las
  medidas independientemente por la KB de gaming, no en el Diario Oficial.
- 🔴 **Riesgo abierto sobre el entregable:** el TJUE dictará su primera decisión sobre copyright y
  AI (**Like Company v Google**) a finales de 2026 o principios de 2027. **La regla puede cambiar
  durante un proyecto** ⇒ registrar la procedencia del dato desde el día 1.

---
*v2026-11-20 — Fuentes: Thomson Reuters 2026, Clio 2026, 8am Legal Industry Report 2026,
ACC/Everlaw, Bloomberg Law, Comisión Europea (AI Office, CNIL), Latham & Watkins (APAC),
Baker Botts, Baker Donelson, MoFo, Atlantic Council, xenoss/CASRAI (LATAM), y verificación
directa por API de GitHub + lectura de LICENSE para cada repo citado.*
