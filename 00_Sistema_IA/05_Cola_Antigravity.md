---
tipo: "indice"
area: "sistema"
fecha: 2026-11-02
estado: "activo"
tags: ["sistema", "cola"]
---
# Cola de tareas para Antigravity
Formato de cada tarea (las añade Claude u otra IA al final de "Pendientes"):

```
### T-AAAAMMDD-NN — <título corto>
- **Proyecto:** <slug o cerebro>
- **Orden:** <instrucciones completas y verificables>
- **Criterio de hecho:** <cómo comprobar que está bien>
- **Modelo sugerido:** flash | pro
```

## Pendientes
##### T-20261103-05 — Partir la guía de POO en notas por unidad
- **Proyecto:** cerebro (estudios)
- **Orden:** BLOQUEADA hasta que el usuario pegue la guía de NotebookLM en `02_Estudios/01_Grado_Ingenieria_Informatica/Asignaturas/T1_Trimestre_1/01_Diseno_Programacion_Orientada_Objetos/Apuntes/_Guia_NotebookLM.md`. Entonces:
  1. Divídela en `UD1_Paradigma_POO.md`, `UD2_Java.md`, `UD3_Encapsulacion.md` y `Complementario_Python.md` (frontmatter: tipo "apuntes", area "universidad", fecha real, asignatura "diseno_programacion_orientada_objetos", tags ["universidad", "apuntes", "poo"], generado_por "notebooklm", verificado false, fuente "Guía NotebookLM sobre el temario UI1").
  2. Mueve la sección de trampas de examen a `Errores.md` (crea la nota si no existe) bajo `## Trampas conocidas`.
  3. Añade al final de cada nota de unidad una sección `## Por comprobar` con estas correcciones donde apliquen: Java tiene 4 niveles de visibilidad (public, protected, package-private, private); falta sobrecarga vs sobrescritura y ligadura dinámica; constructor por defecto desaparece al declarar uno con parámetros; Java permite implementar varias interfaces; `true`/`false` en minúscula en Python da NameError, no error de sintaxis; `__str__` que devuelve tupla lanza TypeError; Eclipse+PyDev no forma parte de la ejecución del intérprete; la anécdota del bug está adornada.
  4. Borra `_Guia_NotebookLM.md` solo cuando las notas estén creadas y verificadas (Git conserva el original).
- **Criterio de hecho:** 4 notas de unidad + `Errores.md` con frontmatter válido y secciones «Por comprobar».
- **Modelo sugerido:** flash
- **Estado:** Bloqueada: a la espera de que el usuario pegue la guía de NotebookLM en `02_Estudios/01_Grado_Ingenieria_Informatica/Asignaturas/01_Curso_1/T1_Trimestre_1/01_Diseno_Programacion_Orientada_Objetos/Apuntes/_Guia_NotebookLM.md`.

##### T-20261103-11B — Ollama en el PC principal
- **Proyecto:** cerebro_voz
- **Orden:**
  1. Instalar Ollama para Windows en el PC principal de sobremesa.
  2. Comprobar con `ollama ps` que el modelo se carga en la GPU (RX 6900 XT, 16 GB) y no en la CPU.
  3. Probar y medir 3 modelos instruct candidatos (7B-14B cuantizados con buen español) con 10 preguntas de prueba, documentando latencia y calidad en el README.
  4. Fijar `llm_provider = "ollama"` en `config.local.toml` del PC principal.
- **Criterio de hecho:** `ollama ps` muestra el modelo en VRAM de la GPU; Cerebro responde preguntas abiertas en < 3 s en el PC; tabla en README.
- **Modelo sugerido:** pro
- **Estado:** Bloqueada: requiere el PC de sobremesa.

