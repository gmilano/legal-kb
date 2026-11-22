---
industry: legal
region: Global
updated: 2026-11-22
---

# 📡 Tendencias — Legal Services

> Última actualización: 2026-11-20

## 🆕 Tendencias del pase 3 (2026-11-21, auditoría)

### A. La comoditización llegó por arriba: cuatro verticales legales de laboratorio en seis meses
**Anthropic (12-may-2026) → Google (25-ago-2026) → OpenAI (sep-2026) → Microsoft (oct-2026).**
Los cuatro con la misma arquitectura (skills legales + conectores a las herramientas del abogado)
y **ninguno con corpus jurisdiccional propio**. Es la tendencia que reordena todas las demás:
**«construimos un asistente legal» caducó como propuesta diferenciada**, porque los cuatro lo
incluyen en una licencia de empresa que el cliente ya paga. Lo que no caducó, y es donde esta KB
tiene activos verificados: **jurisdicción, corpus redistribuible, residencia de datos y
defensibilidad**. Detalle y tabla de encaje en `intel/market.md`.

Dos consecuencias que no son obvias:
1. **Google integra `CourtListener` (AGPL-3.0) como conector de primera clase.** El corpus abierto
   pasó de alternativa barata a **infraestructura dentro del producto del hiperescalador** — lo que
   sube el valor de la capa de corpus de esta KB en vez de bajarlo.
2. **Microsoft puso 20+ skills legales dentro de Word.** Esta KB sostiene desde el primer pase que
   *el canal decisivo es Word*; la tesis se confirma y a la vez **el canal se ocupa**. La pieza
   permisiva de la KB (`ms-word-addin`, Apache-2.0) sigue siendo la respuesta correcta sólo cuando
   el cliente necesita **control del add-in y de los datos**, no cuando quiere la función.

### B. El eje regulatorio de EE. UU. giró de DIVULGAR a VERIFICAR
Connecticut (**§ 4-9, 23-jun-2026**) obliga a **verificar de forma independiente toda cita
producida por AI**; Nueva York (**Part 161, 1-jun-2026**) **no exige divulgación** y desplaza el
deber al contenido; Indiana (TR 11) hace que **la firma certifique la autenticidad de la
autoridad**. ⇒ **El requisito de producto no es un banner de divulgación, es una primitiva
ejecutable de verificación de cita.** Refuerza la tendencia nº 1 del pase 2 y le pone normas con
fecha. Y el contrapeso: el comité federal de Reglas Civiles **rechazó** una regla sobre
alucinaciones, así que **el deber concreto depende del foro**, no de una norma nacional.

### C. El retorno se declara por primera vez, y abre la brecha de gobernanza de par en par
**64% declara impacto positivo en ingresos, desde 36% en 2025** (Clio). Simultáneamente: **94% de
los despachos usa o explora GenAI** (ILTA, 500 despachos) y **sólo 9% tiene una política escrita y
realmente aplicada**. Una brecha de **85 puntos** entre uso y gobierno, con retorno ya demostrado
⇒ **la venta deja de ser evangelización y pasa a ser implantación y control.** Y la asimetría por
tamaño dice a quién: **<1/3 de los despachos pequeños captura ingresos frente a ~60% de los
grandes**; a los pequeños no les falta modelo, les falta despliegue.

### D. El formato nuevo del sector trae un déficit sistemático de licencia
Los tres repos legales **nuevos** con más tracción **no tienen fichero de licencia**:
`ai-legal-claude` (**1.852★**), `ai-legal-compliance-assistant` (342★), `contract-review-pro`
(311★) — ≈**2.500★ de material jurídicamente inutilizable** (sin licencia expresa el default es
*todos los derechos reservados*). Los tres son **skills/prompt packs**, no librerías: se publican
como contenido, desde cuentas personales, sin el reflejo de añadir `LICENSE`. Junto con
`awesome-legal-skills` (CC-BY-NC-ND, el peor régimen) y `legal-skills-open` (Apache-2.0 **sobre el
contenido**, el mejor), son **tres regímenes para un mismo formato**. ⇒ En *skills*, **la licencia
se comprueba antes que la calidad**, y **las estrellas no miden adoptabilidad**.

