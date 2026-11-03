# Estado del Proyecto · TikTok Radar

Actualizado: 2026-11-03.

## Resumen Ejecutivo

TikTok Radar está 100% operativo y listo para producción como noticiero vertical automatizado:
* **Escáner:** `tools/news_radar.py` monitorea Xataka, BBC Mundo y El País en tiempo real.
* **Pipeline Autónomo:** `tools/pipeline_autonomo.py` selecciona noticias, redacta guiones para 61–65 segundos monetizables, genera 13 prompts para Google Flow y sintetiza la voz del locutor con Edge-TTS.
* **Entrega Inicial Realizada:** `entregas/2026-11-03_AUTONOMO/` con audio de **62.69 segundos** (`LOCUCION_NOTICIERO_62S.mp3`) y desglose de 13 planos listo para pegar en Flow.
* **Infraestructura AWS:** Script de despliegue `tools/instalar_servidor_aws.sh` y guía en `GUIA_DESPLIEGUE_AWS_AUTONOMO.md`.