## Hechas
##### T-20261107-16 — Palabra de activación «Oye Cerebro»
- **Proyecto:** cerebro_voz
- **Resultado:** Completado el 2026-11-07.
  1. **Evaluación de viabilidad y arquitectura desacoplada:** El entrenamiento sintético local de openWakeWord requiere dependencias POSIX/Linux (`piper-sample-generator`) y datasets masivos no viables en Windows/portátil CPU. Siguiendo la decisión del usuario, se implementó toda la infraestructura base modular tras la interfaz abstracta `DetectorActivacion` en `C:\dev\cerebro-voz\wake_word.py`, con implementaciones `DetectorMock`, `DetectorOpenWakeWord` (preparado para `models/oye_cerebro.onnx` con ONNXRuntime) y `DetectorPorcupine`.
  2. **Escucha continua y privacidad estricta:** Implementado `WakeWordListener` en hilo en segundo plano con `sounddevice` en bloques de 80 ms (1280 muestras a 16 kHz mono). El audio se analiza en memoria y se descarta de inmediato; no se almacena ni persiste nada hasta que se detecta la palabra. VAD por compuerta de energía (RMS < 0.003) para evitar cómputo de inferencia en silencio.
  3. **Exclusión mutua del micrófono (`MicrophoneLock`):** Sistema thread-safe de bloqueo de dispositivo. Garantiza un único dueño del micrófono a la vez; si el usuario inicia un turno mediante clic en el HUD o atajo de teclado, la escucha de la palabra clave cede el acceso cooperativamente sin colisiones de audio.
  4. **Ciclo de turno y ventana de réplica:** Al detectar la palabra de activación:
     - Emite el evento reactivo `despertar` vía HTTP hacia `POST /api/eventos` del dashboard, difundiéndolo por SSE (`/api/stream`) a los clientes web (la esfera cambia a «Escuchando» y emite un tono suave de aviso).
     - Graba el turno con detección de silencio (`AudioRecorder`), transcribe con `faster-whisper`, procesa el turno con `router.py` y reproduce la respuesta sintetizada mediante `tts.speak()`.
     - Abre una ventana de réplica interactiva de 8 segundos permitiendo réplicas encadenadas sin repetir «Oye Cerebro», regresando a reposo tras agotarse el tiempo en silencio.
  5. **Comandos de voz y control en el HUD:**
     - Comandos de voz en el router: *«Cerebro, deja de escuchar»* (pausa la escucha activa) y *«Cerebro, vuelve a escuchar»* (la reanuda).
     - Endpoint REST `GET /voz/escucha` y `POST /voz/escucha` (con toggle en el backend Node y estado en `/api/salud`).
     - Comando de consola interactiva `/escucha` en el HUD.
     - Indicador en tiempo real en la cabecera: `«Voz local lista · Escucha activa»` / `«Voz local lista · Escucha pausada»`.
  6. **Suite de tests automatizados y commits:**
     - Creada suite unitaria `tests/test_wake_word.py` (5/5 superadas) validando muestras positivas y negativas, exclusión de micrófono, pausa/reanudación y comandos de voz. Suite completa de `cerebro-voz` en verde (20/20 pruebas). Commit local `096bd09` en `C:\dev\cerebro-voz`.
     - Suite REST de `cerebro-dashboard` ampliada en `test-api.js` (12/12 superadas). Commit local `a513313` en `C:\dev\cerebro-dashboard`.
##### T-20261103-11A — Cerebro Voz, fase 2: conversación libre (LLM) - Parte A
- **Proyecto:** cerebro_voz
- **Resultado:** Completado el 2026-11-07.
  1. **Arquitectura y Configuración por Equipo:** implementado `llm.py` desacoplado con proveedores intercambiables (`ninguno` | `ollama` | `gemini`). Soporte para `config.local.toml` (ignorado por Git) para definir la configuración específica por máquina. En el portátil queda configurado con `provider = "ninguno"` por defecto (modo reglas puras).
  2. **Herramientas de Bóveda (Function Calling):**
     - `leer_nota(ruta)`: lectura segura acotada dentro de `VAULT_PATH`, rechazando path traversal y carpetas ocultas/internas como `.obsidian`. Omite frontmatter YAML.
     - `buscar_proyecto(nombre)`: búsqueda en `03_Proyectos` devolviendo estado y resumen.
     - `anotar(texto)`: añade línea a `00_Sistema_IA/00_Inbox.md` con marca de tiempo.
     - `tareas_cola()`: extrae tareas pendientes de `00_Sistema_IA/05_Cola_Antigravity.md`.
     - `proponer_tarea(titulo, orden, criterio)`: prepara la propuesta sin escribir en disco, requiriendo confirmación explícita por voz/texto («¿La añado a la cola, señor?»). Solo escribe tras confirmación afirmativa del usuario («sí», «adelante»), permitiendo cancelación («no», «cancela»).
  3. **Límites y Control de Coste:** implementado `UsageTracker` con persistencia en `logs/uso_llm.json` (máx. 200 llamadas/día por defecto). Expuesto en `GET /voz/estado` del núcleo Python.
  4. **Streaming por Frases:** función `split_sentences` para trocear la respuesta en oraciones y enviarlas progresivamente a Piper TTS.
  5. **Integración con Router y Servidor:** `router.py` evalúa reglas e identidad primero; si nada encaja deriva a LLM; ante fallos de red o límite diario recurre al fallback formal de la identidad sin corromper la memoria volátil de turnos. `server.py` pasa el historial de turnos válidos como contexto.
  6. **Suite de Pruebas Automatizadas:** implementada `tests/test_llm.py` (6/6 pasando) con mock LLM, verificando fallback sin clave, rechazo de límites diarios, seguridad de acceso a la bóveda y flujo condicional de confirmación de tareas. Suite completa de cerebro-voz en verde (15/15 tests superados).
  7. **Commit Local:** commit `8513b0a` en `C:\dev\cerebro-voz`.
