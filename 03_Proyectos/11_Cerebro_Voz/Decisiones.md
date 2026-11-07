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

## 2026-11-03 — Portabilidad al home server (obligatoria desde la fase 1)
- **Decisión:** todo componente de Cerebro (núcleo de voz, HUD, futuros trabajadores) debe poder ejecutarse sin cambios de código en Linux dentro de Docker:
  - Rutas y puertos solo por configuración o variables de entorno (`CEREBRO_VAULT`, `VOZ_HOST`, `VOZ_PORT`); nada de rutas de Windows en el código.
  - El micrófono y el altavoz pertenecen al **cliente** (navegador, PWA). El servidor solo recibe audio y devuelve audio. El atajo de teclado es un cliente opcional, separado del núcleo.
  - La bóveda se lee y escribe como archivos `.md` (sin depender del plugin REST de Obsidian, que necesita la app abierta).
  - Escucha en `127.0.0.1` por defecto; para exponerlo se pone delante un proxy con autenticación (fase 5), nunca abriendo el puerto directamente.
  - Incluir `Dockerfile` y `docker-compose.yml` (servicios `hud`, `voz`) aunque hoy se ejecute en Windows.
- **Motivo:** la fase 5 lleva Cerebro al ThinkCentre (24/7) con acceso desde cualquier portátil o el iPhone. Si se diseña portable ahora, migrar será copiar contenedores; si no, habría que reescribirlo.

## 2026-11-03 — LLM local primero
- **Decisión:** la fase 2 usa Ollama en la RX 6900 XT (16 GB) como LLM por defecto; Gemini de pago pasa a ser un respaldo opcional. Proveedor intercambiable por configuración.
- **Motivo:** hay hardware capaz (antes se creía que no). Coste 0 y privacidad total; la fase 6 del roadmap (cerebro propio) se adelanta. Gemini solo para lo que el modelo local no resuelva bien.

## 2026-11-07 — Configuración de LLM por equipo (T-11A)
- **Decisión:** `llm_provider` se define en `config.local.toml` (ignorado por Git) para permitir portabilidad entre el portátil (modo solo reglas con provider="ninguno") y el PC de sobremesa (Ollama en GPU RX 6900 XT).
- **Motivo:** independencia entre hardware de desarrollo y de producción; seguridad y prevención de fallos sin GPU dedicada.
