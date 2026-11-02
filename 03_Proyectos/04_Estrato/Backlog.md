---
area: desarrollo
tipo: backlog
proyecto: estrato
estado: activo
fecha: 2026-11-02
tags: []
---

# Backlog — Estrato

## Ahora
- [ ] Publicar Release v0.1.0 en GitHub con `Estrato-Instalador-0.1.0.exe` y `Estrato-Portable-0.1.0.exe` (a mano desde la web: la sesión de Claude no puede crear Releases).
- [ ] Probar un laminado e impresión real en la Ender 3 SE y comparar con Cura.
- [ ] En `C:\dev\Estrato`: `git pull` y `git push` del commit local con AGENTS/GEMINI/CLAUDE.md.

## Siguiente
- [ ] Verificar en Windows real: tooltips con atajo, control por USB y subida a OctoPrint/Moonraker.
- [ ] Crear un perfil propio de la Ender 3 SE (ahora usa el genérico 220×220).
- [ ] Firmar el ejecutable para quitar el aviso de SmartScreen (requiere certificado de pago; opcional).

## Ideas
- [ ] Automatizar la impresión de adaptadores (M-LOK, Skådis) desde CEREBRO.

## Hecho
- [x] v0.1.0: todas las funciones de Simplify3D, importadores de OrcaSlicer y Cura, calibración y control de impresora.
- [x] PrusaSlicer 2.9.6 incluido en el instalador.
- [x] Interfaz v2 (temas, inicio, iconos, avisos, progreso real).
- [x] Licencia PolyForm Noncommercial y repositorio privado en GitHub.
- [x] Logo corregido en el paquete (2026-10-31).