### E. Ley como código, y mantenida por el Estado
**`betagouv/mon-entreprise` (MIT, 337★, commit de hoy)**: el Gobierno francés mantiene derecho
laboral, fiscal y societario como **reglas ejecutables** (`publicodes`), no como prompts. Es la
prueba de existencia del argumento que esta KB defiende desde el principio — que lo defendible
ante un regulador sale de una **regla determinista**, no de generación — y con la única fuente de
autoridad que ningún modelo puede igualar. **Patrón a replicar por jurisdicción**, y el candidato
natural para el hueco LATAM (ver P12).

### F. En Brasil el límite de la AI legal no es la regulación de AI: es el colegio de abogados
El **Consejo Federal de la OAB** autorizó en **ago-2026** demandar a empresas de AI que realicen
actos reservados a la abogacía, y la **OAB-SP presentó acción civil pública contra «Enter»
(Talisman AI) el 7-oct-2026**. Brasil **no tiene ley general de AI**, así que el riesgo no llega
por donde las propuestas lo anticipan: llega por **el estatuto de la abogacía, ya vigente, con
litigio en curso**. ⇒ El producto defendible **termina en un abogado identificado que firma, y el
sistema debe poder demostrarlo**: human gates (`lavern`), registro de atribución y plantilla
determinista (`docassemble`) pasan de buenas prácticas a **requisitos de ingeniería**.

---

## Las tendencias del pase 2 (conservadas; revalidadas en el pase 3)

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

### 🆕 13. El «MCP de fuentes oficiales» es ya el patrón dominante del sector, y es medible

El pase anterior dijo que *la plantilla por jurisdicción es el patrón de producto del año* y contó
6 activos. Con consultas por **capa de arquitectura** en vez de por nombre de agente, el recuento
es **13**, y comparten una forma casi idéntica:

> **envolver las fuentes legales oficiales de un país en un servidor MCP, y exponer la
> verificación de cita como herramienta.**

| Jurisdicción | Activo | Licencia |
|---|---|---|
| 🇨🇭 Suiza | `opencaselaw` — 1M+ sentencias, grafo de citas 10M aristas | MIT + **CC0** |
| 🇰🇷 Corea | `korean-law-mcp` — 42 APIs oficiales del 법제처 | MIT |
| 🇹🇼 Taiwán | `tw-legal-rag` (22,8 M sentencias) / `mcp-taiwan-legal-db` | ⚠️ ELv2 / MIT |
| 🇩🇪 Alemania | `ayunis-legal-mcp` | MIT |
| 🇮🇹 Italia | `mcp-legal-it` (200+ tools) / `italia-mcp-servers` | Apache-2.0 / MIT |
| 🇺🇸 EE. UU. | `us-legal-mcp` | MIT |
| 🇨🇳 China | `devnors-data-mcp` | MIT |

**Implicación para Globant:** no hay que inventar la arquitectura de una oferta legal por país
— está escrita siete veces, casi siempre en MIT. **Lo que escasea no es el diseño: son las
fuentes de cada país conectadas.** Y para LATAM hay **cero**.

### 🆕 14. La licencia es una propiedad del *tag*, no del repositorio

Esta KB verificaba licencias byte a byte sobre `HEAD`. **Insuficiente.** `tw-legal-rag` (350★)
tiene en su LICENSE: *«las versiones hasta la v1.2.2 incluida se publicaron bajo MIT, que sigue
aplicando a esas versiones»* — el resto es **Elastic License 2.0**, que prohíbe ofrecer el
software como servicio gestionado a terceros.

⇒ **Las estrellas de un repo pueden haberse ganado bajo una licencia que ya no rige.** Un repo
puede volverse propietario sin cambiar de nombre, de slug ni de descripción, y los dos canales de
verificación de esta KB mirarían `HEAD` y verían la licencia nueva como si siempre hubiera estado.

