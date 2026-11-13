# ADR-0001: Modelos de IA seleccionados: TensorFlow MoveNet en cliente para postura y Google Gemini en n8n para soporte

- Estado: Aceptado
- Fecha: 2026-11-13
- Decide: Krishna Nahiel Moya Cervantes, Líder de Desarrollo y Gobernanza

## Contexto

El proyecto Paws & Pause requiere resolver dos necesidades técnicas distintas: guiar pausas ergonómicas mediante detección visual de movimiento en tiempo real con estricta privacidad, y atender consultas de usuarios sobre las políticas de bienestar institucional mediante lenguaje natural. Las restricciones críticas son: latencia ultra baja para el análisis de video sin saturar el ancho de banda corporativo, costo predecible y aislamiento absoluto de secretos de API respecto al frontend.

## Decisión

Se decide implementar una arquitectura híbrida de modelos de IA con propósitos bien diferenciados:

1. **Visión por computadora en cliente (MoveNet):** Se utiliza el modelo MoveNet SinglePose Lightning ejecutado localmente en el navegador mediante `@tensorflow/tfjs` y `@tensorflow-models/pose-detection` (`src/services/poseService.js`). La inferencia ocurre al 100% en la CPU/GPU del dispositivo del usuario, sin llamadas de red ni envío de video al backend.
2. **Chat institucional con LLM (Google Gemini vía n8n):** Para el asistente conversacional, se utiliza Google Gemini conectado a través de un flujo de n8n (`n8n/paws-chat-workflow.json`). La comunicación entre el frontend y el modelo se intermedia exclusivamente a través de `POST /api/chat` en `server/index.js`, que invoca el webhook seguro de n8n. La API key de Gemini reside únicamente en el gestor de credenciales cifrado de n8n.
3. **Herramientas de IA en el desarrollo:** Se emplearon asistentes de código (Antigravity y Copilot) para refactorización y generación de pruebas unitarias, bajo la regla estricta de validación manual de cada cambio antes de su integración.

## Alternativas descartadas

- **Procesamiento de video en servidor con APIs en la nube (AWS Rekognition / Google Cloud Video AI):** Descartado por el elevado costo por minuto de video, alta latencia en red y el riesgo severo para la privacidad de transmitir grabaciones de empleados a la nube.
- **Llamar al modelo de lenguaje directamente desde el frontend:** Descartado porque expondría la API key de Google Gemini en el código fuente del cliente web y facilitaría abusos de consumo.
- **Modelos LLM locales autocontenidos en Node.js (Ollama / Llama.cpp en backend):** Descartado debido a los excesivos requerimientos de memoria RAM y tarjeta gráfica en el servidor de desarrollo y despliegue.

## Consecuencias

Se obtiene privacidad por diseño en el módulo de cámara, inferencia en tiempo real sin costo de computación en la nube para el análisis postural, y un chat institucional desacoplado y protegido contra fuga de credenciales. Como consecuencia, el rendimiento del chat depende de la disponibilidad del servicio n8n, lo cual se mitiga mostrando un estado controlado de desconexión en el widget si el webhook no responde.

## Cómo se verifica

La implementación de los modelos y proveedores se verifica en:
- `paws-y-pause/package.json`: presencia de dependencias cliente `@tensorflow/tfjs` y `@tensorflow-models/pose-detection`.
- `paws-y-pause/src/services/poseService.js`: carga del estimador MoveNet directamente en el navegador del usuario.
- `paws-y-pause/n8n/paws-chat-workflow.json`: definición del nodo `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`.
- `paws-y-pause/server/index.js`: endpoint `POST /api/chat` que valida que la consulta se canalice al webhook `N8N_CHAT_URL` con rate limiting (`chatLimiter`).