##### T-20261103-12 — Montaje F1: motor de subtítulos automáticos (CLI)
- **Proyecto:** montaje
- **Resultado:** Completado el 2026-11-04.
  1. **Inicialización y Arquitectura:** Creado repositorio local `C:\dev\montaje` con Git, Node.js 20+ ESM nativo (`"type": "module"`), sin frameworks ni dependencias de runtime superfluas. Licencia PolyForm Noncommercial 1.0.0 y enlaces a la bóveda en `AGENTS.md`, `GEMINI.md`, `CLAUDE.md`.
  2. **Pipeline de Módulos Puros (`src/core/`):**
     - `audio.js`: extracción de audio a WAV PCM 16 kHz mono y extracción de metadatos técnicos con FFmpeg/FFprobe.
     - `transcribe.js`: invocación de `whisper-cli.exe` con modelo `large-v3-turbo`, `--dtw`, VAD y prompt táctico; con reintento automático por CPU (`-ng`) si la GPU falla.
     - `words.js`: extractor de tokens de Whisper a palabras con marcas temporales monótonas y puntuación adherida. Algoritmo de corrección difusa por distancia de Levenshtein normalizada (≤ 0.25) y clave fonética simplificada en español (*v/b*, *c/k/qu*, *z/s*, *w/gu*, *h* muda). Corrección validada para «combat guarrior» → «CombatWarrior», «taktikal barbell» y «tactical barbel» → «Tactical Barbell», sin tocar palabras comunes. Puntuación de confianza (`conf`) preservada por palabra.
     - `segment.js`: troceo dinámico en bloques (máx. 3 palabras en 9:16 y 7 en 16:9; corte por pausas > 300 ms o signos `.?!,;:` y duración mínima de 600 ms sin solapes).
     - `export-srt.js`: exportación formal en formato SubRip (`00:00:01,234 --> ...`).
     - `export-ass.js`: generador de subtítulos `.ass` estilo CapCut. Genera exactamente un evento `Dialogue` por intervalo de palabra activa, aplicando el efecto pop `\fscx115\fscy115\t(0,120,\fscx100\fscy100)` con el color de marca oro táctico (`#FFD400`, `&H0000D4FF&`). `PlayResX/Y` escalado a la resolución nativa de exportación (2160×3840 en 4K). En 9:16 el texto queda centrado al ~65 % de la altura, fuera de las zonas de botones de TikTok/Reels.
     - `project.js`: exportador y lector de proyectos `.montaje.json` (versión 1).
     - `render.js`: pipeline de renderizado con escalado Lanczos de alta fidelidad, recorte centrado 16:9 a 9:16 sin barras negras, quemado de subtítulos con `libass` a resolución 4K nativa y aceleración por GPU AMD AMF (`h264_amf` con QVBR/VBR a 60–80 Mbps). Barra de progreso en consola mediante tubería.
  3. **Estilos, Presets y Glosario:**
     - `styles/cw-impacto.json` con tipografía Anton (OFL descargada en `fonts/Anton-Regular.ttf`), borde negro grueso y sombra suave.
     - `presets/tiktok-4k.json` (2160×3840 vertical), `presets/yt-4k.json` (3840×2160 horizontal) y `presets/borrador.json` (1080p).
     - `glosario.json` con vocabulario táctico de CombatWarrior.
  4. **Entorno y Scripts:** `scripts/setup.ps1` para comprobación y descarga automática de binarios y modelos.
  5. **Suite de Tests:** 16 pruebas unitarias implementadas con `node:test` (`tests/*.test.js`), cubriendo Levenshtein, fonética española, parser de tokens, tiempos monótonos, segmentación, formatos SRT/ASS y construcción de argumentos de renderizado. 16/16 pruebas superadas en verde (274 ms).
  6. **Estado de Clip de Muestra:** `muestras/prueba.mp4` no existe actualmente en el disco; queda documentado en Backlog y Resumen a la espera de que el usuario coloque un clip real para calibración en vivo.
  7. **Commit:** Commit local `cbc293c` en `C:\dev\montaje`.