Y en la dirección contraria: `awesome-legal-skills` (966★) parece permisivo por nombre y por
tamaño y es **CC-BY-NC-ND 4.0** — **NonCommercial prohíbe el engagement y NoDerivatives prohíbe
adaptarlo a la jurisdicción del cliente**, que son las dos únicas cosas que Globant haría con él.

> **Tendencia de fondo, no anécdota:** a medida que los proyectos legal-AI open source buscan
> monetizar, el relicenciamiento hacia ELv2/BUSL y el contenido bajo CC-NC van a crecer.
> **La licencia hay que verificarla en la versión que se fija y re-verificarla en cada pase.**

### 🆕 15. En LATAM la obligación de verificar citas llega por el juez, no por el legislador

Mientras Brasil, México y Colombia **no tienen ley de AI en vigor**, sus tribunales ya resolvieron:

- **Colombia, Corte Suprema (AC739-2026):** multa de **15 salarios mínimos mensuales** a un
  abogado por citar jurisprudencia inventada por AI.
- **México, dos tesis de ene-2026:** la AI puede **calcular la garantía del amparo**, pero
  **no debe alcanzar el razonamiento jurídico**.
- **Colombia, Corte Constitucional (T-008 de 2026):** remite a la contencioso-administrativa la
  cuestión de los actos administrativos redactados con AI.

⇒ **Convergencia por tres vías distintas hacia el mismo requisito técnico:** Indiana Trial Rule 11
(regla procesal, EE. UU.), Art. 50 del AI Act (reglamento, UE) y la vía judicial (LATAM).
**La verificación de cita con log auditable es el único requisito que las tres rutas comparten**, y
es el que esta KB puede implementar hoy con `opencaselaw`, `korean-law-mcp`, `tw-legal-rag` y
`CaseCite`. **Para LATAM no hay fuente conectada: ese es el trabajo.**

### 🆕 16. La capa de menor riesgo del sector legal era la que nadie había mirado

`shmsoft/FreeEed` (Apache-2.0, creado en **2011**, commit de **hoy**) es la única plataforma de
e-discovery open source viva, y hasta este pase **esta KB no tenía una sola fila en esa capa**.

**Por qué es la de menor riesgo:** el producto del e-discovery es **un conjunto de documentos
responsivos**, no un consejo jurídico. Si el sistema falla, el fallo es *recall* medible y
corregible — **no una afirmación falsa firmada por un abogado**. Es el único flujo legal donde la
alucinación no se traslada al cliente final en forma de riesgo deontológico.

⇒ **Es el punto de entrada técnicamente más defendible de un engagement legal**, y el más fácil
de justificar ante un socio reticente. Que estuviera ausente de la KB es un recordatorio:
**una capa no buscada se parece mucho a una capa que no hace falta.**

### 🆕 17. El corpus en dominio público deja de ser hipotético

Esta KB sostenía que *el corpus permisivo es más escaso que el código permisivo* y que el **grant
partido código/corpus** era el modo de fallo propio del sector. `opencaselaw` tiene el grant
partido **a favor**: **MIT el código, CC0 los datos** — 1M+ sentencias suizas, 21k leyes y un grafo
de citas de 10M de aristas **en dominio público**, descargables en Parquet.

⇒ **La conclusión se refina:** el grant partido no es el problema; **partirlo en la dirección
contraria** lo es. Y ahora hay un caso positivo que demuestra que el régimen que esta KB pide
(datos incorporables sin cadena de licencias) **es alcanzable**, lo que convierte «no existe
corpus permisivo para mi país» de excusa en **especificación de trabajo**.

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


## 🆕 PASE 4 (2026-11-21) — tres tendencias que el pase 3 no registró

### T-P4-1 — La categoría de compra ya se llama «legal LLM», y se define por el corpus
El **Legal LLM Market Report 2026** (18-nov-2026) proyecta **55,67 B USD en 2030** y nombra
**Thomson Reuters, LexisNexis, Harvey AI e Ironclad**. Que exista un informe de analista con ese
recorte significa que hay **presupuesto con ese nombre**, y la composición de la lista —dos
incumbentes de *datos jurídicos* y dos nativos de AI— confirma que **la categoría se define por
quién tiene el corpus, no por quién tiene el modelo**. Encaja exactamente con lo que esta KB midió
en el pase 3: los cuatro laboratorios frontera lanzaron vertical legal y **ninguno trae corpus
jurisdiccional propio**. ⇒ **El activo defendible de un engagement es el corpus de la
jurisdicción**, no la capa de agente, que es commodity a doce meses.

