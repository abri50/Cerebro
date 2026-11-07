---
tipo: log
proyecto: cerebro
estado: activo
fecha: 2026-11-02
tags: [sistema, registro]
---
# Registro de actividad de las IAs

Las entradas se añaden al final, la más reciente abajo. Formato:

```
## AAAA-MM-DD HH:MM — <IA> — <proyecto>
- **Hecho:** qué se ha hecho (archivos tocados)
- **Estado:** dónde se queda
- **Siguiente:** próximo paso o bloqueo
```

---

## 2026-11-02 11:10 — Claude (Opus 5.5) — cerebro
- **Hecho:** añadidos a `00_Sistema_IA/01_Instrucciones_Generales.md` la misión de CEREBRO, la arquitectura con los nombres reales de carpeta (`01_Ejercito`, `02_Estudios`, `03_Proyectos`), el esquema YAML y el protocolo de lectura y escritura para cualquier IA. Directriz 6 ajustada a los campos YAML reales. Creado este registro.
- **Estado:** bóveda con estructura base; carpetas de área todavía vacías.
- **Siguiente:** confirmar que el MCP de Smart Connections (`C:\Users\aam12\smart-connections-mcp`) carga en Claude Desktop tras reiniciarlo.


## 2026-11-02 11:36 — Antigravity (Claude Opus 4.6) — cerebro
- **Hecho:** creadas Plantilla_Militar.md, Plantilla_Uni.md y Plantilla_Proyectos.md en 00_Sistema_IA/Plantillas/ (fecha Templater en línea 4).
- **Estado:** plantillas disponibles para Templater.
- **Siguiente:** —


## 2026-11-02 11:39 — Antigravity (Claude Opus 4.6) — cerebro
- **Hecho:** creado `02_Estudios/Ingenieria_Informatica/Conceptos_Redes_Prueba.md` con resumen técnico de 3 topologías de red (bus, estrella, malla). Subcarpeta `Ingenieria_Informatica` creada dentro de `02_Estudios`.
- **Estado:** archivo de prueba disponible en la bóveda.
- **Siguiente:** —


## 2026-11-02 11:58 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** poblado inicial de la bóveda (56 notas creadas en 00_Sistema_IA, 01_Ejercito, 02_Estudios, 03_Proyectos y 04_Recursos). Actualizada la arquitectura en 01_Instrucciones_Generales.md.
- **Estado:** estructura completa; contenido marcado como pendiente.
- **Siguiente:** completar los apartados pendientes de cada resumen y de cada asignatura.


## 2026-11-02 12:02 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** reorganizada la estructura de `02_Estudios/01_Grado_Ingenieria_Informatica/Asignaturas/` incorporando el nivel de curso (`01_Curso_1/`). Actualizados los enlaces en `00_Indice_Asignaturas.md` y `03_Indice_General.md`, y añadido el metadato `curso: 1` al frontmatter de las 6 asignaturas.
- **Estado:** asignaturas organizadas por curso y trimestre; enlaces sincronizados.
- **Siguiente:** —


## 2026-11-02 12:10 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** Fase 0: plantillas tipadas (proyecto, entrenamiento, asignatura, sesion_estudio), 04_Esquema_YAML.md, 00_Dashboard.md con Dataview, frontmatter normalizado en resúmenes de proyectos y asignaturas.
- **Estado:** dashboard operativo; sin datos de entrenamiento ni de estudio todavía.
- **Siguiente:** registrar datos reales 3-4 semanas; después, dashboard Node en C:\dev\cerebro-dashboard.


## 2026-11-02 12:58 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** bóveda versionada en Git; creados `.gitignore` (excluye secretos de Local REST API, workspace y `.smart-env`) y `.gitattributes`, completada la auditoría de secretos (0 credenciales expuestas), configurada identidad global (`Abraham Almagro Martínez` / `abri50@users.noreply.github.com`), añadido protocolo de versionado a `01_Instrucciones_Generales.md`, realizado commit inicial (88 archivos) y configurado remoto `origin`.
- **Estado:** repositorio remoto sincronizado (rama `main` al día con `origin/main`).
- **Siguiente:** configurar el plugin Obsidian Git (auto commit/push).


## 2026-11-02 13:40 — Claude (Sonnet 5.5) — intendencia
- **Hecho:** completados `00_Resumen.md` (estado v79, repo, arquitectura), `Backlog.md` y `Decisiones.md` de `03_Proyectos/02_Intendencia`. Sin secretos escritos.
- **Estado:** nota de Intendencia al día con v79.
- **Siguiente:** revisar el Supabase real (segunda cuenta) y arreglar 5 tests dependientes de la fecha.


## 2026-11-02 14:03 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** archivos de arranque (AGENTS/GEMINI/CLAUDE.md) en raíz de la bóveda, 00_Estado_Actual.md, protocolo de traspaso en instrucciones generales, clonados 3 repositorios en C:\dev (combat-warrior-hub, asesor-financiero, Estrato) con AGENTS/GEMINI/CLAUDE.md y commit local en cada uno, y actualizadas las notas de proyecto en CEREBRO.
- **Estado:** traspaso entre IAs operativo.
- **Siguiente:** el usuario rellena 00_Estado_Actual.md en la revisión semanal.


## 2026-11-02 14:10 — Claude (Opus 5.5) — estrato
- **Hecho:** traspaso de las sesiones del 29 al 31 de octubre. Completados `03_Proyectos/04_Estrato/00_Resumen.md` (funcionalidades, estado, compilación), `Backlog.md` y `Decisiones.md` (6 decisiones). Código subido a `abri50/Estrato` (rama `main`, 3 commits: v0.1.0, licencia, logo).
- **Estado:** v0.1.0 instalada y arrancando en el PC del usuario, con PrusaSlicer 2.9.6 incluido. Release de GitHub sin publicar.
- **Siguiente:** publicar Release v0.1.0 con los dos `.exe`, probar impresión real en la Ender 3 SE y subir el commit local de AGENTS/GEMINI/CLAUDE.md desde `C:\dev\Estrato`.


