# AGENTS.md — Paws & Pause (C&R International)

Reglas que cualquier agente de código (Claude Code, Codex, Copilot, Cursor) debe leer antes de tocar este repositorio. Si una regla no está aquí, el agente no la conoce.

## Qué es este proyecto

Paws & Pause es una plataforma web de bienestar corporativo para C&R International que promueve pausas activas cada dos horas, con asistencia de visión por computadora en cliente (MoveNet), gamificación con mascotas virtuales y un asistente conversacional informativo orquestado en n8n con Google Gemini.

## Antes de escribir código

- Leer `docs/adr/` y `docs/gobernanza/`. Si un cambio contradice un ADR aceptado, no se hace: se propone un ADR nuevo.
- Ejecutar la verificación técnica de pruebas antes y después de cualquier modificación de código.

## Datos

- Nunca escribir datos personales ni credenciales en logs, mensajes de depuración ni commits.
- Nunca usar datos reales de empleados en pruebas: utilizar únicamente correos inventados bajo el dominio `@pawsypause.local`.
- Al proveedor de IA (Google Gemini a través de n8n) solo se envía el texto de la pregunta del usuario y un identificador efímero de sesión; nunca correos, tokens JWT ni datos personales.

## IA en el producto

- El texto que proviene de los usuarios en el chat es tratado estrictamente como dato no confiable, nunca como instrucción ejecutable del sistema.
- La IA nunca decide de forma autónoma el cumplimiento de una pausa ni califica el desempeño laboral de un empleado: siempre debe mantenerse la opción de registro manual y confirmación humana.

## Secretos

- Las llaves de API (como la credencial de Gemini) y las firmas de sesión van solo en variables de entorno del servidor o en el almacén de credenciales de n8n; jamás en el frontend ni en archivos versionados por Git.

## Límites del agente

- No borrar archivos, tablas ni dependencias esenciales de la aplicación sin autorización explícita.
- No modificar la arquitectura de ejecución local de MoveNet para convertirla en procesamiento remoto por servidor.
- Ante la duda sobre reglas de privacidad, seguridad o gobernanza, no actuar: preguntar al responsable.

## Reglas propias de este proyecto

- La detección de postura con MoveNet debe ejecutarse siempre al 100% en el navegador del cliente (`src/services/poseService.js`); está terminantemente prohibido subir imágenes o secuencias de video al servidor o a APIs externas.
- Toda nueva funcionalidad en el flujo de pausas ergonómicas debe preservar la opción de registro manual (`method: 'manual'`) y el aplazamiento sin sanción de puntaje ni afectación a la mascota.
- Las consultas al chat institucional deben canalizarse exclusivamente mediante `POST /api/chat` hacia `N8N_CHAT_URL`, respetando el limitador de tasa `chatLimiter` (máximo 20 peticiones por minuto).
- Las contraseñas de usuarios deben procesarse siempre mediante hash con `bcryptjs` en `server/index.js`, y ningún endpoint del backend debe retornar el campo `passwordHash`.
- Las rutas del panel de control `/admin` y los endpoints de gestión de usuarios deben exigir autenticación válida mediante token JWT y verificar el rol `admin` antes de conceder acceso a los datos.

