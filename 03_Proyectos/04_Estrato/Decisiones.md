---
area: desarrollo
tipo: decisiones
proyecto: estrato
estado: activo
fecha: 2026-11-02
tags: []
---

# Decisiones — Estrato

Formato: fecha | decisión | motivo.

---

- 2026-10-29 | Electron + three.js con PrusaSlicer como motor por línea de comandos | Escribir un motor de laminado propio son años de trabajo; PrusaSlicer es libre, maduro y se controla por completo con un 3MF.
- 2026-10-29 | Perfiles de OrcaSlicer y Cura se leen en tiempo de ejecución, no se incluyen | Evitar redistribuir material AGPL/LGPL dentro de Estrato.
- 2026-10-30 | PrusaSlicer 2.9.6 recortado (129 MB) incluido en el instalador | El usuario no tiene que instalar nada aparte; el recorte da el mismo G-code que la instalación completa.
- 2026-10-30 | Con E relativa y Marlin, Estrato añade `G92 E0` al G-code de capa; con E absoluta lo quita | PrusaSlicer se niega a laminar sin esa línea.
- 2026-10-30 | Licencia PolyForm Noncommercial 1.0.0 | Permite ver y usar el código pero prohíbe el uso comercial sin permiso escrito. PrusaSlicer va como programa aparte y conserva su AGPL.
- 2026-10-31 | Repositorio privado `abri50/Estrato`; los `.exe` van en Releases, no en el repositorio | Límite de 25 MB por archivo en la web de GitHub.