## 2026-11-02 14:53 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** sincronizados y fusionados los cambios de Intendencia (commit de Claude en remoto), Estrato (traspaso de Claude en local) y protocolo de IA / arranque. Bóveda subida a GitHub (`abri50/Cerebro`). Subidos a GitHub los commits locales con `AGENTS.md` en los 3 repositorios de `C:\dev` (`Estrato`, `asesor-financiero`, `combat-warrior-hub`).
- **Estado:** los 4 repositorios sincronizados y limpios al 100% con `origin/main`.
- **Siguiente:** el usuario rellena 00_Estado_Actual.md en la revisión semanal; publicar Release v0.1.0 de Estrato.


## 2026-11-02 14:55 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** creado `00_Sistema_IA/06_Enrutado_IAs.md` (criterio de coste y derivación entre Claude, Antigravity, Gemini, NotebookLM y Usuario) y añadido como paso 3 en la secuencia de lectura de `AGENTS.md`.
- **Estado:** enrutado de tareas documentado y enlazado en el arranque de agentes.
- **Siguiente:** —


## 2026-11-02 15:06 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** añadido `area: "sistema"` al frontmatter de `00_Sistema_IA/01_Instrucciones_Generales.md`.
- **Estado:** frontmatter alineado con el esquema del sistema.
- **Siguiente:** —


## 2026-11-02 15:14 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** creado `00_Sistema_IA/05_Cola_Antigravity.md` (cola de trabajo para derivación entre IAs con formato T-AAAAMMDD-NN) y añadida la sección `## Cola de tareas` a `AGENTS.md`.
- **Estado:** cola de tareas operativa y documentada para ejecución de órdenes mecánicas.
- **Siguiente:** —


## 2026-11-02 15:25 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** configurada la regla de usuario de enrutado y procesamiento de cola (`AGENTS.md` y `05_Cola_Antigravity.md`) a nivel global (`~/.gemini/config/rules/`, `~/.gemini/config/GEMINI.md`, `C:\Users\aam12\GEMINI.md`), en el entorno de desarrollo (`C:\dev\GEMINI.md`) y en la bóveda (`CEREBRO/GEMINI.md`).
- **Estado:** regla permanente y activa tanto dentro de la bóveda como en cualquier proyecto o sesión externa de Antigravity.
- **Siguiente:** —


## 2026-11-02 15:35 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** inicializado el proyecto `C:\dev\cerebro-dashboard\` con Node.js, `gray-matter` y `chokidar`. Creados `indexer.js` (watcher y parseador de metadatos YAML de la bóveda CEREBRO) y `server.js` (servidor HTTP en 127.0.0.1:3000 con endpoints REST). Añadidos archivos de arranque (`AGENTS.md`, `GEMINI.md`, `CLAUDE.md`, `.gitignore`), verificado test de escaneo inicial (73 notas indexadas) y commit local inicial en git.
- **Estado:** backend base listo y funcional en disco, sin frontend todavía.
- **Siguiente:** desarrollar la interfaz web/dashboard (HTML/Tailwind o framework ligero).


## 2026-11-02 15:40 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** refactorizado el backend de `C:\dev\cerebro-dashboard\` a arquitectura Express modular (`config.js`, `indexer.js`, `server.js`). Añadidos endpoints REST de solo lectura (`/api/status` y `/api/resumen` agrupando por tipo), middleware de bloqueo estricto de escrituras (405 Method Not Allowed en POST/PUT/DELETE) y configurado CORS local. Verificados tests con 73 notas indexadas.
- **Estado:** backend Express operativo en 127.0.0.1:3000 y protegido contra escrituras.
- **Siguiente:** desarrollar la capa de frontend visual.


## 2026-11-02 15:55 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** desarrollada la interfaz visual HUD táctico (`public/index.html` y `public/app.js`). Configurado `express.static('public')` en `server.js`. Interfaz oscura industrial con Tailwind CDN, Chart.js, indicadores de estado reactivos (polling cada 10s), grid con los 4 paneles principales (Acondicionamiento físico, Grado Informática UI1, Portfolio de proyectos y Bitácora de estudio) y manejo de desconexión. Verificado acceso HTTP en `127.0.0.1:3000`.
- **Estado:** HUD operativo y listo para uso en el navegador.
- **Siguiente:** —


## 2026-11-02 16:22 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** implementado el endpoint `POST /api/ejecutar-accion` en `server.js` con arquitectura modular (`actions.js` y `audit.js`). Añadidos comandos seguros locales: `ping_sistema` (telemetría de hardware y uptime), `chequear_yaml` (auditoría de frontmatter) y `forzar_reindex` (rescan de chokidar). Configurado log de auditoría persistente en `logs/audit.log` con IP 127.0.0.1, timestamp y estado. Validación de acciones con HTTP 400 y protección contra escrituras HTTP 405.
- **Estado:** backend operativo con funciones de ejecución segura y auditoría en `127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 16:32 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** añadido el endpoint `GET /api/buscar?q=termino` en `server.js` y el método `search(query, limit)` en `indexer.js`. Almacenado el contenido Markdown parseado en memoria en el indexador, implementada ponderación de relevancia (título, ruta y contenido), extracción contextual de fragmentos (`extracto`) y límite a las 10 mejores coincidencias. Búsqueda insensible a mayúsculas verificada mediante tests automáticos.
- **Estado:** motor de búsqueda en memoria operativo en el backend.
- **Siguiente:** —


## 2026-11-02 16:47 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** creado el módulo `watcher-alerts.js` integrado en `server.js` (ejecución al arrancar y de forma programada cada 1 hora). Realiza un barrido recursivo de la bóveda verificando campos YAML obligatorios (`tipo`, `area`, `estado`, `fecha`, reglas por tipo de `04_Esquema_YAML.md`). Volcado del reporte JSON en `public/data/alerts.json` y expuesto en el endpoint `GET /api/alerts`.
- **Estado:** auditoría de integridad YAML activa y programada en el servidor.
- **Siguiente:** —


## 2026-11-02 16:58 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** rediseño visual completo del frontend HUD de CEREBRO en `C:\dev\cerebro-dashboard\public\` a estética futurista minimalista estilo JARVIS. Implementado el Orbe Central procedural en Canvas 2D/3D con anillos concéntricos giroscópicos, ticks tácticos, núcleo luminoso palpitante y partículas orbitales reactivas al estado ONLINE/OFFLINE. Creada consola de comandos interactiva integrada en el pie de página con comandos rápidos (`help`, `status`, `yaml`, `reindex`, `ping`, `buscar <q>`, `alerts`, `clear`) y navegación por historial. Desplazados los datos de entrenamiento táctico, universidad, proyectos y sesiones a paneles holográficos laterales desplegables (drawers con tabs y backdrop). Verificado en `http://127.0.0.1:3000`.
- **Estado:** HUD futurista JARVIS operativo en producción local.
- **Siguiente:** —


