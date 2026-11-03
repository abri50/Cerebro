---
tipo: "decisiones"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "cerebro_voz"
tags: ["proyecto", "decisiones", "voz"]
generado_por: "claude"
verificado: false
fuente: "Sesión Claude 2026-11-03"
---
# Decisiones — Cerebro Voz

## 2026-11-03 — Identidad de la voz
- **Decisión:** voz original de Cerebro (Piper + efecto). No se clona la voz de ningún actor ni personaje.
- **Motivo:** clonar la voz de una persona real sin su consentimiento no es aceptable; una voz propia es además una identidad única.

## 2026-11-03 — LLM por fases
- **Decisión:** fase 1 sin LLM (reglas). Fase 2 con API de Gemini de pago (Flash) y límite de gasto mensual. Descartado el nivel gratuito.
- **Motivo:** las órdenes diarias (anotar, estado, siguiente acción) no necesitan IA. El nivel gratuito puede usar los datos para entrenar; el de pago cuesta céntimos con este uso. Gemini por coste y porque el usuario ya usa su ecosistema.

## 2026-11-03 — Todo local en fase 1
- **Decisión:** STT y TTS locales en CPU; fase 1 sin llamadas de red.
- **Motivo:** privacidad (el micrófono no sale del PC), coste cero y funciona sin conexión.

## 2026-11-03 — Activación
- **Decisión:** atajo de teclado global primero; palabra «Cerebro» con openWakeWord a medida después.
- **Motivo:** la palabra personalizada requiere entrenar un modelo; el atajo permite usarlo desde el primer día.

## 2026-11-03 — Higiene
- **Decisión:** los errores y los logs técnicos van a un log local en `C:\dev\cerebro-voz\logs`, nunca a la bóveda. Solo se dicta contenido personal.
- **Motivo:** reglas de higiene de memoria y de seguridad de CEREBRO.

## 2026-11-03 — Interfaz de conversación
- **Decisión:** la interfaz web CEREBRO // CORE (`127.0.0.1:3000`) es el cliente de voz: clic en la esfera abre el modo conversación con turnos automáticos por detección de silencio. El núcleo Python sirve en `127.0.0.1:3001`. Prohibida la Web Speech API del navegador.
- **Motivo:** la Web Speech API envía el audio a servidores externos, lo que rompe la decisión «todo local en fase 1». Separar interfaz y núcleo permite reutilizar el núcleo desde la PWA del home server.

## 2026-11-03 — Alcance de la «conversación»
- **Decisión:** en fase 1 el modo conversación entiende las órdenes del router. Para charla libre y preguntas abiertas hace falta la fase 2 (Gemini de pago), que se enchufa en el router como respuesta por defecto.
- **Motivo:** sin LLM no hay comprensión libre; con LLM, el coste y la privacidad quedan controlados por el límite de gasto.