### T-P4-2 — La gobernanza de agentes se está escribiendo en APAC, no en la UE
El **IMDA de Singapur** lanzó el **Model AI Governance Framework for Agentic AI (22-ene-2026)**:
el primer marco dirigido a sistemas que **actúan**, no a modelos que generan ni a contenido que se
etiqueta. El EU AI Act regula por *riesgo de la aplicación* y el Anexo III legal no muerde hasta
dic-2027; Japón e India no tienen nada vinculante de propósito general. ⇒ **Para documentar un
despliegue agéntico hoy, el único marco de referencia disponible es singapurense y voluntario** —
lo que lo convierte en **plantilla de diseño sin coste de cumplimiento**, utilizable en cualquier
jurisdicción. **Tendencia a vigilar: que los reguladores que sí sancionan adopten su estructura.**

### T-P4-3 — Las estrellas de GitHub se están contaminando como señal: el repo como gancho comercial
Medido en esta KB este pase (`agents/top.md` → **G-L8**): el segundo repo de agente legal más
estrellado, **1.852★**, **declara en su propia `description` que es la captación de una comunidad
de pago**, no tiene fichero de licencia y lleva 8 meses sin commits. No es un caso aislado de un
vertical: el patrón **repo-como-gancho** es independiente de la industria. ⇒ **Consecuencia para
toda la rotación: a partir de este pase, «muchas estrellas» deja de ser una señal de adopción y
pasa a ser una pregunta — *¿por qué tiene estas estrellas?*.** El discriminador barato es leer la
`description` completa buscando llamada a la acción comercial, y el patrón firma es
**estrellas altas + sin licencia + dormido**.

---

## 🆕 PASE 5 (2026-11-21) — cinco tendencias, cuatro de ellas medidas en más de una región

### T-P5-1 — El caudal de activos legales nuevos **se ha secado**, y lo que los pases anteriores medían era otra cosa

Query datada y reproducible: `legal AI created:>2026-09-01 stars:>=40` → **`total_count = 4`**, y al
leer los cuatro **sólo dos son legales**, de los cuales **uno ya estaba en esta KB**. ⇒ **En once
semanas, UN repo legal nuevo cruzó los 40★.**

Esto obliga a separar dos fenómenos que esta KB venía confundiendo:

| | Qué es | Estado medido |
|---|---|---|
| **Caudal de creación** | repos legales **nuevos** con señal | **~1/mes. Seco.** |
| **Deuda de descubrimiento** | repos **preexistentes** que la KB no había encontrado | **Era enorme** (los pases 2 y 3 añadieron 7 filas cada uno, casi todas de repos antiguos) y **se está pagando** |

🔑 **Consecuencia operativa para la rotación entera:** que un pase añada muchas filas **no** indica
un ecosistema en expansión — indica que la KB venía con retraso. Una vez pagada la deuda, **un pase
horario sobre la misma industria no puede producir activos nuevos.** La cadencia útil para
`agents/top.md` y `repos/foundations.md` es **semanal o mensual**; lo que rinde cada hora es
**verificación, corrección y cierre de huecos.**

### T-P5-2 — 🔑 El competidor no es Harvey: es **ChatGPT dentro del despacho**

La herramienta de AI más usada en despachos **de todos los tamaños** sigue siendo la **genérica**
(ChatGPT, Microsoft Copilot): **43–48%** (Clio 2026). En APAC, **94%** usa alguna AI pero sólo
**46%** usa AI legal especializada (LexisNexis, n=1.715, 10 mercados). **La brecha entre esas dos
cifras es el mercado**, y está ocupada hoy por herramientas **sin trazabilidad, sin verificación de
cita y sin registro de auditoría**.