##### T-20261104-15 — Cerebro como app: un solo arranque
- **Proyecto:** cerebro
- **Resultado:** Completado el 2026-11-04.
  1. **Supervisor de subprocesos (`supervisor.js`):** implementada clase `ProcessSupervisor` integrada en `server.js`. Arranca el núcleo de voz local Python (`C:\dev\cerebro-voz\main.py --server`), redirigiendo logs a `logs/voz.log`. Health check cada 10s con auto-reinicio (hasta 5 intentos en 10 min con backoff exponencial). Monitoriza también Ollama en `http://127.0.0.1:11434` (levantando `ollama serve` si está disponible). En apagado ejecuta `taskkill /T /F` contra todos los PIDs hijos.
  2. **Modo servidor de voz:** añadido flag `--server` a `main.py` en `C:\dev\cerebro-voz` para levantar exclusivamente HTTP en `127.0.0.1:3001` sin atajos globales. Control de bloqueo de archivos en `FileHandler` para permitir concurrencia CLI/supervisor.
  3. **Lanzador silencioso (`Cerebro.vbs`):** script VBScript en la raíz de `cerebro-dashboard`. Verifica si el puerto 3000 ya responde; si no, lanza Node en segundo plano oculto (`vbHide`), espera hasta 30s a `/api/salud` y abre la app en modo ventana nativa con Edge (`msedge --app=http://127.0.0.1:3000`) o Chrome.
  4. **Accesos directos:** generados iconos `cerebro.ico` y `public/favicon.ico` con la paleta sináptica del orbe. Creados accesos directos `Cerebro.lnk` en el Escritorio del usuario y en el Menú Inicio (`AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Cerebro.lnk`).
  5. **Apagado limpio:** implementado endpoint `POST /api/apagar` en `server.js`, comando `/apagar` en la consola HUD y atajo de teclado global `Ctrl+Q` con confirmación, que detiene el árbol de procesos hijos (Python/Ollama) y cierra el servidor Node.
  6. **Documentación:** actualizado `README.md` con la sección «Doble clic en Cerebro y listo», ciclo de vida, resolución de problemas y logs. Añadida opción `arranque_con_windows: false` en `config.js`. Smoke test REST (11/11) superado. Commit local `a539281` en `cerebro-dashboard`.

##### T-20261104-14 — Ajustes del HUD v3: tamaño de la esfera y sin texto hablado
- **Proyecto:** cerebro
- **Resultado:** Completado el 2026-11-04.
  1. Tamaño y centrado exacto de la esfera calculado a partir del hueco real entre la línea del día (`#dia`) y el indicador de estado (`#estado`): radio máximo deformado = 40 % de la altura del hueco y 30 % del ancho. La esfera y sus partículas quedan 100 % centradas y contenidas en el marco sin desbordar. Recálculo automático en cada resize.
  2. Transcripción hablada eliminada de la vista visible y contenida en contenedor con `aria-live="polite"` (`#subtitulos-live`). Añadida opción `subtitulos: false` en `config` (activable mediante `localStorage` o clase `.con-subtitulos`). Debajo de la esfera queda únicamente el estado (`#estado`).
  3. Estado de la voz: al hacer clic en la esfera con el servicio 3001 caído, el estado muestra inmediatamente «Voz no disponible: arranque el núcleo de voz» en color de alerta en lugar de intentar capturar micrófono.
  4. Verificado y capturado en 1366×768, 1920×1080 y 390×844: capturas adjuntadas en `03_Proyectos/10_Cerebro/capturas/`.

