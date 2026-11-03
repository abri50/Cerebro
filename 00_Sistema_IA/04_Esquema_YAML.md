---
tipo: "core_prompt"
area: "sistema"
fecha: 2026-11-02
estado: "activo"
tags: ["sistema", "esquema"]
---

# Esquema YAML estandarizado (Fase 0)

## Proyecto

```yaml
---
tipo: "proyecto"
area: "desarrollo"
fecha: 2026-11-02
estado: "activo"
proyecto: ""
siguiente_accion: ""
prioridad: 2
tags: ["codigo", "proyecto"]
---
```

| Clave | Tipo de dato | Valores permitidos |
|---|---|---|
| `tipo` | string | `"proyecto"` |
| `area` | string | `"desarrollo"` |
| `fecha` | string (AAAA-MM-DD) | Fecha de creación de la nota |
| `estado` | string | `activo` \| `pausado` \| `finalizado` |
| `proyecto` | string | Slug en minúsculas del proyecto (ej. `combatwarrior`, `intendencia`) |
| `siguiente_accion` | string | Descripción breve de la próxima acción accionable |
| `prioridad` | entero | `1` (alta) \| `2` (media) \| `3` (baja) |
| `tags` | lista de strings | Incluye `codigo`, `proyecto` y etiquetas específicas |

## Entrenamiento

```yaml
---
tipo: "entrenamiento"
area: "ejercito"
fecha: 2026-11-02
estado: "completado"
modalidad: ""
fase_tb: ""
volumen_kg: 0
distancia_km: 0.0
carga_ruck_kg: 0
duracion_min: 0
rpe: 0
tags: ["entrenamiento", "tactico"]
---
```

| Clave | Tipo de dato | Valores permitidos |
|---|---|---|
| `tipo` | string | `"entrenamiento"` |
| `area` | string | `"ejercito"` |
| `fecha` | string (AAAA-MM-DD) | Fecha de la sesión |
| `estado` | string | `completado` \| `parcial` \| `cancelado` |
| `modalidad` | string | `fuerza` \| `rucking` \| `carrera` \| `tactico` |
| `fase_tb` | string | `base_building` \| `operator` \| `fighter` |
| `volumen_kg` | entero | Numérico sin unidades ni comillas, `0` si no aplica |
| `distancia_km` | decimal | Numérico sin unidades ni comillas, `0.0` si no aplica |
| `carga_ruck_kg` | entero | Numérico sin unidades ni comillas, `0` si no aplica |
| `duracion_min` | entero | Numérico en minutos sin unidades ni comillas, `0` si no aplica |
| `rpe` | entero | Entero `1`-`10` (escala RPE de esfuerzo percibido), `0` si no aplica |
| `tags` | lista de strings | `["entrenamiento", "tactico"]` |

## Asignatura

```yaml
---
tipo: "asignatura"
area: "universidad"
fecha: 2026-11-02
estado: "pendiente"
asignatura: ""
trimestre: 0
tags: ["universidad", "asignatura"]
---
```

| Clave | Tipo de dato | Valores permitidos |
|---|---|---|
| `tipo` | string | `"asignatura"` |
| `area` | string | `"universidad"` |
| `fecha` | string (AAAA-MM-DD) | Fecha de creación de la nota |
| `estado` | string | `pendiente` \| `en_curso` \| `superada` |
| `asignatura` | string | Slug sin tildes de la asignatura (ej. `interfaces_de_usuario`, `dpoo`) |
| `trimestre` | entero | Entero del trimestre (`1`, `2`, `3`) |
| `tags` | lista de strings | `["universidad", "asignatura"]` |

## Sesión de estudio

```yaml
---
tipo: "sesion_estudio"
area: "universidad"
fecha: 2026-11-02
estado: "completado"
asignatura: ""
horas_estudio: 0.0
tags: ["universidad", "sesion"]
---
```

| Clave | Tipo de dato | Valores permitidos |
|---|---|---|
| `tipo` | string | `"sesion_estudio"` |
| `area` | string | `"universidad"` |
| `fecha` | string (AAAA-MM-DD) | Fecha de la sesión |
| `estado` | string | `completado` \| `parcial` \| `cancelado` |
| `asignatura` | string | Slug sin tildes correspondiente a la asignatura estudiada |
| `horas_estudio` | decimal | Horas en formato decimal (ej. `1.5`), `0.0` si no aplica |
| `tags` | lista de strings | `["universidad", "sesion"]` |

## Ubicación de las notas

- **entrenamiento:** `01_Ejercito/04_Preparacion_Fisica/`
- **asignatura:** `00_Resumen.md` de cada asignatura en `02_Estudios/`
- **sesion_estudio:** `Apuntes/` de la asignatura correspondiente
- **proyecto:** `00_Resumen.md` de cada proyecto en `03_Proyectos/`

## Log de IAs

No usa YAML por entrada; es un archivo único con una sección `##` por entrada (ver [[02_Registro_Actividad_IAs]]).

## Notas generadas por IA

Toda nota creada o redactada por una IA debe incorporar en su frontmatter YAML las siguientes claves obligatorias adicionales:

```yaml
generado_por: claude | antigravity | gemini | notebooklm
verificado: false
fuente: "" # ruta a archivo de la bóveda, URL o "conocimiento del modelo"
```

| Clave | Tipo de dato | Valores permitidos |
|---|---|---|
| `generado_por` | string | `claude` \| `antigravity` \| `gemini` \| `notebooklm` |
| `verificado` | booleano | Inicialmente `false`. Solo el usuario cambia `verificado` a `true`. |
| `fuente` | string | Ruta interna a la nota fuente, URL externa o `"conocimiento del modelo"` |

**Regla de verificación:** fechas, cifras y datos que no salgan de una fuente citada van en una sección final `## Por comprobar`. Solo el usuario cambia `verificado` a `true`.