Y se cierra con los otros dos datos del pase: **64%** de los despachos que usan AI declara **efecto
positivo en ingresos** (Clio) **mientras** las sanciones por citas alucinadas se intensifican en
número y severidad, con **descalificación, revocación de *pro hac vice* y traslado al colegio**
(ABA). ⇒ **El valor ya se está capturando con herramientas que no son defendibles.** Ése es el
argumento comercial completo, y no requiere convencer a nadie de que adopte AI.

### T-P5-3 — «Adoption is near universal, governance is not» aparece **en las cuatro regiones a la vez**

Por primera vez esta KB puede documentar el mismo diagnóstico, en el mismo trimestre, con fuentes
independientes por región:

| Región | Formulación medida | Fuente |
|---|---|---|
| **APAC** | el titular literal: *«adoption is near universal, governance is not»* | LexisNexis, n=1.715 |
| **EMEA** | adopción casi universal en UK&I, con **integración y gobernanza responsable** como el problema pendiente | Clio UK&I 2026 |
| **North America** | los 40 despachos de ≥500 abogados usan AI legal, y **no todos tienen política de uso**; *vetting*, formación y gobernanza son lo que **frena** el despliegue | Bloomberg Law |
| **LATAM** | difusión temprana pero acelerando, con marcos regulatorios **en construcción** y obligaciones que llegan por vía **sectorial y judicial** | BID, FPF, IBA |

⇒ **Deja de ser una hipótesis de posicionamiento y pasa a ser un hecho replicado.** La gobernanza
es el cuello de botella en los cuatro mercados simultáneamente, lo que significa que **el mismo
entregable se vende en los cuatro**, cambiando sólo el instrumento normativo que lo justifica
(Art. 50 en la UE, reglas procesales y colegiales en EE. UU., ley coreana en APAC, juez y colegio
en LATAM).

### T-P5-4 — El punto de entrada se desplaza del despacho **al consumidor**

**46% de los consumidores consultaría a una AI antes de contactar a un abogado** (Clio 2026). Es la
cifra con más consecuencias estratégicas del pase: parte de la demanda **ya no entra por el
despacho**. Y es la única tendencia de esta KB cuya base abierta está **madura y permisiva**:
`docassemble` (MIT, 200+ instalaciones, Suffolk LIT Lab) nació precisamente ahí. Ver P3.

### T-P5-5 — La ausencia de e-signature permisiva es **estructural**, no un hueco de búsqueda

Medido sobre los **tres proyectos más grandes** del segmento: DocuSeal **AGPL-3.0** (19.110★),
Documenso **AGPL-3.0** (15.841★), OpenSign **AGPL-3.0 + carve-out** (7.316★); LibreSign AGPL-3.0.
**Cuatro de cuatro copyleft de red.** Con esa unanimidad, la explicación no es casualidad: en firma
electrónica el valor está en la **confianza y el cumplimiento normativo**, y el copyleft de red es
precisamente la licencia que protege a un proveedor SaaS de que le forkeen el producto. ⇒ **Para un
entregable cerrado, esta capa se compra. Para un despliegue interno del cliente, DocuSeal o
Documenso son viables** (AGPL no contamina sin distribución ni servicio a terceros). **Es una
decisión de modelo de negocio, no técnica**, y conviene decírselo al cliente así.

### T-P5-6 — `NOASSERTION` de GitHub **no** significa «sin licencia» (y esta KB lo estaba tratando así)

Dos casos en un solo pase, uno por cada lado de la regla de bytes 932-G1: **Mayan EDMS** (586 B ⇒
puntero **Apache-2.0** genuino) y **OpenSign** (35.051 B ⇒ **AGPL-3.0 compuesta** con carve-out).
**Los dos eran adoptables y los dos los clasifica GitHub como `NOASSERTION`.** El descarte legítimo
no es la clasificación del proveedor, es **la ausencia medida del fichero** (404 en `LICENSE`,
`LICENSE.md`, `LICENSE.txt`, `LICENCE`, `COPYING` × `HEAD`/`main`/`master`). **Aplicar en las 12
industrias: toda fila descartada por `NOASSERTION` sin abrir el fichero debe revisarse.**

