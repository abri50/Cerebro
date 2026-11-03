---
tipo: "indice"
area: "sistema"
fecha: 2026-11-02
estado: "activo"
tags: ["sistema", "cola"]
---
# Cola de tareas para Antigravity
Formato de cada tarea (las añade Claude u otra IA al final de "Pendientes"):

```
### T-AAAAMMDD-NN — <título corto>
- **Proyecto:** <slug o cerebro>
- **Orden:** <instrucciones completas y verificables>
- **Criterio de hecho:** <cómo comprobar que está bien>
- **Modelo sugerido:** flash | pro
```

## Pendientes

## Hechas
##### T-20261103-01 — Reglas de memoria (lecciones JARVIS)
- **Proyecto:** cerebro
- **Orden:**
  1. En `00_Sistema_IA/06_Enrutado_IAs.md`, al final de "Reglas para toda IA que lea esto", añade: `7. Fallback: si dudas a qué herramienta derivar, o una derivación falla, hazlo tú con el modelo actual. Nunca dejes al usuario sin respuesta.`
  2. En `00_Sistema_IA/01_Instrucciones_Generales.md`, al final de la sección "Protocolo de traspaso entre IAs", añade: `**Higiene de memoria:** en CEREBRO solo se escriben resultados verificados. Intentos fallidos, mensajes de error y salidas de herramientas no se copian; se resumen en una línea ("Bloqueado: motivo").`
  3. Justo debajo, añade: `**Rotación del registro:** cuando 02_Registro_Actividad_IAs.md supere 20 entradas, Antigravity (flash) mueve sin modificarlas las entradas de meses anteriores a 00_Sistema_IA/Registro_Archivo/AAAA-MM.md y deja en el registro solo el mes en curso. Las IAs leen el archivo solo si lo necesitan.`
- **Criterio de hecho:** los tres textos están presentes literalmente; ningún otro contenido modificado.
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Añadida la regla 7 de fallback en `00_Sistema_IA/06_Enrutado_IAs.md`, y añadidas las cláusulas de "Higiene de memoria" y "Rotación del registro" en `00_Sistema_IA/01_Instrucciones_Generales.md`.

##### T-20261103-02 — Contrato de verificación para notas generadas por IA
- **Proyecto:** cerebro
- **Orden:**
  1. En `00_Sistema_IA/04_Esquema_YAML.md` añade al final la sección `## Notas generadas por IA` con: claves obligatorias adicionales `generado_por` (claude | antigravity | gemini | notebooklm), `verificado: false` y `fuente: ""` (ruta, URL o "conocimiento del modelo"). Regla: fechas, cifras y datos que no salgan de una fuente citada van en una sección final `## Por comprobar`. Solo el usuario cambia `verificado` a `true`.
  2. En `AGENTS.md`, en la lista de reglas finales, añade: `Toda nota que generes cumple la sección "Notas generadas por IA" de 00_Sistema_IA/04_Esquema_YAML.md.`
  3. Al final de `00_Sistema_IA/00_Dashboard.md` añade:
     ## 🔍 Pendiente de verificar
     ```dataview
     LIST generado_por
     FROM ""
     WHERE verificado = false
     SORT file.mtime DESC
     ```
- **Criterio de hecho:** las tres secciones existen; la consulta del dashboard se renderiza sin error en Obsidian.
- **Modelo sugerido:** flash
- **Resultado:** Completado el 2026-11-03. Añadida la sección "Notas generadas por IA" en `00_Sistema_IA/04_Esquema_YAML.md`, regla añadida en `AGENTS.md` y bloque Dataview "🔍 Pendiente de verificar" añadido en `00_Sistema_IA/00_Dashboard.md`.
