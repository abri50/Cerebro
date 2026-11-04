---
tipo: "decisiones"
area: "desarrollo"
proyecto: "montaje"
fecha: 2026-11-03
estado: "activo"
tags: ["codigo", "decisiones"]
generado_por: claude
verificado: false
fuente: "conocimiento del modelo"
---

# Decisiones — Montaje

## 2026-11-03 — D01 App propia inspirada en CapCut
- **Decisión:** diseño y código propios con las mejores funciones de CapCut como referencia; uso personal, sin comercializar.
- **Motivo:** el usuario quiere su herramienta, no un clon. Las funciones clave (STT, estilos de texto, export 4K) se resuelven con piezas libres (whisper.cpp, libass, FFmpeg).

## 2026-11-03 — D02 whisper.cpp en lugar de faster-whisper
- **Decisión:** `whisper-cli.exe` con Vulkan como proceso hijo.
- **Motivo:** la GPU es AMD (RX 6900 XT); faster-whisper (CTranslate2) solo acelera en CUDA y caería a CPU. whisper.cpp es un ejecutable sin Python, más fácil de empaquetar en Electron. MIT.

## 2026-11-03 — D03 Subtítulos en ASS quemados con libass
- **Decisión:** el estilo CapCut se genera como `.ass`: un evento por intervalo de palabra activa con la línea completa y la palabra activa con color y escala propios.
- **Motivo:** `\k` (karaoke) solo rellena color; el «pop» de CapCut necesita `\t` por palabra. ASS es portable, se previsualiza y FFmpeg lo quema sin código propio de render.

## 2026-11-03 — D04 Vocabulario propio por prompt + glosario
- **Decisión:** `--prompt` de Whisper con los términos de la marca y `glosario.json` de correcciones aplicado tras transcribir.
- **Motivo:** Whisper falla con nombres propios y anglicismos (Tactical Barbell, rucking, sandbag, CombatWarrior).

## 2026-11-03 — D05 Núcleo CLI antes que interfaz
- **Decisión:** F1 es un CLI Node con módulos puros; Electron llega en F2 y reutiliza el núcleo.
- **Motivo:** valor inmediato (subtitular reels ya) y núcleo testeable sin interfaz.

## 2026-11-03 — D06 Export 4K TikTok como preset nativo
- **Decisión:** preset `tiktok-4k`: 2160×3840, fps de origen (30 o 60), H.264 High por AMF (`h264_amf`) a ~60 Mbps (HEVC `hevc_amf` opcional), `yuv420p`, AAC 48 kHz 320 kb/s, `+faststart`. Origen menor de 4K → escalado Lanczos **antes** de quemar subtítulos; el `.ass` se genera con `PlayRes` 2160×3840.
- **Motivo:** el texto se rasteriza a 4K nativo (bordes nítidos, no escalados), y AMF aprovecha la GPU del usuario. H.264 por compatibilidad máxima en la subida; HEVC queda como opción.

## 2026-11-03 — D07 Glosario difuso y confianza por palabra
- **Decisión:** tras transcribir, cada palabra o n-grama se compara con el glosario por distancia de edición normalizada y por clave fonética española; si supera el umbral se sustituye. Se guarda `conf` por palabra y el editor de F2 resalta las de baja confianza.
- **Motivo:** CapCut usa refuerzo de palabras clave dentro del decodificador (ver [[Informe_RE_CapCut]]); con Whisper solo hay prompt. La corrección posterior compensa buena parte de esa diferencia sin modificar el modelo.

## 2026-11-03 — D08 Control de tasa QVBR en AMF; sin AV1
- **Decisión:** `tiktok-4k` usa QVBR de AMF (calidad constante con techo de bitrate) en vez de VBR con bitrate fijo. No se ofrece AV1 por GPU en la RX 6900 XT.
- **Motivo:** aproxima el control de tasa por contenido de CapCut; RDNA2 no codifica AV1.
