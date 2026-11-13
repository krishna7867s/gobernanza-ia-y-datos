# Registro de riesgos

Al menos tres riesgos, cada uno con quién sale afectado y una mitigación que ya exista o que tenga responsable. Guía: [OWASP Top 10 para aplicaciones con LLM](https://genai.owasp.org/llm-top-10/) y [OWASP Top 10 para aplicaciones agénticas](https://genai.owasp.org/resource/2025-12-09/owasp-top-10-for-agentic-applications-for-2026).

| # | Riesgo | Quién sale afectado | Probabilidad (B/M/A) | Impacto (B/M/A) | Mitigación | Estado | Responsable |
| --- | --- | --- | --- | --- | --- | --- | --- |
| R1 | Inyección directa de prompt (OWASP LLM01) en el chat para saltar directrices institucionales o extraer prompts del sistema | Colaboradores y la reputación institucional de C&R International | M | M | System prompt restrictivo en el agente de n8n que delimita el alcance temático estricto y bloquea la interpretación de instrucciones embebidas en la entrada del usuario | Hecho | Krishna Nahiel Moya Cervantes |
| R2 | Denegación de servicio y agotamiento de cuota de API por llamadas masivas al chat (OWASP LLM04) | Usuarios que pierden acceso al soporte y costos de API del proyecto | M | M | Limitación de tasa de peticiones mediante `express-rate-limit` (`chatLimiter` a 20 consultas por minuto) y degradación elegante si n8n no responde | Hecho | Krishna Nahiel Moya Cervantes |
| R3 | Fuga accidental de credenciales o tokens de sesión en logs de red o respuestas de error (OWASP LLM06) | Usuarios autenticados y seguridad integral del backend | B | A | Las llaves de API residen exclusivamente en el gestor seguro de n8n y en `.env`; el backend sanitiza las respuestas y omite cabeceras de autorización al invocar el webhook externo | Hecho | Krishna Nahiel Moya Cervantes |
| R4 | Falsos negativos o fallos de detección en MoveNet por condiciones de luz o limitaciones de cámara web | Empleados que intentan validar pausas activas | M | B | Disponibilidad permanente de la opción de verificación manual y aplazamiento sin penalización de puntaje en la mascota | Hecho | Krishna Nahiel Moya Cervantes |

