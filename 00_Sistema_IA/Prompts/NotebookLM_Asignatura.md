---
tipo: "core_prompt"
area: "universidad"
fecha: 2026-11-03
estado: "activo"
tags: ["sistema", "prompt", "notebooklm"]
generado_por: "claude"
verificado: false
fuente: "Sesión Claude 2026-11-02"
---
# Prompts de NotebookLM por asignatura

## 1. Instrucción del cuaderno (Configurar chat → Personalizado)
Sustituye `<ASIGNATURA>` y `<EVALUACIÓN>`.

```
Contexto: asignatura <ASIGNATURA>, Grado en Ingeniería Informática, Universidad Isabel I. Evaluación: <EVALUACIÓN>. Objetivo doble: aprobar y dominar la materia.

Reglas:
1. Responde solo con base en las fuentes y cita siempre la unidad (UDx). Si algo no está en las fuentes, dilo explícitamente antes de completarlo.
2. Explica primero la idea en 2-3 líneas, después un ejemplo (código si aplica) y termina con una pregunta tipo test de 4 opciones.
3. Señala las trampas típicas de examen (conceptos que se confunden).
4. Si te explico un concepto con mis palabras, corrige los errores sin suavizarlos.
5. No adornes con anécdotas ni datos que no estén en las fuentes.
6. Español, directo, sin relleno.
```

## 2. Guía por unidad (para llevar a CEREBRO)
```
Genera la guía de estudio de la UD<N> en Markdown: ## por apartado, definiciones exactas del temario, ejemplo por concepto, tabla de conceptos que se confunden y 5 preguntas tipo test con solución justificada. Cita la UD en cada apartado. Lo que no esté en las fuentes, en una sección final "Por comprobar".
```

## 3. Simulacro de examen
```
Hazme un test de <N> preguntas tipo examen sobre las UD<lista>, mezclando dificultad. No muestres soluciones hasta que responda todas. Después corrige, explica cada fallo citando la UD y dame la lista de conceptos a repasar.
```

## Flujo
1. Una fuente por unidad en el cuaderno; transcripciones de clase si las hay.
2. Audio Overview por unidad (para ruck o coche).
3. Prompt 2 → revisar → pegar en `Apuntes/UDx_<tema>.md` con `generado_por: notebooklm`, `verificado: false`.
4. Cada fallo de test → `Errores.md` de la asignatura.
5. Semana de examen: prompt 3 + repaso de `Errores.md`.
