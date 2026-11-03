---
area: desarrollo
tipo: decisiones
proyecto: home_server
estado: activo
fecha: 2026-11-02
tags: []
---

# Decisiones — Home Server

Formato: fecha | decisión | motivo.

---

## 2026-11-03 — Arquitectura del home server (propuesta Claude, pendiente de verificar)
- **Decisión:** ThinkCentre con **Ubuntu Server LTS** + **Docker Compose** (gestión visual con Dockge). Sin Proxmox de momento.
- **Servicios (un contenedor cada uno):**
  - **Cerebro:** bóveda, HUD, voz, router/LLM, trabajadores (Claude Code CLI y CLI de Antigravity/Gemini con sus suscripciones).
  - **Jellyfin:** streaming propio, libre y sin cuenta en la nube; transcodificación por la iGPU Intel (Quick Sync).
  - **Immich:** fotos del iPhone, con copia automática.
  - **Syncthing:** sincronización de la bóveda y de archivos con el PC y el iPhone (Nextcloud solo si se necesita compartir con terceros).
  - **Tailscale** (acceso privado desde portátiles y móvil) y **cloudflared** (solo el MCP remoto de Cerebro, con OAuth).
  - **Uptime Kuma** (servicios caídos) y copias de seguridad con **restic** (regla 3-2-1: disco externo + copia cifrada fuera de casa).
- **Cerebro como panel de mando del servidor:** lee el estado de Docker, disco (SMART), copias y servicios, y lo muestra en el HUD (panel «Servidor»). Reiniciar un contenedor, borrar o actualizar requiere tu aprobación.
- **Punto único de entrada:** todas las consultas van a Cerebro, que enruta a la IA adecuada; las apps de cada IA quedan como respaldo.
- **Motivo:** Ubuntu + Docker es la opción más simple de mantener y la más documentada; un contenedor por servicio permite actualizar o restaurar cada pieza por separado; Jellyfin e Immich encajan con la preferencia por software libre y autoalojado.
- **Pendiente:** modelo exacto, CPU, RAM y discos del ThinkCentre para dimensionar (Immich y Whisper son lo que más memoria consume).

## 2026-11-03 — Hardware disponible y plan híbrido
- **Inventario:** PC principal Ryzen 5 5600 + RX 6900 XT (16 GB VRAM); equipo Xeon E5-2680 v4 (14 núcleos/28 hilos, 32 GB RAM, sin gráfica integrada).
- **Decisión:**
  1. **Ya:** el PC principal es el «músculo» de IA local (Ollama en la GPU). Cerebro, todavía en el PC, lo usa como LLM por defecto.
  2. **Laboratorio (0 €):** el Xeon sirve para aprender Ubuntu Server + Docker y validar el despliegue de Cerebro como servidor. No se usa para inferencia por CPU (lenta frente a la GPU) ni como servidor 24/7 definitivo (consumo y ruido en reposo).
  3. **Definitivo:** mini PC de bajo consumo 24/7 (Cerebro, Syncthing, Immich, Jellyfin, Tailscale) que llama a Ollama en el PC principal cuando está encendido y recurre a Gemini de pago o a las reglas cuando está apagado.
- **Motivo:** la RX 6900 XT con 16 GB hace viable la IA local hoy, sin comprar nada. El Xeon no tiene Quick Sync, así que transcodificar en Jellyfin le costaría mucha CPU, y gasta bastante en reposo. Un mini PC con iGPU Intel resuelve el 24/7 con poco consumo.

## 2026-11-03 — Objetivo final: Ollama siempre disponible (opciones abiertas)
- **Requisito:** un equipo 24/7 con aceleración para modelos de 7-14B.
- **Opciones:**
  1. **Xeon + gráfica NVIDIA de segunda mano con 12 GB o más** (p. ej. RTX 3060 12 GB): reutiliza el Xeon y sus 32 GB; la NVIDIA aporta además NVENC para transcodificar en Jellyfin. Contras: consumo y ruido 24/7.
  2. **Pasar la RX 6900 XT al servidor** cuando se renueve la gráfica del PC de juego: coste 0 en GPU, 16 GB de VRAM.
  3. **Equipo eficiente con memoria unificada** (Mac mini con Apple Silicon o mini PC AMD con mucha memoria unificada): bajo consumo y silencioso, inversión inicial mayor.
- **Mientras tanto:** PC bajo demanda + Gemini de pago como respaldo.
- **Pendiente:** decidir cuando Cerebro fases 1-2 estén operativas, comparando el consumo real medido con un enchufe medidor.

## 2026-11-03 — Elegida la opción 3 (equipo eficiente con memoria unificada)
- **Decisión:** el servidor definitivo será un equipo de bajo consumo con memoria unificada. Falta elegir entre Mac mini (Apple Silicon) y mini PC AMD de gama alta con memoria unificada, y la cantidad de memoria.
- **Criterio de memoria:** 24-32 GB mínimo (modelo de 14B + embeddings + Immich + Jellyfin + Cerebro); 64 GB o más si se quieren modelos de más de 30B.
- **Impacto en la arquitectura:** si es Mac, Ollama se ejecuta nativo en macOS (Docker en Mac no accede a la GPU) y el resto de servicios en Docker; si es AMD con Linux, se mantiene «todo en Docker» con Ollama acelerado (verificar el soporte de su GPU integrada en Ollama antes de comprar).
- **Pendiente:** presupuesto del usuario; comparar precios actuales en el momento de la compra.

## 2026-11-03 — AMD + Linux
- **Decisión:** mini PC AMD con memoria unificada, Ubuntu Server LTS y todos los servicios en Docker (incluido Ollama con la GPU integrada).
- **Motivo:** libertad total para alojar todas las apps (las existentes y las que se creen), Linux nativo y la arquitectura ya diseñada, sin excepciones.
- **Antes de comprar:** (1) confirmar en la documentación de Ollama que acelera la GPU integrada del modelo elegido en Linux; (2) memoria mínima de 32 GB, recomendable 64 GB por el número de servicios previstos (normalmente va soldada: no se amplía); (3) dos ranuras M.2 o la posibilidad de un disco externo USB 3.2/USB4 para el contenido de Jellyfin y las copias de seguridad; (4) red de 2,5 GbE.

## 2026-11-03 — Homelab en rack con NAS (planteamiento)
- **Idea del usuario:** rack con NAS.
- **Propuesta:** separar cómputo y almacenamiento en un **rack de 10"** (compacto, apto para escritorio o estantería):
  - **Cómputo:** mini PC AMD (Cerebro, Ollama, apps en Docker).
  - **Almacenamiento (NAS):** 2-4 discos en espejo (RAID1) o RAIDZ1, con NAS comercial o casero (TrueNAS/Unraid). Comparte el contenido de Jellyfin, Immich y las copias por la red.
  - **Red:** switch de 2,5 GbE + panel de parcheo.
  - **SAI** (sistema de alimentación ininterrumpida): obligatorio con NAS, para evitar corrupción de datos en un corte de luz.
- **19"** solo si se van a montar servidores de rack de verdad (más ruido, más fondo, más consumo).
- **Regla:** el NAS no es una copia de seguridad. Se mantiene la 3-2-1 (NAS + disco externo + copia cifrada fuera de casa).
- **Orden de compra:** mini PC → discos/NAS → SAI → switch → rack (el rack es mobiliario: lo último).
- **Pendiente:** decidir entre NAS comercial y casero, capacidad necesaria (TB) y presupuesto total.