---
tipo: "plan"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "cerebro"
tags: ["proyecto", "roadmap", "ia"]
generado_por: "claude"
verificado: false
fuente: "Diseño Claude 2026-11-03"
---
# Roadmap: Cerebro como orquestador

## Visión
Cerebro deja de ser una bóveda que leen las IAs y pasa a ser **el agente que las dirige**: recibe la orden (voz o texto), decide, reparte el trabajo entre modelos y herramientas, supervisa el resultado y lo guarda en su memoria. Tú hablas solo con Cerebro.

## Arquitectura objetivo
```
Tú (voz/texto) → CEREBRO (orquestador)
                  ├─ Memoria: bóveda .md + índice de embeddings
                  ├─ Router: reglas → modelo local pequeño → modelo grande
                  ├─ Trabajadores:
                  │    · modelo local (Ollama): clasificar, resumir, charla, RAG
                  │    · Claude (claude -p / API): arquitectura, código difícil, revisión
                  │    · Gemini / Antigravity CLI: ejecución en disco, búsqueda web
                  ├─ Herramientas (MCP): bóveda, Git, Supabase, Vercel, calendario…
                  └─ Supervisión: aprobaciones humanas, registro, límites de gasto
```

## Fases
| Fase | Qué gana Cerebro | Requisito |
|---|---|---|
| 1 (en curso) | Voz local, órdenes por reglas, HUD con datos reales | Ninguno |
| 2 | Conversación libre (Gemini Flash de pago) | Clave API + límite de gasto |
| 3 | **Delegación real**: Cerebro lanza tareas a Claude Code (`claude -p`) y a Antigravity/Gemini CLI en modo no interactivo, con la cola como contrato | Revisar límites y términos de cada suscripción |
| 4 | Memoria semántica propia (embeddings locales en CPU) | Más de 50 notas |
| 5 | Home server: Cerebro siempre encendido, MCP remoto, PWA en el iPhone | ThinkCentre montado |
| 6 | **Cerebro con cerebro propio**: modelo local en Ollama como router y voz conversacional; los modelos grandes solo para lo difícil | GPU con 12-16 GB de VRAM o equipo con memoria unificada alta |

## Reglas de gobierno (desde el primer día)
1. **Humano en el bucle:** publicar, borrar, push, pagos o cualquier acción irreversible requieren tu aprobación explícita.
2. **Mínimo privilegio:** cada trabajador recibe solo las carpetas y herramientas de su tarea.
3. **Todo queda registrado:** cada orden delegada deja traza en el registro.
4. **Presupuesto:** límite de gasto mensual por proveedor; Cerebro se degrada a reglas si se alcanza.
5. **Evaluación:** cada prompt del router tiene un conjunto de pruebas (frase → destino esperado) que se ejecuta antes de cambiarlo.

## Plan de aprendizaje (ligado a cada fase)
| Fase | Concepto que aprendes | Práctica |
|---|---|---|
| 1 | STT/TTS, audio en el navegador, arquitectura cliente-servicio | T-07 y T-08 |
| 2 | Llamadas a LLM, *system prompts*, salida estructurada, coste por token | Router con LLM por defecto |
| 3 | Agentes y *tool calling*, orquestación, contratos de tarea | Cerebro → `claude -p` / CLI de Antigravity |
| 4 | Embeddings, RAG, troceado, recuperación híbrida | Índice propio sobre la bóveda |
| 5 | Docker, redes, túneles, OAuth, MCP remoto | Migración al home server |
| 6 | Inferencia local, cuantización, VRAM, evaluación de modelos | Ollama como router y elegir el modelo con tus pruebas |
