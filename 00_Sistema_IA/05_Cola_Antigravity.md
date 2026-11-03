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

##### T-20261103-08 — Modo conversación en la interfaz CEREBRO // CORE (127.0.0.1:3000)
- **Proyecto:** cerebro_voz
- **Depende de:** T-20261103-07. **Ampliación de T-07:** además del atajo de teclado, el núcleo Python expone un servicio HTTP solo en `127.0.0.1:3001`: `POST /voz/turno` (audio webm/wav → `{texto_usuario, respuesta, accion}` + audio de respuesta en wav), `GET /voz/estado`. Misma lógica del router; sin red externa.
- **Orden:**
  1. Localiza el proyecto de la interfaz que sirve `127.0.0.1:3000` (probablemente `C:\dev\cerebro-dashboard`). Si no está bajo Git, haz `git init` y commit del estado actual antes de tocar nada.
  2. Corrige el comando `ping`: hoy muestra `undefined` en Host, SO, memoria, CPUs y uptime. Haz que el endpoint devuelva y el front lea los campos de `os.hostname()`, `os.platform()`, `os.release()`, `os.freemem()`, `os.totalmem()`, `os.cpus().length`, `os.uptime()` y `process.uptime()`.
  3. Clic en la esfera → entra o sale del **modo conversación** (también con la tecla Espacio y con el comando `voz`).
  4. Captura del micrófono en el navegador con `MediaRecorder` + detección de silencio con Web Audio (`AnalyserNode`: el turno termina tras 1,2 s por debajo del umbral). **No uses la Web Speech API del navegador** (envía el audio a servidores externos). Cada turno → `POST http://127.0.0.1:3001/voz/turno` (proxy desde el servidor Node para evitar CORS).
  5. Estados visuales de la esfera: `reposo` (giro lento) → `escuchando` (pulsa con la amplitud de tu voz) → `pensando` (rotación rápida, color más frío) → `hablando` (se deforma con la amplitud del audio de respuesta, vía `AnalyserNode` sobre la reproducción). El texto central muestra el estado y el terminal recoge cada turno como `TÚ:` / `CEREBRO:`.
  6. Bucle de conversación: tras hablar Cerebro, vuelve a escuchar automáticamente. Sale con clic, con Espacio o al decir «fin», «salir» o «gracias Cerebro». Tiempo máximo de inactividad: 30 s.
  7. Memoria de la conversación: solo en el servidor y en RAM (últimos 10 turnos). No se escribe nada en la bóveda salvo las órdenes explícitas (anota/registra). Al salir del modo, si hubo alguna orden ejecutada, añade una sola entrada al registro de actividad (`Cerebro Voz`) con el resumen.
  8. Si el servicio de voz (3001) no responde: la esfera pasa a estado `desconectado` y el terminal lo indica; la interfaz sigue funcionando.
  9. Crea en el repo de la interfaz `AGENTS.md`, `GEMINI.md` y `CLAUDE.md` enlazados a `CEREBRO/03_Proyectos/11_Cerebro_Voz/`. Documenta en el README cómo arrancar los dos procesos (3000 y 3001).
  10. Actualiza `Backlog.md`, `siguiente_accion` y el registro.
- **Criterio de hecho:** `ping` sin `undefined`; clic en la esfera → «estado» hablado → Cerebro responde con voz y la esfera reacciona en los 4 estados; «fin» sale del modo; ninguna petición de red sale de `127.0.0.1` (comprobado en la pestaña Red del navegador).
- **Modelo sugerido:** pro

