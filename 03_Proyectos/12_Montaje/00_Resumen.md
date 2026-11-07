---
tipo: "proyecto"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "montaje"
siguiente_accion: "Usuario: dejar un clip real con voz en C:\\dev\\montaje\\muestras\\prueba.mp4 para prueba de quemado y calibración fina. Siguiente desarrollo: F2 (Editor de subtítulos en Electron)."
prioridad: 2
stack: [electron, vanilla-js, ffmpeg, whisper-cpp]
tags: ["codigo", "proyecto", "combatwarrior", "video"]
generado_por: claude
verificado: false
fuente: "conocimiento del modelo; https://github.com/ggml-org/whisper.cpp"
---

# Montaje — editor de vídeo propio para CombatWarrior

## Qué es
App de escritorio propia para Windows, de **uso personal**, con lo mejor de CapCut para las piezas de [[01_CombatWarrior/00_Resumen|CombatWarrior]]: reels/TikTok 9:16 y vídeos 16:9. Prioridades:
1. **Subtítulos automáticos** estilo CapCut (palabra activa resaltada, 2-4 palabras por bloque, español, vocabulario propio).
2. **Exportación en 4K** para TikTok (2160×3840 vertical), con subtítulos nítidos a esa resolución.

## Enfoque
Diseño y código propios. CapCut solo es la referencia de qué funciones merece la pena tener; no se usa su código.

## Arquitectura
| Capa | Elección |
|---|---|
| Transcripción | `whisper-cli` de whisper.cpp (Vulkan → GPU RX 6900 XT), modelo `large-v3-turbo` cuantizado, `-l es`, VAD Silero, marcas por palabra (DTW) |
| Render / export | FFmpeg: escalado Lanczos, subtítulos quemados con libass a resolución nativa, codificación por GPU AMD (AMF) |
| Núcleo | Node.js (ESM), módulos puros y testeables: `transcribe` → `words` → `segment` → `export (json/srt/ass)` → `render` |
| Interfaz (F2+) | Electron + Vanilla JS/Tailwind, mismo patrón que Estrato |
| Proyecto | JSON propio (`.montaje.json`) |

## Fases
1. **F1 — Motor CLI** (Completada): vídeo → subtítulos (`.json`, `.srt`, `.ass` con pop CapCut) → render 4K TikTok (AMF / Lanczos).
2. **F2 — Editor de subtítulos**: vista previa, forma de onda, corregir palabras, retemporizar, presets de estilo.
3. **F3 — Línea de tiempo básica**: cortar, recortar, dividir, música con *ducking*, eliminar silencios automática.
4. **F4 — Extras**: auto-reencuadre 16:9 → 9:16, plantillas de marca (intro, logo, outro), LUT.

## Repositorio
- **Ruta local:** `C:\dev\montaje` (inicializado, 16 tests pasando en verde)
- **Remoto:** `abri50/montaje` (pendiente)
- **Licencia:** PolyForm Noncommercial 1.0.0 (uso personal).

## Por comprobar
- Nombre de la app («Montaje» es provisional).
- Límites actuales de subida de TikTok (resolución, fps, códec y peso máximos) antes de fijar el preset definitivo.