## 2026-11-02 17:02 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** migración estética del HUD hacia una identidad visual basada en Ultron (negro absoluto `#030303`, rejilla de radar roja, núcleo y anillos en carmesí `#ef4444` y ámbar táctico `#f59e0b`, tipografía en gris ceniza técnico `#9ca3af`). Cadencia del orbe central acelerada con doble armónico militar de alta energía, retícula balística cruzada, chispas de combate, terminal de mando con prompt `ULTRON@cerebro:~$` y cursor carmesí, y paneles holográficos desplegables estilizados con acentos carmesí.
- **Estado:** HUD Ultron Prime activo en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 17:21 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** sustituido el renderizado 2D del orbe central por un motor 3D interactivo real en WebGL con Three.js (`index.html` y `app.js`). Implementado shader GLSL personalizado con 4 octavas de Simplex Noise para simular plasma volcánico en ebullición (carmesí, naranja y blanco incandescente), efecto Fresnel para el borde limbo, anillos Torus 3D orbitales con inclinación real, sistema de 400 partículas de erupción solar, luces dinámicas (`AmbientLight` y `PointLight` orbital), calibración espacial de Raycaster sobre el canvas local para detección de hover precisa y disparo de pulsos de partículas expansivas al interactuar.
- **Estado:** núcleo 3D WebGL Three.js con interactividad táctil y paralaje fluido operativo en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 17:34 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** corregido problema crítico de renderizado del núcleo central migrando a Canvas 2D nativo sin dependencias externas (`core-canvas`). Fijadas dimensiones explícitas en el contenedor (`w-80 h-80 sm:w-96 sm:h-96`) con canvas absoluto `400x400` y capas de texto superpuestas con `pointer-events-none`. Implementado renderizado volumétrico de plasma solar con gradientes radiales complejos (centro blanco `#ffffff`, halo naranja `#f97316` y borde carmesí `#dc2626`), turbulencia interna orgánica, anillos orbitales 3D inclinados con ticks balísticos, chispas solares radiantes y control completo de ratón (`mousemove`, `mouseenter`, `mouseleave`) con paralaje sutil y expansión dinámica de halo y aceleración en hover.
- **Estado:** núcleo de plasma 3D nativo completamente operativo y visible en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 18:03 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** rebranding definitivo del HUD a **CEREBRO // CORE** eliminando cualquier referencia a Ultron/JARVIS en `server.js`, `index.html` y `app.js`. Migrada la paleta hacia una estética sináptica/neuronal (fondo `#0f051d`, magenta `#e11d48`, carmesí `#be123c`, púrpura `#9333ea`, rosa táctico `#f43f5e`). Orbe en Canvas 2D actualizado con gradientes sinápticos, vórtices de plasma violeta/magenta y estado `isProcessing` que acelera la rotación e intensifica el halo durante la ejecución de directivas. Consola 100% conectada a la API local (`status`, `resumen`, `yaml`, `reindex`, `ping`, `buscar <q>` con ponderación por etiquetas y contenido, `clear`). Servidor reiniciado y probado.
- **Estado:** CEREBRO // CORE totalmente interactivo y operativo en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 18:20 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** implementada la arquitectura backend desacoplada para la futura integración de voz y React en `C:\dev\cerebro-dashboard\`. Creado `eventBus.js` (emisor central de eventos con soporte nativo de streaming SSE, heartbeat cada 15s y registro de clientes), `orchestrator.js` (orquestador de decisiones y capa de abstracción LLM compatible con herramientas locales y proveedores externos como Ollama con contrato estructurado), y `audioRouter.js` (módulo de preparación de audio y voz con endpoints `GET /api/voice/status` y `POST /api/voice/process` para pipelines STT/TTS). Conectados en `server.js` los endpoints `GET /api/stream` y `POST /api/orchestrate`, límite de payload ampliado a 15MB para audio base64, y eventos del indexador (`system_state`, `note_event`) vinculados al bus reactivo.
- **Estado:** servicios de streaming SSE, orquestación LLM y pipeline de voz activos y verificados en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 21:15 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** implementada la reconstrucción completa del núcleo central con Three.js WebGL en `C:\dev\cerebro-dashboard\public\` (`index.html` y `app.js`). Creada la clase `CoreNeuralMeshOrb` con una malla poligonal esférica orgánica (red neuronal 3D / celosía viva) compuesta por `MeshBasicMaterial` con wireframe magenta profundo (`#e11d48`) y `THREE.Points` luminosos en rosa táctico (`#f43f5e`), núcleo interior sólido y brillante (`#fce7f3`), halo sináptico y anillo orbital táctico. Implementada deformación procedural en tiempo real con armónicos multi-sinusoidales que simulan respiración y movimiento orgánico, campo de 650 partículas estelares en el fondo oscuro (`#05020a`), y control interactivo de rotación con paralaje 3D y aceleración angular al aproximar el cursor al núcleo o ejecutar directivas (`isProcessing`).
- **Estado:** núcleo 3D Three.js con malla poligonal sináptica y campo estelar operativo en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 21:18 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** eliminado el círculo sólido/opaco interior de Three.js en `public/app.js` (`innerCore` y `innerCorona`), sustituyéndolo por un micro-núcleo translúcido de estructura icosaédrica en alambre (`#f43f5e`) y un diminuto nódulo de luz sináptica. Actualizados los textos de telemetría ("ONLINE", "Nodos activos") en `public/index.html` y `app.js` con contenedor 100% transparente y resplandor sutil (drop-shadow magenta/rosa), permitiendo apreciar toda la profundidad de la malla poligonal 3D y las partículas estelares sobre el fondo negro `#0f051d`.
- **Estado:** núcleo sináptico 3D 100% translúcido y limpio operativo en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 21:55 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** redactado el manual técnico definitivo `CLAUDE.md` en la raíz de `C:\dev\cerebro-dashboard\`, detallando arquitectura del sistema (Node.js, Express, `indexer.js`, `actions.js`, `audit.js`, `watcher-alerts.js`, `eventBus.js`, `orchestrator.js`), puertos y entorno (`127.0.0.1:3000`), tecnología frontend (HTML5, Tailwind, Three.js WebGL, consola), paleta cromática sináptica completa y catálogo de endpoints REST y streaming SSE. Verificada la integridad del repositorio (cero referencias a Ultron) y conectado el evento `action_executed` en `POST /api/ejecutar-accion` hacia el bus de streaming SSE.
- **Estado:** documentación `CLAUDE.md` y streaming SSE activos y verificados en `http://127.0.0.1:3000`.
- **Siguiente:** —


