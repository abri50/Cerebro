# CEREBRO — Arranque para agentes de IA
Antes de actuar, lee en este orden:
1. 00_Sistema_IA/00_Estado_Actual.md (foco actual)
2. 00_Sistema_IA/01_Instrucciones_Generales.md (perfil, reglas y protocolo de traspaso)
3. 00_Sistema_IA/06_Enrutado_IAs.md (qué IA hace cada tarea)
4. Si la tarea es de un proyecto: su 00_Resumen.md, Backlog.md y las 3 últimas entradas de 00_Sistema_IA/02_Registro_Actividad_IAs.md que mencionen ese proyecto.
Al terminar: cumple el "Protocolo de traspaso" de 01_Instrucciones_Generales.md.
Nunca escribas secretos (API keys, tokens, contraseñas) ni información oficial o clasificada en la bóveda.
Toda nota que generes cumple la sección "Notas generadas por IA" de 00_Sistema_IA/04_Esquema_YAML.md.

## Cola de tareas
- Si el usuario dice "ejecuta la cola": procesa en orden las tareas de 00_Sistema_IA/05_Cola_Antigravity.md (sección Pendientes). Por cada una: ejecuta, verifica el criterio de hecho, muévela a Hechas con el resultado y añade su entrada al registro de actividad. Si una tarea es ambigua o requiere una decisión, déjala en Pendientes con una línea "Bloqueada: <motivo>" y continúa con la siguiente.
- Claude no ejecuta trabajo mecánico (archivos, formato, código ya especificado, instalaciones, git): lo añade a la cola con una orden completa y verificable.
