---
tipo: "core_prompt"
area: "sistema"
fecha: 2026-11-03
estado: "activo"
tags: ["sistema", "mantenimiento"]
---

# Rutina de Mantenimiento Semanal de CEREBRO

Este procedimiento lo ejecuta cualquier IA cuando el usuario dice: «ejecuta mantenimiento».

## Pasos de la Rutina

0. **Procesar el inbox:**
   - Procesa el inbox siguiendo `00_Sistema_IA/Prompts/Procesar_Inbox.md`.

1. **Rotación del registro:**
   - Si `00_Sistema_IA/02_Registro_Actividad_IAs.md` supera las 20 entradas, mueve sin modificarlas las entradas de meses anteriores a `00_Sistema_IA/Registro_Archivo/AAAA-MM.md`. En el registro activo permanece únicamente el mes en curso.

2. **Salud YAML:**
   - Escanea todos los archivos `.md` de la bóveda (excluyendo `.obsidian/`, `00_Sistema_IA/Plantillas/` y `00_Sistema_IA/Registro_Archivo/`).
   - Identifica y lista aquellos que carezcan de los campos obligatorios `tipo`, `area` o `fecha`.
   - *Regla:* Solo se informa en la revisión, no se corrigen automáticamente.

3. **Proyectos parados:**
   - Revisa todos los archivos `00_Resumen.md` en `03_Proyectos/`.
   - Lista aquellos con `estado: "activo"` que no hayan registrado modificaciones o actividad en los últimos 14 días.
   - *Regla:* Solo se informa en la revisión, no se modifica su estado.

4. **Notas sin verificar:**
   - Lista todas las notas de la bóveda que contengan en su frontmatter `verificado: false`.
   - *Regla:* Solo se informa en la revisión, no se cambia el valor.

5. **Actualización del Índice General:**
   - Comprueba `00_Sistema_IA/03_Indice_General.md`.
   - Si falta algún enlace a un `00_Resumen.md` de cualquier área (`01_Ejercito/`, `02_Estudios/`, `03_Proyectos/`, `04_Recursos/`), añade el enlace correspondiente en su sección sin borrar contenido existente.

6. **Generación de la Nota de Revisión:**
   - Crea una nota en `00_Sistema_IA/Revisiones/AAAA-Wnn.md` (donde `AAAA-Wnn` es el año y la semana ISO actual) con la siguiente estructura:
     - Frontmatter YAML estándar (`tipo: revision`, `area: sistema`, `fecha: AAAA-MM-DD`, `estado: completado`, `tags: ["sistema", "revision"]`).
     - `## Hecho esta semana`: recopilación de actividades realizadas a partir de `02_Registro_Actividad_IAs.md`.
     - `## Pendiente`: tareas pendientes en `05_Cola_Antigravity.md` y tareas en la sección "Ahora" de los `Backlog.md` de proyectos activos.
     - `## Alertas de mantenimiento`: resultados informativos de los puntos 2 (salud YAML), 3 (proyectos parados) y 4 (sin verificar).
     - `## Propuesta para 00_Estado_Actual`: borrador o sugerencia de actualización de prioridades para `00_Estado_Actual.md`. *(Importante: no editar directamente `00_Estado_Actual.md`, solo proponer)*.

7. **Registro de actividad:**
   - Añade una entrada al final de `00_Sistema_IA/02_Registro_Actividad_IAs.md` indicando la ejecución de la rutina de mantenimiento.