##### T-20261103-09 — HUD v2 según especificación de diseño
- **Proyecto:** cerebro
- **Depende de:** T-20261103-08.
- **Orden:** implementa en la interfaz `127.0.0.1:3000` la especificación completa de `03_Proyectos/10_Cerebro/HUD_Diseno.md` (layout de 3 columnas, sistema visual, núcleo con shader y estados, partículas = tareas pendientes, color = salud global, endpoints `/api/estado`, `/api/cola`, `/api/registro`, `/api/proyectos`, `/api/salud` con SSE, movimiento y `prefers-reduced-motion`). Elimina cualquier métrica sin fuente real. Fuentes y Three.js en copia local. Commit por cada bloque (layout, visual, núcleo, datos). Sin push.
- **Criterio de hecho:** cada número visible sale de un endpoint; la esfera cambia de color al detener el servicio de voz; las partículas coinciden con las tareas de la cola; 60 fps estables con la pestaña visible; con `prefers-reduced-motion` no hay animación. Captura de pantalla adjunta en el registro.
- **Modelo sugerido:** pro

##### T-20261103-11 — Cerebro Voz, fase 2: conversación libre (LLM)
- **Proyecto:** cerebro_voz
- **Depende de:** T-07, T-08, T-10. **BLOQUEADA** hasta que el usuario confirme que la variable de entorno `GEMINI_API_KEY` existe (clave del nivel de pago).
- **Orden:**
  1. `llm.py` con el SDK oficial `google-genai`. Modelo configurable en `config.toml` (`llm_model`, por defecto el Gemini Flash vigente; consulta el nombre actual en la documentación oficial, no lo inventes). La clave solo desde la variable de entorno; nunca en archivos ni en la bóveda.
  2. *System prompt* = contenido de `00_Sistema_IA/07_Identidad_Cerebro.md` + «Responde en español, de usted, en un máximo de 3 frases salvo que se pida detalle. No inventes datos: si no está en el contexto o en una herramienta, dilo».
  3. Contexto por turno: `00_Estado_Actual.md` (sin frontmatter) + el `00_Resumen.md` del proyecto si el usuario nombra uno + los últimos 10 turnos (en RAM).
  4. Herramientas (*function calling*): `leer_nota(ruta)` (solo dentro de la bóveda, excluye `.obsidian`), `buscar_proyecto(nombre)`, `anotar(texto)` → bandeja, `tareas_cola()`, `proponer_tarea(titulo, orden, criterio)` → **pide confirmación por voz** («¿La añado a la cola, señor?») y solo escribe tras un «sí».
  5. Router: reglas primero (fase 1 + identidad); si nada encaja → LLM. Si falta la clave, se agota el límite diario o hay un error de red → respuesta de fallback de la identidad y sigue funcionando por reglas (nunca un callejón sin salida; el error no entra en la memoria de turnos).
  6. Streaming: divide la respuesta en frases y manda cada frase a Piper en cuanto llega, para que empiece a hablar antes de terminar.
  7. Chat por texto: en el terminal del HUD, cualquier texto que no sea un comando del HUD va al mismo `POST /voz/turno` (versión texto) y la respuesta aparece y se oye.
  8. Límites: `max_llm_llamadas_dia` en la configuración (por defecto 200); contador diario en `logs/uso_llm.json` expuesto en `/voz/estado` y en `/api/salud` del HUD (llamadas hoy / límite).
  9. Tests con el LLM simulado (*mock*): fallback sin clave, límite diario alcanzado, herramienta fuera de la bóveda rechazada, `proponer_tarea` no escribe sin confirmación.
  10. Actualiza `00_Resumen` (fase 2), Backlog, Decisiones y el registro.
- **Criterio de hecho:** «¿Qué me recomiendas estudiar hoy?» obtiene una respuesta coherente con `00_Estado_Actual`, con la voz de Cerebro y empezando a hablar en menos de 3 s; sin clave, Cerebro sigue respondiendo por reglas; tests en verde.
- **Modelo sugerido:** pro

