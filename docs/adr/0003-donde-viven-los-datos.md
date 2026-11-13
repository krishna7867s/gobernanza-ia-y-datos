# ADR-0003: Almacenamiento local seguro, inferencia efímera en cliente y aislamiento de datos enviados a terceros

- Estado: Aceptado
- Fecha: 2026-11-13
- Decide: Krishna Nahiel Moya Cervantes, Líder de Desarrollo y Gobernanza

## Contexto

Conforme a la Ley 8968 de Protección de la Persona frente al Tratamiento de sus Datos Personales (Costa Rica), Paws & Pause debe garantizar que los datos recolectados se manejen con fines proporcionales, seguros y con delimitación estricta de responsabilidades. El sistema maneja credenciales de acceso, historiales de hábitos saludables y un chat conectado a servicios de terceros, requiriendo claridad sobre la residencia y el ciclo de vida de la información.

## Decisión

Se adopta una política de minimización de datos y almacenamiento con fronteras claras:

1. **Datos de cuenta y autenticación:** Se custodian en el servidor backend (`server/index.js`). Las contraseñas se almacenan únicamente como hashes criptográficos irreversibles mediante `bcryptjs`. El acceso a recursos protegidos se controla mediante tokens JWT con expiración definida y control de acceso basado en roles (`empleado` y `admin`).
2. **Preferencias locales del cliente:** La configuración de música lo-fi, volumen, tema visual y la hora del próximo recordatorio se almacenan exclusivamente en el `localStorage` del navegador del usuario. El usuario puede borrarlos en cualquier momento limpiando los datos de su navegador.
3. **Imágenes de cámara y postura:** Tienen un ciclo de vida de milisegundos en la memoria RAM del navegador. No se escriben en disco, no se almacenan en caché persistente y no se transfieren a ninguna red ni base de datos.
4. **Datos transferidos a terceros:** El único servicio externo que procesa datos es Google Gemini (mediante el agente de n8n). Se establece la regla estricta de que **únicamente se transmite el texto de la consulta del usuario** y un identificador de sesión temporal. Está prohibido por arquitectura enviar tokens de autorización, correos, nombres o métricas de empleados a n8n o a Google.
5. **Derecho de supresión y retención:** Los datos de cuenta se mantienen mientras exista la relación laboral con C&R International. Ante una solicitud de supresión de datos (derecho ARCO, Ley 8968), el administrador puede purgar el usuario y su histórico lúdico desde la consola de administración (`src/features/dashboard/`).

## Alternativas descartadas

- **Subir capturas de video a almacenamiento en la nube (S3 / Cloud Storage):** Descartado por representar una intromisión innecesaria a la intimidad del usuario y generar contingencias legales bajo la Ley 8968.
- **Guardar el historial completo de conversaciones del chat en base de datos central:** Descartado para cumplir con el principio de minimización de datos, dado que las consultas informativas son de autoservicio y no requieren auditoría retroactiva con identidad de usuario.

## Consecuencias

Se cumple rigurosamente con los principios de autodeterminación informativa y proporcionalidad de la Ley 8968. Se reduce la superficie de ataque y el costo de almacenamiento en la infraestructura. Como compensación, el chat no ofrece persistencia histórica entre diferentes sesiones del navegador, lo cual es deseable desde la perspectiva de privacidad.

## Cómo se verifica

La política de almacenamiento y aislamiento se verifica en:
- `server/index.js`: middleware de sanitización de payload y exclusión de headers sensibles antes de invocar `N8N_CHAT_URL`.
- `tests/privacyAndCompliance.test.mjs`: suite de pruebas que valida que ninguna petición de ejercicio transmita archivos multimedia y que los endpoints no expongan contraseñas ni datos sensibles en texto plano.
- `tests/httpClientSanitization.test.mjs`: prueba automatizada que verifica que la llamada al chat no filtre tokens JWT ni correos de usuario.

