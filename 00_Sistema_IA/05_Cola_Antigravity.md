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

##### T-20261103-07 — Cerebro Voz, fase 1 (núcleo local)
- **Proyecto:** cerebro_voz
- **Orden:** lee `03_Proyectos/11_Cerebro_Voz/00_Resumen.md` y `Decisiones.md`. Implementa en `C:\dev\cerebro-voz` (git init; `.gitignore` con `.venv/`, `models/`, `logs/`, `*.wav`):
  1. Entorno: Python 3.11+ con venv; dependencias `faster-whisper`, `sounddevice`, `numpy`, `keyboard` (o `pynput`), `piper-tts`, `pyyaml`, `pytest`. Descarga el modelo Whisper `small` y una voz Piper española masculina en `models/`.
  2. `config.toml`: `vault_path = "C:\\Users\\aam12\\Documents\\CEREBRO"`, `hotkey = "ctrl+alt+c"`, parámetros de voz (`pitch_semitones`, `speed`, `effect`).
  3. Bucle: atajo pulsado → graba hasta 1,2 s de silencio (máx. 20 s) → transcribe en `es` → `router.py` → acción → respuesta con TTS. Un solo mensaje a la vez.
  4. `router.py` con reglas por regex sobre el texto normalizado (minúsculas, sin tildes):
     - `^(anota|apunta|guarda) (.+)` → añade `- AAAA-MM-DD HH:MM — <texto>` bajo `## Entradas` de `00_Sistema_IA/00_Inbox.md`. Responde «Anotado».
     - `^registra (.+)` → igual que anota (lo archiva "procesa inbox"). Responde «Registrado en la bandeja».
     - `(estado|que toca|informe)` → lee `00_Sistema_IA/00_Estado_Actual.md`, quita frontmatter, marcas Markdown y callouts, y lo lee (máx. 60 s de audio).
     - `(siguiente|donde lo dejamos).*(de|con|en) (\w+)` → busca en `03_Proyectos/*/00_Resumen.md` el `proyecto` que coincida (aproximado) y lee su `siguiente_accion`.
     - `(cola|tareas pendientes)` → cuenta las `###` bajo `## Pendientes` de `05_Cola_Antigravity.md` y lee sus títulos.
     - Sin coincidencia → «Esa orden aún no la conozco; la dejo en la bandeja» y la anota con prefijo `¿?`.
  5. Voz: Piper → posprocesado con numpy (tono más grave según `pitch_semitones`, leve reverb). Genera `muestras/variante_{1,2,3}.wav` con 3 ajustes distintos de la frase «Cerebro operativo. Todo en orden.» para que el usuario elija.
  6. Escritura segura en la bóveda: añadir con apertura en modo append, UTF-8, sin reescribir archivos; si `00_Inbox.md` no existe, avisa por voz y no lo crees.
  7. Fase 1 sin red: añade un test que falle si el código importa `requests`, `httpx` o `urllib.request`.
  8. Tests `pytest` del router con al menos 10 frases (incluidas con tildes y mayúsculas).
  9. `README.md`: instalación, uso, atajo, cómo cambiar la voz.
  10. Crea en el repo `AGENTS.md`, `GEMINI.md` y `CLAUDE.md` enlazados a `CEREBRO/03_Proyectos/11_Cerebro_Voz/` según el protocolo de traspaso.
  11. Actualiza `Backlog.md` y `siguiente_accion` del proyecto y registra la actividad.
- **Criterio de hecho:** `pytest` en verde; con el atajo, «anota prueba de voz» añade la línea al inbox y «estado» lee `00_Estado_Actual` en voz alta; existen las 3 muestras de voz; commit local hecho (sin push).
- **Modelo sugerido:** pro

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