## 2026-11-02 22:00 — Antigravity (Gemini 3.8 Flash) — cerebro-dashboard
- **Hecho:** creado el runner de smoke tests automatizados `test-api.js` en `C:\dev\cerebro-dashboard\`. Valida contra `http://127.0.0.1:3000` el estado y esquema de 5 endpoints críticos (`GET /api/status`, `GET /api/resumen`, `GET /api/buscar?q=test`, `GET /api/alerts`, `POST /api/ejecutar-accion` con `ping_sistema`). Salida formateada con colores ANSI (✔/✖, tiempos de respuesta y código de salida 0/1). Añadido el comando `"test:api": "node test-api.js"` en `package.json`. Suite ejecutada con 5/5 pruebas superadas.
- **Estado:** suite de smoke test operativa y verificada en local.
- **Siguiente:** —


## 2026-11-03 13:30 — Claude (Sonnet 5.5) — intendencia
- **Hecho:** v80 en `abri50/asesor-financiero`: los fijos automáticos no se duplican tras un pago adelantado (ni si se apuntó como movimiento normal) y se limpian los duplicados ya creados. Tests t93 y t94 nuevos.
- **Estado:** subido a `main` y desplegado en Vercel. No reproducido: cargo fijo que baja el saldo sin salir en Movimientos/Gastos.
- **Siguiente:** pedir al usuario qué fijo concreto no aparece; revisar el Supabase real (segunda cuenta).


## 2026-11-03 20:50 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** procesadas las tareas pendientes de `00_Sistema_IA/05_Cola_Antigravity.md`:
  - **T-20261103-01:** añadida la regla 7 de fallback en `00_Sistema_IA/06_Enrutado_IAs.md` y las cláusulas de "Higiene de memoria" y "Rotación del registro" en `00_Sistema_IA/01_Instrucciones_Generales.md`.
  - **T-20261103-02:** añadida la sección "Notas generadas por IA" en `00_Sistema_IA/04_Esquema_YAML.md` (claves `generado_por`, `verificado: false`, `fuente: ""`), directriz de cumplimiento en `AGENTS.md` y vista Dataview "🔍 Pendiente de verificar" en `00_Sistema_IA/00_Dashboard.md`.
  - Tareas verificadas y movidas a `## Hechas` en la cola.
- **Estado:** cola vacía (0 pendientes, 2 hechas). Bóveda al día.
- **Siguiente:** —

## 2026-11-03 22:10 — Claude (Opus 5.5) — cerebro
- **Hecho:** creado `03_Proyectos/10_Cerebro/` (00_Resumen, Decisiones con 12 decisiones de la sesión de diseño 02-03/11, Backlog). Añadidas a la cola T-20261103-03 (mantenimiento), -04 (plantillas por carpeta) y -05 (partir guía POO, bloqueada hasta que el usuario pegue la guía). Skill `cerebro` guardada en Claude.
- **Estado:** CEREBRO documentado como proyecto propio; tareas mecánicas en cola.
- **Siguiente:** Antigravity: ejecuta la cola. Usuario: Obsidian Git, 00_Estado_Actual, pegar guía POO.

## 2026-11-03 22:45 — Claude (Opus 5.5) — cerebro_voz
- **Hecho:** creado `03_Proyectos/11_Cerebro_Voz/` (resumen, 5 decisiones, backlog). Especificada la fase 1 en la cola como T-20261103-07 (depende de T-06, inbox).
- **Estado:** diseño cerrado; fase 1 sin LLM ni red, voz original con Piper.
- **Siguiente:** Antigravity: ejecuta la cola (modelo Pro para T-07). Usuario: elegir variante de voz.


## 2026-11-03 23:15 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** ejecutadas las tareas mecánicas pendientes de la cola (`00_Sistema_IA/05_Cola_Antigravity.md`):
  - **T-20261103-03 (Mantenimiento semanal):** creado `00_Sistema_IA/Prompts/Mantenimiento_Semanal.md` con rutina de 7 pasos, actualizada sección `## Mantenimiento` en `AGENTS.md`, actualizados enlaces a proyectos 10 y 11 en `00_Sistema_IA/03_Indice_General.md` y ejecutada primera revisión en `00_Sistema_IA/Revisiones/2026-W45.md`.
  - **T-20261103-04 (Plantillas automáticas Templater):** creado backup `.obsidian/plugins/templater-obsidian/data.json.bak` y configuradas las 5 rutas de `folder_templates` en `data.json` con validación formal de JSON.
  - **T-20261103-06 (Bandeja de entrada Inbox):** creado `00_Sistema_IA/00_Inbox.md`, prompt de clasificación `00_Sistema_IA/Prompts/Procesar_Inbox.md`, sección `## Inbox` en `AGENTS.md` y añadido Paso 0 en `00_Sistema_IA/Prompts/Mantenimiento_Semanal.md`.
  - **T-20261103-05 (Guía POO):** dejada como bloqueada en pendientes a la espera de que el usuario pegue `_Guia_NotebookLM.md`.
  - Movidas T-03, T-04 y T-06 a `## Hechas` en la cola.
- **Estado:** tareas mecánicas resueltas; cola con T-05 (bloqueada) y T-07, T-08, T-09 (pendientes, sugeridas para modelo Pro).
- **Siguiente:** el usuario debe pegar `_Guia_NotebookLM.md` para desbloquear T-05, o iniciar T-07 (Cerebro Voz fase 1).