##### T-20261104-13 — HUD v3: nuevo layout con la esfera actual
- **Proyecto:** cerebro
- **Resultado:** Completado el 2026-11-04. Implementado el layout de HUD v3 según `HUD_v3_prototipo.html` y la Corrección final:
  1. Esfera Three.js conservada y mejorada: posicionada en la parte superior, deformación orgánica por ruido a lo largo de la normal (3% reposo, hasta 15% con voz), cámara con margen de seguridad sin recortes, partículas orbitales interactivas ligadas a tareas de la cola con tooltip.
  2. Marco de carta con paleta matizada oficial (`--terreno`, `--curva`, `--hueso`, `--senal`, `--violeta`, `--alerta`).
  3. Línea del día 24 h en la cabecera alimentada con las horas de las entradas del registro de hoy.
  4. Conversación protagonista en el centro con aparición sincronizada palabra por palabra (`.w.on`).
  5. Márgenes laterales alimentados por datos reales de endpoints: `/api/estado` (prioridades, evaluación), `/api/cola` (tareas pendientes), `/api/proyectos` (proyecto activo), `/api/salud` (estado de voz y bóveda).
  6. Entrada de texto oculta tras «/» que envía a `/api/voz/turno` y reproduce la respuesta hablada; eliminados terminal inferior y botones obsoletos.
  7. Tipografía Archivo variable local (woff2) y Three.js local, sin dependencias CDN externas.
  8. Suite `test-api.js` ampliada a 11 pruebas: 11/11 pasadas con 100% de éxito.

##### T-20261103-09 — HUD v2 según especificación de diseño
- **Proyecto:** cerebro
- **Resultado:** Sustituida por T-13 (HUD v3).

##### T-20261103-01 — Reglas de memoria (lecciones JARVIS)
- **Proyecto:** cerebro
- **Orden:**
  1. En `00_Sistema_IA/06_Enrutado_IAs.md`, al final de "Reglas para toda IA que lea esto", añade: `7. Fallback: si dudas a qué herramienta derivar, o una derivación falla, hazlo tú con el modelo actual. Nunca dejes al usuario sin respuesta.`
  2. En `00_Sistema_IA/01_Instrucciones_Generales.md`, al final de la sección "Protocolo de traspaso entre IAs", añade: `**Higiene de memoria:** en CEREBRO solo se escriben resultados verificados. Intentos fallidos, mensajes de error y salidas de herramientas no se copian; se resumen en una línea ("Bloqueado: motivo").`
  3. Justo debajo, añade: `**Rotación del registro:** cuando 02_Registro_Actividad_IAs.md supere 20 entradas, Antigravity (flash) mueve sin modificarlas las entradas de meses anteriores a 00_Sistema_IA/Registro_Archivo/AAAA-MM.md y deja en el registro solo el mes en curso. Las IAs leen el archivo solo si lo necesitan.`
- **Criterio de hecho:** los tres textos están presentes literalmente; ningún otro contenido modificado.
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Añadida la regla 7 de fallback en `00_Sistema_IA/06_Enrutado_IAs.md`, y añadidas las cláusulas de "Higiene de memoria" y "Rotación del registro" en `00_Sistema_IA/01_Instrucciones_Generales.md`.

##### T-20261103-02 — Contrato de verificación para notas generadas por IA
- **Proyecto:** cerebro
- **Orden:**
  1. En `00_Sistema_IA/04_Esquema_YAML.md` añade al final la sección `## Notas generadas por IA` con: claves obligatorias adicionales `generado_por` (claude | antigravity | gemini | notebooklm), `verificado: false` y `fuente: ""` (ruta, URL o "conocimiento del modelo"). Regla: fechas, cifras y datos que no salgan de una fuente citada van en una sección final `## Por comprobar`. Solo el usuario cambia `verificado` a `true`.
  2. En `AGENTS.md`, en la lista de reglas finales, añade: `Toda nota que generes cumple la sección "Notas generadas por IA" de 00_Sistema_IA/04_Esquema_YAML.md.`
  3. Al final de `00_Sistema_IA/00_Dashboard.md` añade:
     ## 🔍 Pendiente de verificar
     ```dataview
     LIST generado_por
     FROM ""
     WHERE verificado = false
     SORT file.mtime DESC
     ```
