---
tipo: "decisiones"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "cerebro"
tags: ["proyecto", "decisiones"]
generado_por: "claude"
verificado: false
fuente: "Sesión de diseño Claude 2026-11-02/03"
---
# Decisiones — CEREBRO

## 2026-11-02 — Propósito
- **Decisión:** CEREBRO sirve para unificar proyectos entre IAs y que varias trabajen en el mismo proyecto. Sin gestor gráfico propio por ahora.
- **Motivo:** el valor está en el traspaso de contexto, no en la interfaz.

## 2026-11-02 — Acceso de Claude a la bóveda
- **Decisión:** MCP integrado del plugin Local REST API (v5.5.2) con `mcp-remote` y certificado en `C:\Users\aam12\.obsidian-rest\`. La configuración va en el archivo que abre Ajustes → Desarrollador → Editar configuración, no en `%APPDATA%\Claude\`.
- **Motivo:** `msdanyg/smart-connections-mcp` es incompatible con Smart Connections 4.7 (formato `.smart-env/multi/`). Claude Desktop usa una ruta de configuración virtualizada.

## 2026-11-02 — Búsqueda semántica
- **Decisión:** aplazada hasta tener más de 50 notas reales. Candidato: fork `ilmoniemi/smart-connections-mcp` (compatible con SC 4.7).
- **Motivo:** con la bóveda vacía no aporta y cada MCP añade contexto fijo a cada mensaje.

## 2026-11-02 — Formato del registro
- **Decisión:** lista con una sección `##` por entrada, no tabla.
- **Motivo:** RAG trocea por encabezados (un vector por entrada), lecturas parciales por MCP y añadir es barato.

## 2026-11-02 — Material universitario
- **Decisión:** PDF y vídeos fuera de la bóveda (`C:\UI1\<asignatura>\`); en CEREBRO solo resúmenes Markdown, una nota por unidad, y `Errores.md` por asignatura. NotebookLM lo usa el usuario directamente.
- **Motivo:** binarios en Git, derechos de la universidad, RAG ineficaz sobre PDF y coste de tokens de navegar NotebookLM.

## 2026-11-02 — Visualización
- **Decisión:** Dataview ya; dashboard Node (`C:\dev\cerebro-dashboard`, fuera de la bóveda, solo lectura, `127.0.0.1`) tras 3-4 semanas de datos; PWA en el home server más adelante.
- **Motivo:** el esquema debe probarse con datos reales antes de construir código sobre él.

## 2026-11-02 — Modelos e IA local
- **Decisión:** sin Ollama ni APIs de pago. Se usan las suscripciones (Claude, Gemini Pro) a través de sus apps y de Antigravity.
- **Motivo:** hardware insuficiente; las suscripciones no incluyen API; el nivel gratuito de la API de Gemini puede usar los datos para entrenar.

## 2026-11-02 — Enrutado y delegación
- **Decisión:** tabla `06_Enrutado_IAs.md` + cola `05_Cola_Antigravity.md`. Claude decide y especifica; Antigravity ejecuta lo mecánico; NotebookLM para el temario; tareas de menos de 2 minutos las hace la IA actual.
- **Motivo:** reservar los tokens de Claude para lo que requiere criterio.

## 2026-11-02 — Versionado
- **Decisión:** Git con repo privado `abri50/cerebro`; `.gitignore` excluye `data.json` del REST API, `workspace*.json` y `.smart-env/`; correo noreply de GitHub en los commits.
- **Motivo:** las IAs escriben solas en disco; Git da historial, copia y reversión.

## 2026-11-02 — Seguridad
- **Decisión:** nada oficial, clasificado, de personal ni operativo en `01_Ejercito`. El futuro Atajo de iOS, solo para uso personal. Ningún secreto en notas.
- **Motivo:** la bóveda la leen IAs en la nube y se sincroniza fuera del PC.

## 2026-11-02 — Arquitectura futura (home server)
- **Decisión:** ThinkCentre con Linux + Docker como copia maestra; MCP remoto sobre archivos (no requiere Obsidian) publicado con Cloudflare Tunnel + OAuth; Syncthing o Git hacia PC e iPhone; embeddings en CPU. Supabase solo para lo público o multiusuario (combatwarrior, Intendencia).
- **Motivo:** los conectores de Claude se llaman desde la nube (Tailscale no basta); el plugin REST necesita la app de Obsidian abierta.

## 2026-11-03 — Lecciones del análisis de JARVIS
- **Decisión:** fallback (ante la duda, resuelve la IA actual), higiene de memoria (solo resultados verificados), rotación del registro a los 20 entradas, contrato de verificación (`generado_por`, `verificado`, `fuente`, sección «Por comprobar»).
- **Motivo:** evitar callejones sin salida, contexto contaminado y datos inventados.

## 2026-11-03 — Voz
- **Decisión:** voz en dos sentidos sin coste de API: captura con Atajo de iOS (dictado → `00_Sistema_IA/00_Inbox.md` vía plugin Advanced URI) que Antigravity archiva con "procesa inbox", y lectura con Atajo (Siri lee `00_Estado_Actual.md`). Conversación por voz con IA: modos de voz de las apps de Claude y Gemini. Asistente de voz propio (STT Whisper + TTS Piper en el home server) aplazado: el razonamiento seguiría necesitando una API de pago.
- **Motivo:** la captura es lo que más fricción quita; dictar cuesta 0 tokens y el archivado lo hace Antigravity con Flash. Dictar solo contenido personal, nunca del destino.