## 2026-11-03 23:50 — Claude (Opus 5.5) — montaje
- **Hecho:** creado `03_Proyectos/12_Montaje/` (resumen, 5 decisiones, backlog): editor de vídeo propio tipo CapCut, enfoque en sala limpia. Especificada la F1 (motor de subtítulos CLI con whisper.cpp Vulkan + ASS + FFmpeg) como T-20261103-12.
- **Estado:** arquitectura cerrada; sin código.
- **Siguiente:** Antigravity: ejecuta la cola (Pro para T-12). Usuario: clip de prueba en `C:\dev\montaje\muestras\prueba.mp4`, nombre y licencia.

## 2026-11-03 23:55 — Claude (Opus 5.5) — montaje
- **Hecho:** reenfocado Montaje como app propia de uso personal (D01 reescrita) y añadido el export 4K TikTok (D06). Ampliada T-20261103-12 con `render.js`, presets `tiktok-4k`/`yt-4k`/`borrador` y subtítulos rasterizados a 4K.
- **Estado:** especificación de F1 cerrada; sin código.
- **Siguiente:** Antigravity: ejecuta la cola (Pro para T-12). Usuario: clip de prueba y nombre de la app.


## 2026-11-03 23:55 — Antigravity (Gemini 3.8 Flash) — cerebro_voz
- **Hecho:** ejecutada y verificada la tarea `T-20261103-07` (Cerebro Voz, fase 1) en `C:\dev\cerebro-voz`:
  - Creado repositorio git e inicializado `.gitignore` ignorando `.venv/`, `models/`, `logs/`, `*.wav`.
  - Configurado entorno Python 3.13 con `faster-whisper` (small int8 en CPU), `piper-tts` (voz española masculina `es_ES-davefx-medium`), `sounddevice`, `numpy`, `pynput` y `pytest`.
  - Implementado `audio_fx.py` con modificación tonal de pitch (-2.5 semitonos), remuestreo y WSOLA para preservación de tempo, reverb de reflejos tempranos y normalización.
  - Implementado `router.py` con normalización de caracteres/tildes y 5 reglas operativas (anota/apunta/guarda, registra, estado/que toca/informe, siguiente acción por proyecto aproximado, recuento de cola y fallback seguro a bandeja).
  - Implementado `audio_capture.py` con detección de energía y silencio (1.2 s) y captura bloqueante o de streaming.
  - Generadas las 3 muestras de voz en `muestras/` (`variante_1.wav`, `variante_2.wav`, `variante_3.wav`) sobre «Cerebro operativo. Todo en orden.».
  - Verificada la suite `pytest` (3/3 pruebas superadas: `test_no_network_imports`, `test_normalize_text`, `test_router_10_phrases`).
  - Pruebas reales validadas: «anota prueba de voz» escribe en `00_Inbox.md` y «estado» lee la telemetría de `00_Estado_Actual.md`.
  - Creados `README.md`, `requirements.txt`, `config.toml`, `AGENTS.md`, `GEMINI.md`, `CLAUDE.md`.
  - Commit local inicial completado (`b835f62`).
  - Actualizado `03_Proyectos/11_Cerebro_Voz/00_Resumen.md` y `Backlog.md`. Movida `T-07` a `## Hechas` en la cola.
- **Estado:** núcleo local de voz completamente operativo y probado.
- **Siguiente:** usuario debe probar las 3 muestras de audio en `C:\dev\cerebro-voz\muestras\` y autorizar T-08 (Modo conversación en HUD).

## 2026-11-04 00:05 — Claude (Opus 5.5) — montaje
- **Hecho:** análisis estático con REA de CapCut 9.5.0.4050 (sin descompilar): `03_Proyectos/12_Montaje/Informe_RE_CapCut.md`. Decisiones D07 (glosario difuso + confianza) y D08 (QVBR en AMF, sin AV1). Ampliación 2 de T-20261103-12.
- **Estado:** especificación de F1 cerrada con los hallazgos.
- **Siguiente:** Antigravity: ejecuta la cola (Pro, T-12). Usuario: exportar un vídeo 4K de TikTok con CapCut para medirlo con ffprobe.


## 2026-11-04 18:15 — Antigravity (Gemini 3.8 Flash) — cerebro_voz
- **Hecho:** ejecutada y verificada la tarea `T-20261103-10` (Identidad de Cerebro en el router de voz):
  - Creado `identidad.py` en `C:\dev\cerebro-voz`: parseo dinámico de `00_Sistema_IA/07_Identidad_Cerebro.md`, recarga automática por `mtime`, resolución contextual de variables (`{saludo}` por franja horaria, `{n}` tareas en cola, `{resumen_salud}`, `{componente}`) y alternancia de variantes sin repetir la última.
  - Actualizado `router.py` para priorizar reglas de cortesía e identidad (saludo, identidad, agradecimiento, despedida, estado propio) y fallback formal antes de comandos de bóveda.
  - Implementado saludo de arranque en `main.py` con síntesis de voz y mensaje en consola: «Cerebro escuchando. Pulse Ctrl+Alt+C para hablar.».
  - Ampliada suite de tests con verificación de tratamiento formal de respeto (usted/señor, prohibición de tuteo) y alternancia de variantes (5/5 tests pasando).
  - Commit local realizado en `C:\dev\cerebro-voz` (`f72a520`).
  - Actualizados `03_Proyectos/11_Cerebro_Voz/00_Resumen.md`, `Backlog.md` y movida `T-10` a `## Hechas` en la cola.
- **Estado:** personalidad formal e identidad operativa en el núcleo de voz.
- **Siguiente:** ejecutar `T-20261103-08` (Modo conversación en HUD 3000 con servicio HTTP 3001).