- **Ampliación (2026-11-03, prevalece sobre lo anterior):** el LLM es **intercambiable** mediante `llm_provider` en `config.toml`: `ollama` (por defecto) o `gemini`.
  - `ollama`: API local `http://127.0.0.1:11434` (URL configurable para usar la GPU del PC desde el futuro servidor). Modelo configurable (`ollama_model`); prueba un modelo instruct de 7-14B cuantizado con buen español y deja en el README una tabla con latencia y calidad de 3 candidatos medidos con las mismas 10 preguntas.
  - `gemini`: como se describe arriba (clave de pago en variable de entorno).
  - Cascada: reglas → `ollama` → `gemini` (solo si hay clave y el usuario lo activa con `llm_fallback = "gemini"`) → fallback de la identidad.
  - Ya **no está bloqueada**: con Ollama se puede hacer sin clave. La parte de Gemini se prueba solo si `GEMINI_API_KEY` existe.
  - Paso previo del usuario: instalar Ollama para Windows y comprobar con `ollama ps` que el modelo se carga en la GPU (RX 6900 XT, 16 GB) y no en la CPU.

##### T-20261103-12 — Montaje F1: motor de subtítulos automáticos (CLI)
- **Proyecto:** montaje
- **Orden:** lee `03_Proyectos/12_Montaje/00_Resumen.md` y `Decisiones.md`. Implementa en `C:\dev\montaje` (git init; `.gitignore` con `node_modules/`, `models/`, `bin/`, `out/`, `muestras/`):
  1. Node.js 20+ ESM, sin frameworks. Dependencias permitidas: ninguna en runtime salvo un parser de argumentos mínimo; `node:test` para tests.
  2. Binarios en `bin/` (no versionados) con `scripts/setup.ps1` que los descargue: `whisper-cli.exe` de la última release oficial de `ggml-org/whisper.cpp` **con Vulkan**, `ffmpeg.exe`/`ffprobe.exe` (build con libass). Modelos en `models/`: `ggml-large-v3-turbo-q5_0.bin` y el VAD Silero (`ggml-silero-*.bin`) desde los repos oficiales. Comprueba los flags reales con `whisper-cli --help`; no los inventes.
  3. CLI: `node src/cli.js subs <video> [--estilo cw-impacto] [--formato auto|9:16|16:9] [--palabras 3] [--mayusculas] [--quemar] [--hw amf|cpu]`. Salida en `out/<nombre>/`: `<nombre>.montaje.json`, `.srt`, `.ass` y, con `--quemar`, `<nombre>_subs.mp4`.
  4. Pipeline en módulos puros (`src/core/`):
     - `audio.js`: FFmpeg → WAV 16 kHz mono.
     - `transcribe.js`: `whisper-cli -l es -ojf --dtw large.v3.turbo` + VAD + `--prompt` con los términos de `glosario.json` (clave `prompt`). Si la GPU falla, reintenta con `-ng` y avísalo.
     - `words.js`: tokens del JSON completo → palabras `{texto, ini_ms, fin_ms, conf}` (token con espacio inicial abre palabra; la puntuación se pega a la anterior; descarta tokens especiales `[_...]`); aplica `glosario.json` (clave `correcciones`, sustitución por palabra/frase, sin distinguir mayúsculas). Garantiza tiempos monótonos.
     - `segment.js`: agrupa en bloques: máx. `--palabras` (por defecto 3 en 9:16 y 7 en 16:9), máx. 2 líneas, corta en pausa > 300 ms o en `.?!,`; duración mínima 600 ms; sin solapes.
     - `export-srt.js`, `export-ass.js`, `project.js` (JSON propio, versión `1`).
  5. Estilo `cw-impacto` (`styles/cw-impacto.json`): fuente gruesa OFL incluida en `fonts/` (Montserrat Black o Anton), texto blanco, borde negro grueso, sombra suave; **palabra activa** con el color principal de la marca (extráelo de `C:\dev\combat-warrior-hub`, configuración de Tailwind/CSS; si no hay, `#FFD400`) y efecto pop `\fscx115\fscy115` → 100 % en 120 ms con `\t`. Un evento `Dialogue` por cada intervalo de palabra activa con el bloque completo. `PlayResX/Y` = resolución del vídeo (ffprobe); en 9:16 el texto centrado al ~65 % de la altura (fuera de la interfaz de Reels/TikTok); en 16:9, tercio inferior.
  6. Quemado: `ffmpeg -vf "ass=<ass>:fontsdir=fonts" -c:a copy`; `--hw amf` → `h264_amf`, si no `libx264 -crf 18 -preset veryfast`.
  7. `glosario.json` inicial: prompt «CombatWarrior, Tactical Barbell, Tactical Games, rucking, sandbag, kettlebell, Operator, Fighter, Base Building»; correcciones de ejemplo (`"combat warrior"→"CombatWarrior"`, `"tactical barbel"→"Tactical Barbell"`, `"raking"→"rucking"`).
  8. Tests `node:test` con fixtures JSON de whisper (sin ejecutar whisper): unión de tokens con acentos y puntuación, glosario, segmentación (límites, pausas, mín. 600 ms), formato de tiempo SRT `00:00:01,234` y ASS `0:00:01.23`, un evento ASS por palabra.
  9. `README.md` (setup, uso, estilos, glosario), `LICENSE` PolyForm Noncommercial 1.0.0 con «Copyright © 2026 Abraham Almagro Martínez» (el usuario puede cambiarla), y `AGENTS.md`, `GEMINI.md`, `CLAUDE.md` enlazados a `CEREBRO/03_Proyectos/12_Montaje/`.
  10. Si existe `muestras/prueba.mp4`, ejecuta `subs muestras/prueba.mp4 --quemar` y anota en el registro el tiempo de transcripción y si usó GPU. Si no existe, déjalo indicado.
  11. Actualiza `Backlog.md`, `siguiente_accion` y el registro. Commit local, sin push.