- **Criterio de hecho:** las tres secciones existen; la consulta del dashboard se renderiza sin error en Obsidian.
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Añadida la sección "Notas generadas por IA" en `00_Sistema_IA/04_Esquema_YAML.md`, regla añadida en `AGENTS.md` y bloque Dataview "🔍 Pendiente de verificar" añadido en `00_Sistema_IA/00_Dashboard.md`.

##### T-20261103-03 — Rutina de mantenimiento semanal
- **Proyecto:** cerebro
- **Orden:**
  1. Crea `00_Sistema_IA/Prompts/Mantenimiento_Semanal.md` (frontmatter: tipo "core_prompt", area "sistema", fecha real, estado "activo", tags ["sistema", "mantenimiento"]) con la rutina de 7 pasos.
  2. Añade al final de `AGENTS.md`: `## Mantenimiento` + `- Si el usuario dice "ejecuta mantenimiento": sigue 00_Sistema_IA/Prompts/Mantenimiento_Semanal.md.`
  3. Ejecuta la rutina una vez como prueba.
- **Criterio de hecho:** existe el prompt, `AGENTS.md` tiene la sección y existe la primera nota en `Revisiones/` (debe incluir `03_Proyectos/10_Cerebro` en el índice).
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Creado `00_Sistema_IA/Prompts/Mantenimiento_Semanal.md`, añadida la sección a `AGENTS.md`, actualizado `00_Sistema_IA/03_Indice_General.md` con enlaces a proyectos 10 y 11, y generada la primera revisión `00_Sistema_IA/Revisiones/2026-W45.md`.

##### T-20261103-04 — Plantillas automáticas por carpeta (Templater)
- **Proyecto:** cerebro
- **Orden:**
  1. Con Obsidian cerrado, edita `.obsidian/plugins/templater-obsidian/data.json` (haz copia `data.json.bak` antes): `templates_folder` = "00_Sistema_IA/Plantillas", `trigger_on_file_creation` = true, `enable_folder_templates` = true y `folder_templates` configurado para las 5 carpetas base.
  2. Conserva el resto de claves. Valida el JSON.
- **Criterio de hecho:** JSON válido, copia `.bak` creada, prueba superada.
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Backup `data.json.bak` creado, `data.json` editado con las 5 asignaciones de plantillas de carpeta automáticas y JSON validado formalmente con Node.js.

##### T-20261103-06 — Bandeja de entrada por voz (Inbox)
- **Proyecto:** cerebro
- **Orden:**
  1. Crea `00_Sistema_IA/00_Inbox.md` (frontmatter: tipo "indice", area "sistema", fecha real, estado "activo", tags ["sistema", "inbox"]).
  2. Crea `00_Sistema_IA/Prompts/Procesar_Inbox.md` (frontmatter tipo "core_prompt", area "sistema") con la rutina de archivo y clasificación.
  3. Añade al final de `AGENTS.md`: `## Inbox` + `- Si el usuario dice "procesa inbox": sigue 00_Sistema_IA/Prompts/Procesar_Inbox.md.`
  4. Añade a `00_Sistema_IA/Prompts/Mantenimiento_Semanal.md` un paso 0: "Procesa el inbox (Prompts/Procesar_Inbox.md)".
- **Criterio de hecho:** existen las dos notas, `AGENTS.md` tiene la sección y una prueba con 3 líneas de ejemplo se archiva correctamente.
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Creado `00_Sistema_IA/00_Inbox.md`, creado `00_Sistema_IA/Prompts/Procesar_Inbox.md`, actualizada la regla en `AGENTS.md` y añadido el Paso 0 en `00_Sistema_IA/Prompts/Mantenimiento_Semanal.md`.

