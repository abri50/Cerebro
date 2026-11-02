---
tipo: "proyecto"
area: "desarrollo"
fecha: 2026-11-02
estado: "activo"
proyecto: estrato
siguiente_accion: "Publicar Release v0.1.0 en GitHub con los dos .exe y probar un laminado e impresión real en la Ender 3 SE"
prioridad: 2
stack: [electron, threejs, prusaslicer]
tags: ["codigo", "proyecto"]
---

# Estrato

## Qué es

Laminador 3D de escritorio para Windows, de uso propio, al estilo Simplify3D. La interfaz es propia; el laminado lo hace PrusaSlicer 2.9.6, que va incluido en el instalador.

## Stack

- **Framework:** Electron 33 + three.js 0.170, empaquetado con esbuild.
- **Motor:** PrusaSlicer 2.9.6 por línea de comandos. Estrato le pasa un 3MF con la configuración global, la de cada pieza y los rangos de altura.
- **Distribución:** electron-builder: instalador NSIS y versión portable (x64), ~115 MB cada uno. Sin firmar: Windows muestra el aviso de SmartScreen.

## Funcionalidades implementadas (v0.1.0)

- Varios procesos por pieza y por rango de altura.
- Soportes manuales (pilares reales, bloqueadores y forzadores).
- Vista previa del G-code (tubos iluminados, raíl de capas y de movimientos).
- Perfiles de impresora (30 de serie) y de material (14).
- Multiextrusor con torre de purga; eventos por altura (color, pausa, G-code propio).
- Calibración: torre de temperatura, flujo, pressure advance, retracción, volumétrico máximo, VFA y primera capa.
- Importación de perfiles de OrcaSlicer y Cura (se leen en tiempo de ejecución, no se incluyen).
- Control de impresora por USB (serie) y por red (OctoPrint, Moonraker).
- Reparación, corte, orientación automática y capas adaptativas.
- Interfaz v2: tema claro y oscuro con acento, pantalla de inicio, iconos Lucide, avisos y barra de progreso real.

## Estado

- Laminado real verificado con PrusaSlicer 2.9.6 (rangos de altura, perfil importado de Orca, multiextrusor).
- Instalado y arrancando en el PC del usuario (2026-10-31). Logo corregido en esa versión.
- Pruebas automáticas de núcleo, campos, mallas, impresora, calibración e importadores pasan (`npm test`).

## Repositorio

- **Ruta local:** `C:\dev\Estrato`
- **Remoto:** `https://github.com/abri50/Estrato.git` (privado, rama `main`)
- **Licencia:** PolyForm Noncommercial 1.0.0. PrusaSlicer incluido conserva su AGPL-3.0.
- **Compilar:** `npm install`, `bash tools/fetch-prusaslicer.sh` (motor en `vendor/`), `npm run build` y `npm run dist:win`.
