# Reglas del Agente · TikTok Radar (Servidor AWS y Desarrollo)

Antes de trabajar en este repositorio, lee `ESTADO_PROYECTO.md` y `SUPERVISOR_SERVIDOR_AWS.md` para retomar el contexto completo del sistema autónomo.

## 1. Propósito del Repositorio (`TIKTOK-NEWS`)

Este repositorio es el motor autónomo de producción del **Noticiero 3D de Alto Impacto** optimizado para monetización en TikTok (**> 60 segundos**, objetivo **61 a 65 segundos**).

Consta de 3 módulos principales en `tools/`:
1. `pipeline_autonomo.py` (apoyado en `news_radar.py`): Rastrea **Xataka**, **BBC Mundo** y **El País**, redacta el guión de 61–65 s, genera los 13 prompts en estilo **Animación 3D Estilizada** (`prompt` + `fallback_prompt`) y sintetiza la locución con `edge-tts` (`es-MX-JorgeNeural`).
2. `flow_generator.py`: Inyector autónomo con Playwright sobre el perfil autenticado `~/flow-profile`. Posee auto-curación de bloqueos de Chrome (`SingletonLock`), cierre de popups (`Escape` x3), auto-aprobación del agente de Flow, reintento con `fallback_prompt` ante bloqueos de política y checkpointing plano a plano (`SH01.mp4`..`SH13.mp4`).
3. `ensamblador_final.py`: Editor algorítmico NLE sobre FFmpeg Filtergraph + ASS Vector Engine. Aplica movimiento de cámara 24 fps, transiciones broadcast (`xfade`), subtítulos Kinetic palabra por palabra con resaltado cromático y masterización de audio multicapa a **`-14.8 LUFS`**.
4. `ejecutar_todo.py`: Orquestador maestro de 1 solo comando.

## 2. Reglas de Supervisión en el Servidor AWS

- **No pedir micro-confirmaciones:** Ejecutar el diagnóstico, reparar cualquier bloqueo y entregar el resultado verificado (`PROTOCOLO_APROBACION_RAPIDA.md`).
- **Verificación de Vídeo Final:** Todo máster (`NOTICIERO_FINAL_62S.mp4`) debe verificarse con `ffprobe` / `ffmpeg` confirmando:
  - Duración `> 60.0 s` (estándar 61–65 s).
  - Resolución `1080x1920` a `24 fps`.
  - Sonoridad integrada en torno a `-14.8 LUFS`.
- **Cuidado de la Sesión `~/flow-profile`:** Nunca borrar las cookies de `~/flow-profile`. Solo limpiar archivos `SingletonLock`, `SingletonCookie` y `SingletonSocket` cuando no haya instancias activas de Chrome.
