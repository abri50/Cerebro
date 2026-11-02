---
tipo: "proyecto"
area: "desarrollo"
fecha: 2026-11-02
estado: "activo"
proyecto: intendencia
siguiente_accion: "Revisar el proyecto real de Supabase (segunda cuenta) y ajustar 5 tests que dependen de la fecha"
prioridad: 2
stack: [html, tailwind, supabase]
tags: ["codigo", "proyecto"]
---

# Intendencia

## Qué es

App web de gestión financiera personal.

## Stack

- **Frontend:** Vanilla HTML/CSS/JS + Tailwind
- **Backend:** Supabase con cifrado AES-GCM del lado del cliente
- **Despliegue:** Vercel

## Estado actual (v79, 2026-11-02)

- **Repositorio:** `abri50/asesor-financiero` (privado). Producción: https://asesor-financiero-blond.vercel.app (despliegue automático desde `main`).
- **Arquitectura:** HTML estático generado por `src/build.py` a partir de `src/app.html`, bloques `src/block*.js` y CSS. Datos locales; sincronización cifrada de extremo a extremo (AES-GCM) con Supabase. PWA para iPhone (escritorio).
- **Auditor:** Gemini vía función de Vercel (`api/chat-auditor.js`, streaming). Solo envía un resumen financiero cuando el usuario pulsa Enviar. La clave está en la variable `API_GEMINI` de Vercel.
- **Hecho recientemente:** mes de gestión de nómina a nómina, categorías recuperables, Auditor en directo, logo y nombre Intendencia con créditos, fijos con periodicidad y adelanto de pagos, selector de mes, mismas cifras en todas las pantallas.
- **Tests:** suite Playwright en `src/tests` (86 archivos). 5 fallan por depender de la fecha del sistema (t18, t23, t41, t45, t53).
