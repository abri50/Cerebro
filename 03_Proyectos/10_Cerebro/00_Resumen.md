---
tipo: "proyecto"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "cerebro"
siguiente_accion: "Configurar Obsidian Git y rellenar 00_Estado_Actual.md"
prioridad: 1
tags: ["codigo", "proyecto", "sistema"]
generado_por: "claude"
verificado: false
fuente: "Sesión de diseño Claude 2026-11-02/03"
---
# CEREBRO

## Qué es
Memoria compartida entre IAs (Claude, Antigravity, Gemini, NotebookLM): bóveda Obsidian para que cualquier IA retome cualquier proyecto donde lo dejó otra, gastando lo mínimo. No es una app ni un gestor gráfico.

## Piezas operativas
- Arranque: `AGENTS.md` (+ `GEMINI.md`, `CLAUDE.md`) → `00_Estado_Actual` → `01_Instrucciones_Generales` → `06_Enrutado_IAs`.
- Traspaso: protocolo en `01_Instrucciones_Generales.md`; registro en `02_Registro_Actividad_IAs.md`.
- Delegación: `05_Cola_Antigravity.md` ("ejecuta la cola"); skill `cerebro` en Claude.
- Datos: `04_Esquema_YAML.md`, plantillas tipadas, `00_Dashboard.md` (Dataview).
- Acceso Claude: MCP del plugin Local REST API (v5.5.2) vía `mcp-remote`; requiere Obsidian abierto.
- Versionado: Git, repo privado `abri50/cerebro`.

## Fases
1. ✅ Estructura, esquema, dashboard, traspaso y enrutado.
2. ⏳ Uso real 4 semanas (datos de entrenamiento, estudio y proyectos).
3. Búsqueda semántica (más de 50 notas).
4. Home server: copia maestra, MCP remoto, acceso desde cualquier dispositivo.
5. App PWA (captura, vistas, notificaciones, supervisión de IAs).

Detalle en [[Backlog]] y [[Decisiones]].