##### T-20261103-07 — Cerebro Voz, fase 1 (núcleo local)
- **Proyecto:** cerebro_voz
- **Orden:** lee `03_Proyectos/11_Cerebro_Voz/00_Resumen.md` y `Decisiones.md`. Implementa en `C:\dev\cerebro-voz` (git init; `.gitignore` con `.venv/`, `models/`, `logs/`, `*.wav`).
- **Criterio de hecho:** `pytest` en verde; con el atajo, «anota prueba de voz» añade la línea al inbox y «estado» lee `00_Estado_Actual` en voz alta; existen las 3 muestras de voz; commit local hecho (sin push).
- **Modelo sugerido:** pro
- **Resultado:** Completado el 2026-11-03. Inicializado `C:\dev\cerebro-voz` con Python 3.13 en venv, faster-whisper (small) y Piper TTS (es_ES-davefx-medium) en local. Implementados `audio_fx.py` (WSOLA + reverb sintético), `router.py`, `audio_capture.py`, `stt.py`, `tts.py`, `main.py` y `config.toml`. Suite pytest en verde (3/3 pasando: aislamiento sin red, normalización y 13 casos de enrutado). Generadas 3 muestras de voz en `muestras/`. Pruebas en caliente de "anota" y "estado" validadas contra la bóveda. Commit local realizado (`b835f62`).

##### T-20261103-10 — Identidad de Cerebro en el router de voz
- **Proyecto:** cerebro_voz
- **Orden:** implementada en `C:\dev\cerebro-voz`: `identidad.py` con carga dinámica y recarga por mtime de `00_Sistema_IA/07_Identidad_Cerebro.md`, evaluación previa de cortesía e identidad en `router.py`, saludo al arrancar en `main.py` con impresión de consola, y suite de tests completa verificando tratamiento de respeto formal (usted/señor) y alternancia de respuestas.
- **Criterio de hecho:** al arrancar se oye el saludo; con el atajo, «hola» responde con la identidad y saludo temporal de Cerebro; tests en verde (5/5).
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-04. Creado `identidad.py` con soporte para `{saludo}`, `{n}`, `{resumen_salud}`, `{componente}` y selección sin repetición inmediata. `router.py` prioriza reglas de identidad (saludo, identidad, agradecimiento, despedida, estado propio) y fallback formal. Saludo en arranque implementado en `main.py` con mensaje «Cerebro escuchando. Pulse Ctrl+Alt+C para hablar.». Tests pytest actualizados (5/5 pasando). Commit local en repo `C:\dev\cerebro-voz` (`f72a520`).

##### T-20261103-08 — Modo conversación en la interfaz CEREBRO // CORE (127.0.0.1:3000)
- **Proyecto:** cerebro_voz
- **Orden:** implementado en `C:\dev\cerebro-voz` servicio HTTP `server.py` en `127.0.0.1:3001` con precarga de modelos en arranque, endpoints `GET /voz/estado` y `POST /voz/turno`, memoria RAM de últimos 10 turnos y suite pytest (6/6). En `C:\dev\cerebro-dashboard`: corregido comando `ping` sin `undefined` leyendo métricas de `os` y proceso; implementada clase `ConversationManager` con captura `MediaRecorder` nativa y análisis Web Audio (`AnalyserNode`), umbral de silencio a 1,2s y timeout de inactividad a 30s sin llamadas externas; orbe 3D reactivo a 5 estados (`reposo`, `escuchando`, `pensando`, `hablando`, `desconectado`) con deformación procedural y pulso de amplitud; bucle conversacional continuo y salida con clic, Espacio, o palabras clave («fin», «salir», «gracias Cerebro»); endpoints proxy `/api/voz/*`; suite de smoke tests actualizada con 6/6 tests en verde (`test-api.js`); documentación cruzada (`README.md`, `CLAUDE.md`, `AGENTS.md`, `GEMINI.md`).
- **Criterio de hecho:** `ping` sin `undefined`; clic en la esfera → «estado» hablado → Cerebro responde con voz y la esfera reacciona en los 4 estados; «fin» sale del modo; ninguna petición de red sale de `127.0.0.1` (comprobado en la pestaña Red del navegador).
- **Modelo sugerido:** pro
- **Resultado:** Completado el 2026-11-04. Implementación integral probada en caliente de ambos procesos (Node.js en 3000 y Python en 3001). Smoke test 6/6 verde. Telemetría de hardware verificada sin `undefined`. Proxy de voz operativo con retorno de WAV sintético base64 y estados lumínicos en el núcleo WebGL. Repositorios locales de `cerebro-voz` (commit `3a3bb0b`) y `cerebro-dashboard` (commit `7243f32`) sincronizados y documentados.