- **Criterio de hecho:** `node --test` en verde; con el clip de prueba se generan los 4 archivos, el `.mp4` muestra bloques de ≤3 palabras con la palabra activa resaltada y sincronizada (desfase visual < 150 ms), y «Tactical Barbell»/«CombatWarrior» salen bien escritos; `whisper-cli` informa de Vulkan como dispositivo.
- **Modelo sugerido:** pro

- **Ampliación (2026-11-03, prevalece sobre lo anterior): export 4K TikTok.** Lee `Decisiones.md` D06.
  - Nuevo comando `node src/cli.js render <video> [--subs <ass>] [--preset tiktok-4k|yt-4k|borrador] [--codec h264|hevc]` y `subs ... --quemar` usa por defecto `--preset tiktok-4k`.
  - `src/core/render.js` + `presets/*.json`. `tiktok-4k`: 2160×3840, fps de origen (máx. 60), `h264_amf` (`-quality quality -rc vbr_peak -b:v 60M -maxrate 80M`; comprueba los flags reales con `ffmpeg -h encoder=h264_amf`), `-pix_fmt yuv420p`, `-c:a aac -b:a 320k -ar 48000`, `-movflags +faststart`. `yt-4k`: 3840×2160. `borrador`: 1080p, `libx264 -preset veryfast -crf 23` para revisar rápido. Sin AMF disponible → `libx264 -preset slow -crf 16` y avísalo.
  - Origen 16:9 en preset vertical: escala + recorte centrado (`scale` con `force_original_aspect_ratio=increase`, `crop`), sin bandas negras.
  - Orden del filtro: `scale=...:flags=lanczos` → `crop` → `ass=...` (los subtítulos se rasterizan a 4K). El `.ass` se genera siempre con `PlayResX/Y` del preset de salida, no del vídeo de origen; tamaños de fuente, bordes y márgenes escalados en proporción.
  - Barra de progreso en consola leyendo `-progress pipe:1`.
  - Tests: cadena de filtros y argumentos generados para cada preset (sin ejecutar ffmpeg) y `PlayRes` = resolución del preset.
  - **Criterio de hecho añadido:** `ffprobe` del archivo final da 2160×3840, `yuv420p`, H.264 y audio AAC 48 kHz; los subtítulos se ven nítidos con zoom al 100 % sobre un fotograma 4K exportado con `ffmpeg -ss 5 -frames:v 1`.

## Hechas
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