---

## 🆕 PASE 6 (2026-11-21) — seis tendencias, y una de ellas invierte quién es el comprador

### T-P6-1 — El turno agéntico dejó de ser pronóstico: **15% ya lo usa**, y la gobernanza no va detrás

Thomson Reuters mide **15% de profesionales legales usando ya AI agéntica**, con **41% de despachos
en AI generativa (desde 28%)**. El dato que lo vuelve urgente no es el 15%, es el que va al lado:
el **8am *2026 Legal Industry Report*** mide **54% de despachos sin ninguna formación en AI** y sólo
**46% con AI de propósito general implantada**, frente a **69% de ejercientes individuales que ya
la usan**. ⇒ **La adopción individual va por delante de la institucional, y la formación va por
detrás de las dos.** Un agente que actúa (no que sugiere) dentro de una organización que no ha
formado a nadie es el perfil de riesgo que las sanciones de 2026 ya están castigando. **Para
Globant: el entregable que se vende aquí no es el agente, es el *gate* + la formación + el
inventario de herramientas aprobadas.**

### T-P6-2 — 🔴 **El tribunal se convierte en comprador**, y compra algo distinto de lo que compra el despacho

Es la novedad estructural del pase. Hasta ahora esta KB mapeaba dos compradores: despacho e
in-house. Aparece un tercero, con presupuesto y mandato propios:

- **Nueva York:** política interina del sistema judicial que **obliga a formación en AI a todos los
  jueces y al personal** y **restringe la AI generativa a herramientas aprobadas**.
- **Indiana, Trial Rule 11 (1-ago-2026):** la firma del escrito **certifica que la autoridad citada
  es auténtica**, con cobertura expresa de los escritos asistidos por AI.

⇒ El poder judicial no compra productividad: compra **lista de herramientas aprobadas, formación y
trazabilidad**. Es un comprador que exige **evaluación y documentación**, no demos — y es
precisamente lo que un benchmark permisivo (`LegalBench`, `legal-agent-workshop`) y un `resolver_cita`
auditable sirven. **Y es un comprador al que la hipótesis «el competidor es ChatGPT» no aplica**:
ahí el genérico está directamente prohibido.

### T-P6-3 — El perímetro de cumplimiento se fragmenta **por debajo del Estado**, en dos continentes a la vez

Dos mediciones independientes del mismo fenómeno:

- **Argentina:** sin ley nacional, la obligación llegó **subnacional y administrativa** — **Santa
  Fe, Decreto 2726/2025** y **Provincia de Buenos Aires, Resolución 4/2025**.
- **EE. UU.:** el mosaico estatal (Colorado — con exigibilidad movida al **30-jun-2026** y alcance
  que **incluye decisiones sobre servicios legales** —, Texas TRAIGA **1-ene-2026**, California
  SB 942) y ahora **el conflicto federal-estatal litigado**: orden ejecutiva instruyendo al DOJ y
  **Artificial Intelligence Litigation Task Force creada el 9-ene-2026**.

⇒ **Consecuencia de arquitectura, no de *compliance*:** la política no puede estar cableada a un
país. Tiene que ser **configuración por jurisdicción, hasta nivel provincial/estatal, con fecha de
entrada en vigor como dato**. Es la generalización del patrón «plantilla por jurisdicción» (T4) de
la capa de contenido a la capa de política. Y en EE. UU. hay que añadir una variable que esta KB no
tenía: **qué norma estatal sobrevivirá al litigio** — Colorado ya se movió una vez.

### T-P6-4 — En Brasil cambió **el ejecutor**, no la ley de AI

**PL 2338/2023 sigue trabado** en la Cámara (aprobado en Senado dic-2024), y eso llevaba a esta KB
a leer Brasil como «regulación pendiente». Falso: **el 25-feb-2026 la ANPD pasó a agencia
reguladora plena**, con más autonomía técnica, administrativa y financiera. ⇒ **El riesgo exigible
hoy en Brasil llega por datos personales (LGPD), con un regulador que acaba de ganar estatuto**, no
por una futura ley de AI. Súmese el eje electoral, que sigue siendo el más rápido y vinculante de
la región (prohibición de que la AI recomiende candidatos o señale preferencia de voto + divulgación
obligatoria de contenido de campaña generado con AI). **Regla general que se confirma por segundo
año: en LATAM, antes de preguntar por la ley de AI, pregúntese quién puede sancionar hoy.**

