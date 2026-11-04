# Estado del Proyecto · TikTok Radar (Servidor AWS Autónomo)

Actualizado: 2026-11-04.

## Bot Propio de WhatsApp Web y Supervisión Permanente en AWS (`TIKTOK-NEWS`) · 2026-11-04

1. **Bot Propio Nativo 24/7:**
   - Desplegado en `whatsapp_bot/bot.js` bajo servicio systemd `tiktok-whatsapp-bot.service`.
   - Conexión directa sin intermediarios mediante WhatsApp Web (`whatsapp-web.js`) en Google Chrome headless.
   - Enlazado bidireccionalmente con el agente Antigravity (`agy --dangerously-skip-permissions`) en AWS para responder dudas y recibir comandos (`!estado`, `!generar`).
   - Manual completo y pasos de vinculación en [`WHATSAPP_BOT_SUPERVISOR.md`](WHATSAPP_BOT_SUPERVISOR.md).

2. **Primer Noticiero 3D Completado al 100% en Servidor AWS:**
   - Entrega final: `entregas/2026-11-03_AUTONOMO/NOTICIERO_FINAL_62S.mp4` (61.2 s, 1080×1920, 24 fps, -15.0 LUFS, subtítulos Kinetic ASS).
   - Generado íntegramente con los 13 planos de Google Flow y ensamblado en FFmpeg.

3. **Estado de Servidor:**
   - Servidor en reposo óptimo (RAM disponible ~6.6 GiB, disco al 24%).
   - Para vincular WhatsApp: ejecutar `bash ~/TIKTOK-NEWS/whatsapp_bot/ver_qr.sh` en AWS y escanear el QR desde el celular.

## Estado de Módulos Operativos en `tools/`:

1. **Conexión y Sesión en Servidor AWS (`ubuntu@3.142.230.147`):**
   - Sesión de Google Flow autenticada y verificada con éxito en `~/flow-profile` (`CONEXIÓN EXITOSA` comprobada con `test_flow_session.py`).
2. **Módulos Operativos en `tools/`:**
   - [`tools/news_radar.py`](tools/news_radar.py): Escáner RSS en tiempo real (Xataka, BBC Mundo, El País Tecnología).
   - [`tools/pipeline_autonomo.py`](tools/pipeline_autonomo.py): Selección automática de noticia de impacto, guión de **61–65 segundos** (>60 s para monetización en TikTok), 13 prompts 3D estilizados con `fallback_prompt` anti-bloqueo y síntesis de voz neuronal (`es-MX-JorgeNeural`) con verificación automática de duración `>= 61.0 s`.
   - [`tools/flow_generator.py`](tools/flow_generator.py): Inyector autónomo de Google Flow (Playwright Headless) con auto-curación (`SingletonLock` cleanup, cierre de popups con `Escape` x3, auto-aprobación del agente de Flow, reintento automático con `fallback_prompt` ante bloqueos de política, doble vía de descarga UI + Red y checkpointing de `SH01.mp4` a `SH13.mp4`).
   - [`tools/ensamblador_final.py`](tools/ensamblador_final.py): Editor de vídeo algorítmico NLE para Linux sobre FFmpeg Filtergraph + ASS Vector Engine:
     - Movimiento de cámara 24 fps (Ken Burns + vibración de cabina en planos de tensión `SH04`–`SH09`).
     - Transiciones broadcast reales (`xfade`: `fadeblack`, `smoothleft`, `dissolve`, `circleopen`, `wipeleft`).
     - Subtítulos Kinetic palabra por palabra (`.ass`) con pop-in elástico, resaltado automático en Amarillo/Cian y rótulo superior `🔴 ÚLTIMA HORA · NOTICIERO 3D`.
     - Diseño sonoro multicapa (voz ecualizada + cama de tensión sintética + SFX *whooshes* en cada transición) masterizado a **`-14.8 LUFS`**.
   - [`tools/ejecutar_todo.py`](tools/ejecutar_todo.py): Orquestador maestro de 1 solo comando (`python3 tools/ejecutar_todo.py`).
3. **Manual de Supervisión:**
   - Documentado en [`SUPERVISOR_SERVIDOR_AWS.md`](SUPERVISOR_SERVIDOR_AWS.md) y [`AGENTS.md`](AGENTS.md) para que tanto el usuario como cualquier agente ejecutado dentro del servidor AWS supervisen todo el flujo.
