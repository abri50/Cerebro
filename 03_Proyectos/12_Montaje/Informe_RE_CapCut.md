---
tipo: "apuntes"
area: "desarrollo"
proyecto: "montaje"
fecha: 2026-11-03
estado: "activo"
tags: ["codigo", "montaje", "ingenieria_inversa"]
generado_por: claude
verificado: false
fuente: "Análisis estático con REA 6.8.0 de C:\\Users\\aam12\\AppData\\Local\\CapCut\\Apps\\9.5.0.4050"
---

# Informe de ingeniería inversa — CapCut 9.5.0.4050 (Windows)

Alcance: inventario de la instalación, tablas de importación/exportación PE y cadenas de componentes clave. Sin descompilar ni ejecutar nada. Solo se usa para orientar el diseño de [[00_Resumen|Montaje]]; no se copia código.

## Observado
| Componente | Hallazgo | Evidencia REA |
|---|---|---|
| `speechsdk.dll` | Motor de voz propio («petrel»/«panther»): **RNN-T** con beam search, codificador en streaming y no causal, VAD, `TimestampPostProcessor`, `CaptionPostProcessActor`, `BoostingConfig` y `DeepBiasConfig` (refuerzo de palabras clave), LM neuronal (`NnlmConfig`) | exports `ev_2dbc44d0…`, imports `ev_2fe90ec7…` |
| `speechsdk.dll` | Importa solo KERNEL32, RPCRT4, VCOMP140 (OpenMP), WINMM y dbghelp: **la DLL no abre red por sí misma** | `ev_2fe90ec7…` |
| `Resources/models` | Modelos de vídeo, matting, caras, audio; **no hay ningún modelo de ASR completo** en la instalación (solo índices `media_search/asr`) | listado de carpeta |
| `avcodec-61.dll` | FFmpeg 7.x (Lavc 61.3.100) compilado con AMF, NVENC, QSV (libmfx), MediaFoundation y escalado D3D11. Codificadores: `h264/hevc/av1_amf`, `h264/hevc_nvenc`, `h264/hevc/av1_qsv`, `h264/hevc_mf`. **Sin libx264 ni libx265** | cadenas de la build |
| `codec_extend.dll` | Exporta solo `createEncoder` y `setCodecLogCallback`; enlaza avcodec/avutil: envoltorio de codificador propio | `ev_9ce4e2e5…`, `ev_01172c19…` |
| `models/v*-models/{h264,hevc}_{720,1080}` | Modelos `smartcodec_v1.nnet` + estadísticas: control de tasa adaptado al contenido, solo para 720p y 1080p | listado + `statics` |
| `video_template_ratio.json` | 9:16 = 0,5625 entre los formatos de serie | archivo |
| `ffmpeg.exe` | Enlaza los avcodec/avformat/avfilter del paquete y `libvecrptor.dll` | `ev_74edc594…` |

## Inferido (no probado)
- Los subtítulos automáticos usan ASR RNN-T con **sesgo de vocabulario por palabras clave** (hotword boosting) y un posproceso propio que trocea en bloques de subtítulo. Por eso acierta nombres propios mejor que Whisper con un simple prompt.
- La exportación se apoya en **codificación por GPU** (AMF en AMD). Sin x264, no hay codificación por software de alta calidad.
- El control de tasa «inteligente» solo cubre hasta 1080p; en 4K probablemente usa los parámetros por defecto del codificador por GPU.

## Desconocido
- Si la transcripción va en local (modelo descargado aparte, quizá en `User Data`) o en la nube. No se ha inspeccionado `User Data` ni el tráfico de red.
- Resolución, bitrate y códec exactos de un export «TikTok 4K»: no había vídeos exportados en `CapCut\Videos`.

## Implicaciones para Montaje
1. Whisper + `--prompt` se queda corto frente al refuerzo por palabras clave → añadir **corrección difusa con el glosario** (distancia de edición + fonética española) y marcar en el editor las palabras de baja confianza (D07).
2. AMF como codificador principal confirmado (mismo camino que CapCut). La RX 6900 XT (RDNA2) codifica H.264 y HEVC, **no AV1**: no ofrecer `av1_amf` en ese equipo.
3. Control de tasa: usar el modo de calidad constante de AMF (QVBR) en vez de un bitrate fijo, para aproximar el ajuste por contenido.

## Por comprobar
- Medir con `ffprobe` un vídeo exportado por CapCut en 4K para TikTok y fijar con eso el preset `tiktok-4k`.
- Que el modo QVBR esté disponible en el `h264_amf`/`hevc_amf` del FFmpeg que use Montaje.