### T-P6-5 — El precio se desacopla del asiento

Varias previsiones del sector coinciden en que los proveedores de AI legal **abandonan el SaaS por
asiento hacia modelos por uso**. Es coherente con T-P6-1: un agente que ejecuta tareas consume de
forma muy desigual entre usuarios, y el asiento deja de medir valor. ⚠️ **Es una previsión, no una
medición** — se registra como tal. Pero tiene una consecuencia inmediata y poco obvia para un
engagement: **si el cliente va a pagar por uso, la eficiencia de *tokens* del diseño pasa a ser un
requisito contractual**, y eso favorece arquitecturas con recuperación dirigida (MCP de fuente
oficial, que trae el artículo exacto) frente a RAG de contexto ancho.

### T-P6-6 — Europa es la región de **mayor adopción del mundo**, y la brecha genérico/especializado es el mercado

Dos encuestas independientes, y juntas confirman por tercera vez el reencuadre del pase 5:

- **ACC/Everlaw:** **61% de juristas in-house europeos** usan AI — **la tasa más alta del mundo,
  por delante de EE. UU.** Se acabó el supuesto de que la regulación frena la adopción europea.
- **Wolters Kluwer/Legisway:** **56%** de los departamentos legales europeos usan herramientas
  **generales** (ChatGPT y similares); **sólo 14%** ha implantado **AI legal especializada**.

⇒ **La brecha 56/14 en la única región donde el Art. 50 ya es exigible** es la formulación más
limpia del argumento comercial de esta KB: el valor se está capturando **con herramientas no
defendibles**, y ahí no hay que convencer a nadie de adoptar AI. Coincide con APAC (**94% alguna AI
vs 46% especializada**, LexisNexis n=1.715) y con NA (**41% despachos vs 54% sin formación**).
**Tres regiones, tres encuestas, el mismo hueco.** Y el requisito operativo en EMEA lo está
escribiendo el **colegio profesional**, más rápido que el legislador: guía del **CCBE** (oct-2025),
directrices de la **OVB** (Flandes) y la **NOvA** (Países Bajos).

### ⚠️ Discrepancia de fuentes que este pase deja registrada en vez de resolver

Sobre el **Omnibus** del AI Act: un rastreador lo da por promulgado como **Reglamento (UE)
2026/1744** (lo que esta KB publica desde el pase 3), otras fuentes lo describen como **acuerdo
político del 7-may-2026 pendiente de adopción formal y publicación en el DOUE**. El calendario de
esta KB **no cambia** (Art. 50 vigente 2-ago-2026 · Anexo III dic-2027 · Anexo I ago-2028) y es la
tercera corroboración tras gaming y enterprise. **Pero un cliente que lea otra fuente verá otro
calendario**, así que el argumento de venta no debe depender de cuál tiene razón: véndase el
**inventario fechado** (patrón ya adoptado en la KB de gaming), que es correcto en ambos mundos.


## 🆕 Tendencias del pase 7 (2026-11-22)

### T21. El benchmark legal dejó de ser académico y pasó a publicarlo **el vendedor**, en licencia permisiva

El cambio estructural del año en evaluación legal **no ocurrió en la universidad**:

| | Académico | Del vendedor |
|---|---|---|
| Activo | `HazyResearch/legalbench` | `harveyai/harvey-labs` (Harvey LAB) |
| Licencia | **NOASSERTION**, por tarea (30 de 162 NonCommercial) | **MIT a nivel de repositorio** |
| Tareas | 162 | **2.010** (>1.200 al lanzar en may-2026 → 1.749 → 2.010) |
| Qué incluye | dataset | dataset **+ harness + rúbricas + juez + informes** |
| Último commit | 2026-03-30 | **2026-11-12** |

