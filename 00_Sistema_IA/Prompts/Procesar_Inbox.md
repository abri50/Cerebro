---
tipo: "core_prompt"
area: "sistema"
fecha: 2026-11-03
estado: "activo"
tags: ["sistema", "inbox"]
---

# Rutina para Procesar el Inbox

Procedimiento para vaciar y archivar las entradas capturadas por voz en `00_Sistema_IA/00_Inbox.md` cuando el usuario dice: «procesa inbox».

## Reglas de Procesamiento

Por cada línea listada bajo `## Entradas` en `00_Sistema_IA/00_Inbox.md`, clasifica y archiva según su contenido:

1. **Entrenamiento táctico o físico:**
   - Detecta palabras clave: `ruck`, `km`, `kg`, `RPE`, `sesión`, `carrera`, `fuerza`, `dominadas`, etc.
   - Crea una nota nueva en `01_Ejercito/04_Preparacion_Fisica/AAAA-MM-DD_<modalidad>.md` basada en `Plantilla_Entrenamiento.md`.
   - Rellena solo los campos mencionados explícitamente en la captura de voz (el resto a 0 o valor por defecto).
   - Metadatos obligatorios de IA: `generado_por: antigravity`, `verificado: false`, `fuente: "inbox voz"`.

2. **Sesión de estudio académico:**
   - Detecta palabras clave: `asignatura`, `UD`, `horas`, `repasé`, etc.
   - Crea una nota de tipo `sesion_estudio` en la subcarpeta `Apuntes/` de la asignatura correspondiente en `02_Estudios/`.
   - Rellena las horas o contenidos dichos sin inventar datos adicionales.
   - Metadatos obligatorios de IA: `generado_por: antigravity`, `verificado: false`, `fuente: "inbox voz"`.

3. **Idea o tarea de proyecto:**
   - Si menciona el nombre de un proyecto conocido (`CombatWarrior`, `Intendencia`, `Forja`, `Estrato`, `Telon`, `Brio`, `Home Server`, `Visor PVS420`, `Cerebro`, `Cerebro Voz`, etc.):
   - Añade una línea `- [ ] <texto>` en la sección `## Ideas` del `Backlog.md` de ese proyecto.

4. **Duda de examen o error conceptual:**
   - Si se trata de un fallo, duda de examen o trampa:
   - Añade la entrada bajo `## Dudas y trampas` en `Errores.md` de la asignatura respectiva en `02_Estudios/`.

5. **Entrada ambigua o no clasificable:**
   - Si no hay suficiente información o el contexto es ambiguo:
   - **NO** inventes datos. La línea permanece en `## Entradas` con el prefijo `¿?`.

## Protocolo de Limpieza y Registro

- Mueve cada línea archivada con éxito desde `## Entradas` a `## Procesado`, añadiendo al final el enlace a la nota destino: `→ [[nota destino]]`.
- Registra la actividad en `00_Sistema_IA/02_Registro_Actividad_IAs.md` en una sola entrada indicando el número total de líneas procesadas y archivadas.