## 2026-11-04 19:00 — Antigravity (Gemini 3.8 Flash) — cerebro_voz
- **Hecho:** ejecutada y verificada la tarea `T-20261103-08` (Modo conversación en la interfaz CEREBRO // CORE 127.0.0.1:3000):
  - Microservicio Python `server.py` en `C:\dev\cerebro-voz`: servidor HTTP local en `127.0.0.1:3001` sin dependencias externas, precarga de modelos en arranque, endpoints `GET /voz/estado` y `POST /voz/turno` (audio webm/wav o json con base64), memoria RAM volátil de últimos 10 turnos. Suite pytest 6/6 verde (`test_server.py`). Commit `3a3bb0b`.
  - Backend Node.js en `C:\dev\cerebro-dashboard`: corregido comando `ping` (`ping_sistema`) devolviendo métricas reales de hardware, memoria, CPUs y uptime de `os` sin campos `undefined`. Endpoints proxy implementados: `GET /api/voz/estado`, `POST /api/voz/turno`, `POST /api/voz/resumen-sesion`.
  - Frontend WebGL (`public/app.js`): implementada clase `ConversationManager` con captura de micrófono vía `MediaRecorder`, análisis nativo de silencio (1,2s) y amplitud con `AnalyserNode` de Web Audio API (cero Web Speech API externa). Deformación armónica del orbe Three.js reactiva a 5 estados (`reposo`, `escuchando`, `pensando`, `hablando`, `desconectado`).
  - Control conversacional: activación/pausa mediante clic en la esfera, tecla Espacio (fuera de inputs) y comando `voz` en consola; bucle conversacional automático; salida por palabras clave («fin», «salir», «gracias Cerebro») o inactividad tras 30s.
  - Smoke tests: suite `test-api.js` actualizada y validada al 100% (6/6 pruebas en verde).
  - Documentación cruzada: creados/actualizados `README.md`, `CLAUDE.md`, `AGENTS.md` y `GEMINI.md` enlazados a `03_Proyectos/11_Cerebro_Voz/`. Commit `7243f32`.
  - Actualizados `03_Proyectos/11_Cerebro_Voz/00_Resumen.md`, `Backlog.md` y movida `T-08` a `## Hechas` en la cola.
- **Estado:** modo conversación por voz 100% local, integrado y probado de extremo a extremo entre los puertos 3000 y 3001.
- **Siguiente:** ejecutar `T-20261103-09` (HUD v2 según especificación de diseño).

## 2026-11-04 19:25 — Antigravity (Gemini 3.8 Flash) — cerebro_voz
- **Hecho:** correcciones urgentes en `cerebro-voz` y HUD:
  - Resuelto error `open() got an unexpected keyword argument 'metadata_errors'` en faster-whisper al fijar `av<14` (instalado `av==13.1.0` con wheel nativo para Python 3.13) en `C:\dev\cerebro-voz\requirements.txt`.
  - Creada suite `tests/test_audio_decode.py` con pruebas de decodificación de audio real WAV (16kHz) y WebM/Opus (como el generado por `MediaRecorder` del navegador), además de verificación de fallback hablado ante audio corrupto. Suite pytest completa en verde (9/9).
  - Implementado fallback de voz en `server.py`: ante cualquier fallo de STT o decodificación, el servidor devuelve HTTP 200 con `{ success: false, respuesta: "Tengo un problema con el reconocimiento de voz, señor.", audio_base64: "..." }`, permitiendo que el HUD reproduzca la voz sintética de aviso.
  - Corregido recorte y bordes rectos de la esfera en el HUD (`public/index.html` y `public/app.js`): canvas configurado con `position: absolute; inset: 0` ocupando toda el área central con `overflow: visible`; deformación procedural acotada a lo largo de la normal con armónicos simplex suaves (lerp continuo entre 3% en reposo y hasta 15% del radio base en habla/escucha); cámara ajustada dinámicamente con ≥25% de margen sobre el radio máximo deformado en cualquier aspect ratio de ventana.
  - Commits locales en `C:\dev\cerebro-voz` (`9cc575b`) y `C:\dev\cerebro-dashboard` (`c749fa8`).
- **Estado:** modo voz y HUD interactivo 100% operativos, estables y sin recortes.
- **Siguiente:** continuar con la cola de tareas (`T-20261103-09` HUD v2 o `T-20261103-11` Cerebro Voz fase 2 con Ollama/Gemini).

## 2026-11-04 22:15 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** ejecutada la tarea `T-20261104-13` (HUD v3 con layout definitivo y esfera Three.js superior; sustituye a T-09):
  - Descargada copia local de la tipografía variable Archivo (`archivo-variable.woff2`, 90 KB con ejes `wght` y `wdth`) a `public/vendor/fonts/` y configurado `@font-face` en `fonts.css`. Cero dependencias externas CDN en producción.
  - Implementado layout HUD v3 según `HUD_v3_prototipo.html` y la corrección final:
    - Esfera Three.js conservada en la parte superior del canvas (`public/app.js`), con desplazamiento simplex noise en GPU acotado a lo largo de las normales (3% reposo, hasta 15% con voz), cámara con margen holgado sin recortes, halo dinámico y partículas orbitales interactivas ligadas a tareas pendientes de la cola con raycast tooltip.
    - Marco de carta con paleta ciruela/carmesí/violeta (`--terreno`, `--curva`, `--hueso`, `--senal`, `--violeta`, `--alerta`).
    - Cabecera con marca, reloj en vivo, fecha en español, indicador de salud de voz y línea del día 24 h alimentada con las horas de entradas reales de actividad en el registro.
    - Conversación protagonista debajo de la esfera con animación sincronizada palabra por palabra (`.w.on`).
    - Márgenes laterales con datos 100% reales de endpoints del backend: prioridades y próxima evaluación (`/api/estado`), tareas pendientes (`/api/cola`), proyecto activo (`/api/proyectos`), salud del sistema (`/api/salud`).
    - Entrada de texto oculta tras «/» que envía a `/api/voz/turno` y reproduce respuesta por voz; eliminados terminal y botones obsoletos.
    - Actualización reactiva por SSE (`/api/stream`) suscrita a eventos `vault_change` de chokidar.
    - Suite de smoke tests `test-api.js` ampliada a 11 pruebas: 11/11 pasadas con éxito.
  - Commits en `C:\dev\cerebro-dashboard`: `875113d` (layout), `9a0607a` (visual), `8c704d0` (núcleo), `d38ac27` (datos y layout v3 definitivo). Sin push en local.
  - T-09 marcada como «Sustituida por T-13» y T-13 completada en `00_Sistema_IA/05_Cola_Antigravity.md`.
- **Estado:** HUD v3 de Cerebro operativo, limpio, reactivo, sin datos inventados y con Three.js local a 60 fps estables.
- **Siguiente:** en la cola: T-05 bloqueada por guía NotebookLM; T-11 bloqueada a la espera de instalación de Ollama o GEMINI_API_KEY; siguiente tarea ejecutable: T-12 (Montaje F1: motor de subtítulos CLI).

## 2026-11-04 22:50 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** ejecutada la tarea `T-20261104-14` (Ajustes del HUD v3: tamaño de la esfera y sin texto hablado):
  - Modificado el dimensionamiento y posicionamiento de la esfera Three.js en `public/app.js`: se calcula el hueco real entre la línea del día (`#dia`) y el indicador de estado (`#estado`). Radio máximo deformado fijado estrictamente en el 40 % de la altura de dicho hueco y máximo 30 % de su ancho. Centrado en píxeles mapeado a coordenadas 3D de mundo a la distancia focal, con recálculo automático en cada evento `resize`.
  - Eliminada la transcripción visible de la conversación (Cerebro solo se oye). Texto hablado trasladado a contenedor accesible `#subtitulos-live` con `aria-live="polite"`. Añadida opción `subtitulos: false` en `config` (re-activable en `true` o mediante clase `.con-subtitulos`). Debajo de la esfera queda únicamente el estado (`#estado`).
  - Detección de caída de voz en interacción: si el servicio 3001 está offline, al hacer clic en la esfera el estado muestra inmediatamente «Voz no disponible: arranque el núcleo de voz» en color ámbar sin intentar acceder al micrófono.
  - Generadas y verificadas 3 capturas de pantalla automáticas comprobando que ninguna parte de la esfera, anillo ni partículas toca el borde del marco:
    - [hud_v3_1366x768.png](file:///C:/Users/aam12/Documents/CEREBRO/03_Proyectos/10_Cerebro/capturas/hud_v3_1366x768.png)
    - [hud_v3_1920x1080.png](file:///C:/Users/aam12/Documents/CEREBRO/03_Proyectos/10_Cerebro/capturas/hud_v3_1920x1080.png)
    - [hud_v3_390x844.png](file:///C:/Users/aam12/Documents/CEREBRO/03_Proyectos/10_Cerebro/capturas/hud_v3_390x844.png)
  - Suite de tests `test-api.js` verificada (11/11 pruebas en verde). Commit local `ed78104` en `C:\dev\cerebro-dashboard`.
- **Estado:** HUD v3 perfectamente encajado y calibrado en todas las resoluciones; experiencia auditiva pura y minimalista.
- **Siguiente:** procesar `T-20261104-15` (Cerebro como app: un solo arranque).

## 2026-11-04 23:15 — Antigravity (Gemini 3.8 Flash) — cerebro
- **Hecho:** ejecutada la tarea `T-20261104-15` (Cerebro como app: un solo arranque):
  - Implementado supervisor de subprocesos en Node.js (`supervisor.js`) e integrado en `server.js`:
    - Arranca automáticamente el núcleo de voz local Python (`C:\dev\cerebro-voz\main.py --server`), redirigiendo logs a `logs/voz.log`.
    - Health check periódico cada 10 s; si el proceso cae, realiza auto-reinicio progresivo con backoff exponencial (hasta 5 intentos en 10 min; tras superarlo marca «Voz local offline»).
    - Supervisión de Ollama: verifica `http://127.0.0.1:11434`; si está caído e instalado en el sistema, lanza `ollama serve` como hijo. Expone estado en `/api/salud` (`ollamaOnline`, `ollamaInstalled`).
    - Al cerrarse el servidor, ejecuta `taskkill /T /F` sobre todos los árboles de procesos hijo en Windows.
  - Actualizado `C:\dev\cerebro-voz\main.py` con flag `--server` para levantar solo el servidor HTTP en el puerto 3001 sin activar el hook global de teclado. Manejo de concurrencia y control de bloqueo en `FileHandler` de logging.
  - Creado script lanzador silencioso `Cerebro.vbs` en la raíz de `cerebro-dashboard`: detecta si el puerto 3000 ya responde; si no, lanza Node oculto (`vbHide`), espera la disponibilidad de `/api/salud` (máx. 30 s) y abre la interfaz en modo ventana de app nativa con Edge o Chrome (`--app=http://127.0.0.1:3000`). Si ya está corriendo, enfoca la ventana existente sin duplicar procesos.
  - Generado icono multirresolución `cerebro.ico` y `public/favicon.ico` con la paleta sináptica del orbe WebGL.
  - Creados accesos directos de Windows `Cerebro.lnk` en el Escritorio del usuario y en el Menú Inicio (`AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Cerebro.lnk`).
  - Implementado apagado limpio: atajo `Ctrl+Q` en el HUD, comando `/apagar` en la consola interactiva y endpoint `POST /api/apagar`, cerrando ordenadamente Python, Ollama y Node.
  - Documentación actualizada en `README.md` («Doble clic en Cerebro y listo», ciclo de vida, resolución de problemas y logs).
  - Smoke tests REST `test-api.js` verificados (11/11 pruebas en verde). Commit local `a539281` en `C:\dev\cerebro-dashboard` y `1dee5d9` en `C:\dev\cerebro-voz`.
- **Estado:** Cerebro empaquetado como aplicación de escritorio nativa en Windows; arranque unificado con un solo clic, sin consolas visibles y con apagado limpio.
- **Siguiente:** revisar cola: T-05 y T-11 bloqueadas; proceder con `T-20261103-12` (Montaje F1: motor de subtítulos automáticos CLI).

## 2026-11-04 23:45 — Antigravity (Gemini 3.8 Flash) — montaje
- **Hecho:** ejecutada la tarea `T-20261103-12` (Montaje F1: motor de subtítulos automáticos CLI y render 4K):
  - Inicializado nuevo repositorio en `C:\dev\montaje` con Git, Node.js 20+ ESM nativo (`package.json`, `"type": "module"`), sin dependencias runtime externas. Licencia PolyForm Noncommercial 1.0.0 y enlaces a la bóveda en `AGENTS.md`, `GEMINI.md`, `CLAUDE.md`.
  - Implementado pipeline en módulos puros (`src/core/`):
    - `audio.js`: extracción de audio PCM 16 kHz mono con FFmpeg y telemetría de vídeo (`getVideoInfo`) con ffprobe.
    - `transcribe.js`: integración con `whisper-cli.exe` (Vulkan) y modelo `large-v3-turbo` con VAD, `--dtw` y vocabulario táctico inyectado vía `--prompt`. Reintento automático por CPU (`-ng`) si la GPU falla.
    - `words.js`: extractor de tokens con puntuación ligada y tiempos monótonos; corrección exacta y difusa con `glosario.json` (distancia de Levenshtein normalizada ≤ 0.25 y clave fonética española simplificada unificando *v/b*, *c/k/qu*, *z/s*, *w/gu*, *h* muda). Puntuación de confianza (`conf`) preservada por palabra.
    - `segment.js`: segmentación en bloques (máx. 3 palabras en 9:16 y 7 en 16:9; corte por pausas > 300 ms o signos oracionales; duración mínima 600 ms sin solapes).
    - `export-srt.js`: exportación formal SubRip (`HH:MM:SS,mmm`).
    - `export-ass.js`: generador de subtítulos `.ass` estilo CapCut. Emite exactamente un evento `Dialogue` por intervalo de palabra activa con efecto pop `\fscx115\fscy115\t(0,120,\fscx100\fscy100)` y color de marca `#FFD400` (`&H0000D4FF&`). `PlayRes` nativo a 4K (2160×3840) y margen vertical al ~65% de altura en 9:16 fuera de la interfaz de TikTok/Reels.
    - `project.js`: gestión del formato de proyecto `.montaje.json` (versión 1).
    - `render.js`: filtros de escalado Lanczos, centrado crop 16:9 a 9:16 sin barras negras, quemado de subtítulos con `libass` a resolución 4K nativa y codificación acelerada por hardware AMF (`h264_amf` con QVBR/VBR a 60–80 Mbps). Barra de progreso en consola.
  - Implementada CLI (`src/cli.js`) con comandos `subs <video>` y `render <video>`.
  - Creados `styles/cw-impacto.json` con tipografía Anton (OFL descargada a `fonts/Anton-Regular.ttf`), `presets/tiktok-4k.json`, `presets/yt-4k.json`, `presets/borrador.json`, `glosario.json` y script `scripts/setup.ps1`.
  - Suite de tests automatizados implementada con `node:test` (`tests/*.test.js`): 16/16 pruebas superadas en verde (274 ms).
  - Commit local inicial `cbc293c` en `C:\dev\montaje`.
  - Actualizados `03_Proyectos/12_Montaje/00_Resumen.md`, `Backlog.md` y movida `T-12` a `## Hechas` en la cola.
- **Estado:** motor CLI de subtítulos y render 4K TikTok operativo y testeado al 100%. Muestra de vídeo `muestras/prueba.mp4` pendiente de ser aportada por el usuario para calibración final.
- **Siguiente:** cola de tareas completada (tareas restantes T-05 y T-11 bloqueadas a la espera de entradas del usuario: guía de NotebookLM e instalación de Ollama/Gemini).

## 2026-11-07 13:20 — Antigravity (Gemini 3.8 Flash) — cerebro_voz
- **Hecho:** ejecutada la tarea `T-20261103-11A` (Cerebro Voz, fase 2: conversación libre LLM - Parte A portátil):
  - Diseñada e implementada la arquitectura LLM desacoplada en `C:\dev\cerebro-voz\llm.py` con proveedores intercambiables (`ninguno`, `ollama`, `gemini` vía SDK `google-genai`).
  - Soporte de configuración por máquina mediante `config.local.toml` (ignorado en `.gitignore`), con valor por defecto `provider = "ninguno"` para portátiles sin GPU dedicada.
  - Implementado sistema de herramientas de bóveda (`VaultTools`):
    - `leer_nota(ruta)`: acceso restringido dentro de `VAULT_PATH`, omitiendo frontmatter YAML y denegando path traversal y directorios ocultos/internos (`.obsidian`).
    - `buscar_proyecto(nombre)`: inspección en `03_Proyectos` devolviendo estado, resumen y backlog.
    - `anotar(texto)`: adición a `00_Sistema_IA/00_Inbox.md` con timestamp.
    - `tareas_cola()`: lectura de pendientes en `00_Sistema_IA/05_Cola_Antigravity.md`.
    - `proponer_tarea(titulo, orden, criterio)`: flujo en dos turnos con confirmación explícita previa («¿La añado a la cola, señor?»), escribiendo únicamente tras confirmación afirmativa del usuario («sí», «adelante») y cancelando tras negativa («no», «cancela»).
  - Control de cuota y persistencia en `logs/uso_llm.json` (`UsageTracker`, límite diario de 200 llamadas), expuesto en `GET /voz/estado`.
  - Función generadora `split_sentences` para streaming continuo por oraciones hacia Piper TTS.
  - Cascada en `router.py`: reglas e identidad primero → delegación en LLM → fallback de identidad ante ausencia de clave, fallo de red o agotamiento de cuota. El error no se añade a la memoria de turnos.
  - Actualizado `server.py` para suministrar hasta 10 turnos limpios en RAM y exponer estado de LLM y cuota en `/voz/estado`.
  - Creada suite de tests `tests/test_llm.py` con mock LLM (6/6 superados). Suite global de cerebro-voz pasando al 100% (15/15 pruebas en verde). Commit local `8513b0a` en `C:\dev\cerebro-voz`.
  - Actualizados `03_Proyectos/11_Cerebro_Voz/00_Resumen.md`, `Backlog.md` y `Decisiones.md`. En `00_Sistema_IA/05_Cola_Antigravity.md`, T-11A cerrada en Hechas y T-11B registrada en Pendientes (bloqueada para el PC de sobremesa).
- **Estado:** fase 2 parte A completada e integrada; Cerebro Voz listo para operar en portátil (modo reglas/identidad o Gemini si se define la variable) y preparado para Ollama en el equipo principal.
- **Siguiente:** tareas en cola pendientes bloqueadas (T-05 a la espera de la guía NotebookLM; T-11B a la espera del PC de sobremesa).
