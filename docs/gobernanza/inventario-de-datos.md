# Inventario de datos

No se puede gobernar lo que no se sabe que se tiene. Una fila por cada dato que el sistema guarda, recibe o envía a un tercero, incluido el proveedor del modelo de IA.

| Dato | ¿Personal? | Categoría (Ley 8968, art. 9) | De dónde viene | Dónde se guarda | ¿Sale a un tercero? ¿A quién? | Cuánto se conserva | Quién puede verlo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Correo electrónico institucional | Sí | Acceso restringido | Formulario de registro y login (`src/pages/Login.jsx`) | Base de datos del servidor (`server/index.js`) | No | Mientras la cuenta de empleado esté activa | El usuario y el administrador |
| Contraseña protegida con hash | Sí | Acceso restringido | Formulario de registro y login (`src/pages/Login.jsx`) | Base de datos del servidor (`server/index.js`, cifrado con `bcryptjs`) | No | Mientras la cuenta esté activa | Nadie (solo verificación interna del hash) |
| Nombre de la mascota y estado lúdico | No | No aplica | Interfaz del juego (`src/features/game/`) | Base de datos del servidor y `localStorage` local | No | Permanente mientras exista la cuenta | El usuario asignado |
| Registro de pausas activas (XP, fecha y ejercicio) | No | No aplica | Verificación de pausa (`src/features/pauses/`) | Base de datos del backend (`server/index.js`) | No | Duración del periodo anual corporativo | El empleado y métricas consolidadas de RRHH |
| Preguntas en el chat de soporte institucional | No | No aplica | Widget de chat flotante (`src/features/chat/`) | Memoria de ventana en n8n durante la sesión | Sí: Google Gemini a través del webhook de n8n para generar respuesta | Solo mientras dure la sesión de la pestaña | El usuario en su sesión actual |
| Fotogramas de video de la cámara web | Sí | Acceso restringido | Cámara web del usuario al realizar el ejercicio | Memoria RAM del navegador local | No: procesamiento 100% en cliente con MoveNet | Cero segundos (se descarta tras inferir la pose) | Únicamente el usuario en su pantalla en vivo |

## Lo que NO recolectamos

- Imágenes fijas o transmisiones de video en servidores: La detección de postura mediante MoveNet corre íntegramente en el navegador del usuario (`src/services/poseService.js`). Ninguna imagen o fotograma sale del equipo ni se almacena en backend para resguardar la privacidad del espacio laboral.
- Datos de salud o diagnósticos médicos (datos sensibles): La herramienta se enfoca estrictamente en pausas activas preventivas de bienestar ergonómico y no solicita patologías, historial clínico ni condición médica del empleado.
- Plantillas o vectores biométricos de identificación facial: El modelo de visión solo detecta coordenadas de articulaciones esqueléticas para verificar la postura; no extrae rasgos biométricos faciales ni identifica la identidad de la persona.
- Datos financieros, tarjetas bancarias o datos crediticios: El acceso a Paws & Pause es provisto corporativamente por C&R International para su personal, eliminando cualquier necesidad de pagos o cobros en la plataforma.

