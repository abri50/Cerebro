---
tipo: "nota"
area: "desarrollo"
fecha: 2026-11-03
estado: "activo"
proyecto: "cerebro"
tags: ["proyecto", "diseno", "hud"]
generado_por: "claude"
verificado: false
fuente: "Diseño Claude 2026-11-03"
---
# HUD CEREBRO // CORE — Especificación de diseño v2

## Principio rector
**Cada número y cada elemento animado representa un dato real.** Lo decorativo se distingue visualmente (opacidad ≤ 25 %) y nunca se mezcla con datos. Un adorno falso al lado de un dato real vuelve sospechoso al dato.

## Layout (escritorio, ≥ 1280 px)
```
┌ Barra superior: CEREBRO // CORE · notas · tareas en cola · último commit Git · VOZ ● · REST ● · reloj ┐
├ Panel ESTADO (izq, 320px) ┬ NÚCLEO (centro) ┬ Panel OPERACIONES (der, 360px) ┤
│ Prioridades semana        │ esfera + estado │ Cola Antigravity (pendientes)  │
│ Próxima evaluación (T-d)  │ de voz          │ Últimas 5 entradas del registro│
│ Bloque TB + volumen 7 d   │                 │   con badge de IA              │
│ Alertas de mantenimiento  │                 │ Proyectos activos + siguiente  │
├──────────────────────────── Terminal (plegable) ───────────────────────────┤
```
- < 1280 px: paneles laterales en pestañas bajo el núcleo. Móvil (PWA futura): núcleo arriba, paneles en tarjetas.

## Sistema visual
- **Fondo:** `#07040b` + ruido sutil (2 %) + scanlines (3 %, desactivables).
- **Paneles:** `rgba(18,8,28,.62)`, `backdrop-filter: blur(8px)`, borde 1 px `rgba(255,46,99,.28)`, esquinas en corchete HUD (pseudo-elementos de 10 px) en vez de bordes redondeados.
- **Color semántico (solo con significado):**
  - Primario / identidad: `#ff2e63`
  - Sistema / pensando: `#22d3ee`
  - OK: `#10b981` · Aviso: `#f59e0b` · Fallo: `#ef4444`
  - Texto: `#e9e3f0` · secundario `#9a8fa8` · decorativo `rgba(233,227,240,.22)`
- **Tipografía:** datos y terminal en `JetBrains Mono` (12-14 px); títulos de panel en `Rajdhani` 600, mayúsculas, `letter-spacing: .12em`, 11-12 px. Nunca más de 2 familias.
- **Rejilla:** 8 px. Paneles con padding de 16 px y separación de 12 px.
- **Contraste:** texto de datos ≥ AA (4,5:1) sobre el panel.

## Núcleo (esfera)
- Three.js con `ShaderMaterial`: desplazamiento por ruido simplex en el vértice; uniforms `uAmp` (amplitud de audio), `uState` y `uColor`.
- **Estados** (transición de 300 ms entre uniforms):
  - `reposo`: giro lento, desplazamiento mínimo
  - `escuchando`: desplazamiento ∝ amplitud del micrófono
  - `pensando`: color sistema, rotación ×3, ondas
  - `hablando`: desplazamiento ∝ amplitud de la respuesta
  - `desconectado`: gris, sin animación
- **Color base = salud global:** primario si todo OK; aviso si el mantenimiento tiene alertas; fallo si el servicio de voz o la bóveda no responden.
- **Partículas orbitales = tareas pendientes** de la cola (1 partícula por tarea; clic → muestra la tarea). Decoración ligada a datos.
- Bloom (`UnrealBloomPass`) con intensidad baja (≤ 0,6). `pixelRatio` máximo de 1,5. El render se pausa con la pestaña oculta.

## Movimiento
- UI: 150-250 ms `cubic-bezier(.2,.8,.2,1)`. Nada parpadea más de una vez.
- Arranque: secuencia de ≤ 1,5 s (líneas de estado reales: «Bóveda… OK», «Voz… OK»), saltable con cualquier tecla, solo en la primera carga del día.
- `prefers-reduced-motion`: sin arranque, esfera estática, sin scanlines.

## Datos (servidor Node, solo lectura sobre la bóveda)
- `GET /api/estado` → `00_Estado_Actual.md` parseado por secciones
- `GET /api/cola` → tareas de `## Pendientes` (id, título, modelo)
- `GET /api/registro?limit=5` → últimas entradas (fecha, IA, proyecto, hecho)
- `GET /api/proyectos` → frontmatter de cada `00_Resumen.md` con `estado: activo`
- `GET /api/salud` → último commit Git, servicio de voz (3001), número de notas
- Actualización: SSE con `chokidar` sobre la bóveda; sin sondeo periódico.

## Fuera
- Métricas inventadas o valores aleatorios.
- Más de un elemento con brillo intenso a la vez.
- Fuentes o librerías cargadas desde CDN en producción (copias locales).
