---
tipo: "proyecto"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "cerebro_voz"
siguiente_accion: "Antigravity: ejecutar T-20261103-08 (modo conversación en HUD)"
prioridad: 2
tags: ["codigo", "proyecto", "voz"]
generado_por: "claude"
verificado: false
fuente: "Sesión Claude 2026-11-03"
---
# Cerebro Voz

## Qué es
Asistente de voz propio llamado «Cerebro», con voz original (no clonada de nadie), que lee y escribe en CEREBRO. Sin Siri.

## Arquitectura
```
Activación ("Cerebro" / atajo de teclado) → STT local (faster-whisper)
→ Router por reglas (0 tokens) ── orden conocida → acción sobre la bóveda
                               └─ resto → [fase 2] LLM con contexto mínimo
→ TTS local (Piper + efecto sintético) → respuesta hablada
```

## Stack
- Python 3.11+, código en `C:\dev\cerebro-voz` (fuera de la bóveda).
- STT: faster-whisper `small` int8 en CPU, idioma `es`.
- TTS: Piper (voz española masculina) + efecto (tono más grave, leve modulación/reverb) = voz propia de Cerebro.
- Activación: atajo de teclado global (fase 1) → palabra «Cerebro» con openWakeWord entrenado a medida (fase 1b).
- Escribe directamente en los `.md` de la bóveda (no necesita Obsidian abierto); Git recoge los cambios.

## Fases
1. Sin LLM, sin red: anota, estado, siguiente acción de un proyecto, tareas en cola, registrar entrenamiento → inbox.
2. LLM: API de Gemini **de pago** (modelo Flash), clave fuera de la bóveda, límite de gasto mensual en Google Cloud. Contexto: `00_Estado_Actual` + `00_Resumen` del proyecto citado. Respuestas habladas de 3 frases como máximo; el trabajo pesado se deriva a la cola.
3. Home server + PWA con micrófono vía Tailscale para usarlo desde el iPhone.

Ver [[Backlog]] y [[Decisiones]].