Harvey no publica el banco de pruebas por altruismo: **publicar el estándar de medida es cómo se
define la categoría**. Y el efecto secundario es real y aprovechable — **el harness de evaluación
más completo del sector legal es MIT**, con adaptadores para Anthropic, OpenAI, Google, Meta, xAI y
Mistral, lo que permite a Globant comparar **su** agente contra frontera sobre tareas de M&A, data
room y contratación in-house sin construir nada.

⚖️ **Y el contrapeso, que va en la propuesta y no en una nota al pie:** `LawNext` observó en el
lanzamiento que LAB es *«un benchmark construido por un participante del mercado»*. Las tareas y
las rúbricas codifican **la definición de buen trabajo legal del equipo de Harvey**. La postura de
esta KB es usar **tres** definiciones (`harvey-labs` permisivo, `legalbench` académico filtrado,
`thunlp/CAIL` en chino) y **declarar cuál se usó**, porque en el momento en que un benchmark lo
publica el competidor, *qué se mide* es tan negociable como *cuánto se puntúa*.

### T22. La verificación de cita terminó de migrar de **buena práctica** a **certificación firmada**

El pase 3 registró que el eje regulatorio de EE. UU. giraba de **divulgar** a **verificar**. Este
pase mide el final de ese recorrido, y el salto es cualitativo:

- **Indiana, 1-ago-2026:** la **firma** de un escrito **certifica que la autoridad citada es
  auténtica**, y la regla cubre expresamente los escritos asistidos por AI.
- **Brasil:** sin provimento de la OAB sobre AI generativa a julio de 2026 — y aun así ya se
  sanciona, vía **Estatuto da Advocacia** y **litigância de má-fé**.
- **Nueva York (UCS):** AI generativa limitada a **herramientas aprobadas** + formación obligatoria.

> **La tendencia, formulada para que sirva en las doce industrias:** cuando una tecnología toca una
> profesión regulada, la obligación vinculante **no llega por la ley de la tecnología, llega por el
> deber profesional preexistente** — que ya está vigente, no tiene calendario y no admite cabildeo.
> Las leyes de AI de EE. UU. están en litigio federal; **el deber de certificar lo que firmas, no.**

Consecuencia de producto: la función que vende **no es «nuestro modelo alucina menos»** — es
**«este sistema produce la evidencia que tu firma certifica»**. Es la diferencia entre `casecite` /
`kancelaria-lex` / `opencaselaw` (que **resuelven la cita contra la fuente** y dejan traza) y
cualquier asistente que simplemente escriba mejor.

### T23. Dos pases seguidos con el caudal de repos nuevos seco: la curación venció al descubrimiento

`legal AI created:>2026-08-01 stars:>=25` ⇒ **10 repos en casi cuatro meses**, de los cuales **6 ya
estaban en esta KB**, 2 no son legales y 2 se descartaron por licencia o relevancia. **Cero
incorporaciones netas por descubrimiento.**

Y sin embargo este pase corrigió la licencia del activo del que colgaba toda la capa de evaluación,
midió 6 filas que estaban en `n/d`, cerró el censo de renombrados sobre 93 slugs y añadió el
benchmark más grande del sector. **El valor de un pase horario ya no está en encontrar: está en
verificar lo que se encontró.** Esta es la tercera medición consecutiva que lo dice, y es el
argumento estructural contra repetir industria dentro del mismo día.

### T24. La brecha de gobernanza tiene por fin un par de números comparables

**APAC: 94% usa AI, 58% trabaja bajo una política de AI.** Un 36% de uso descubierto, en la región
con la adopción más rápida y la gobernanza más débil. Combinado con lo que esta KB ya medía —que la
herramienta más usada en despachos de **todos** los tamaños es **genérica** (43–48%)— la tendencia
es una sola y se repite en las cuatro regiones:

> **El valor ya se está capturando con herramientas que no son defendibles.** No hay que convencer
> a nadie de adoptar AI; hay que sustituir una adopción que ya ocurrió y que nadie puede auditar.
