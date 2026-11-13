# ADR-0003: Residencia local de reservas, minimización en cliente y cumplimiento de la Ley 8968

- Estado: Aceptado
- Fecha: 2026-11-13
- Decide: Krishna Nahiel Moya Cervantes, Propietaria y Líder de Proyecto

## Contexto

El sitio web de Café Alma & Grano recolecta datos mínimos de personas para la gestión de reservas de mesas y comunicación con los comensales. Conforme a la Ley N° 8968 de Protección de la Persona frente al Tratamiento de sus Datos Personales (Costa Rica), es obligatorio definir dónde residen los datos, los límites de conservación y los procedimientos para garantizar los derechos de acceso, rectificación y supresión.

## Decisión

Se adopta una política estricta de minimización y protección de la información:

1. **Datos de reservas (nombre, correo y fecha):** Se custodian en el servidor local de reservas de la cafetería con acceso protegido por credenciales administrativas. Solo el personal de recepción y anfitrionía puede consultar la lista de comensales del día.
2. **Cero transferencia a terceros:** Ningún dato personal se vende, comparte ni transmite a redes de publicidad, intermediarios de reservas ni plataformas de analítica invasiva.
3. **Almacenamiento en el dispositivo del cliente:** Las preferencias seleccionadas en el recomendador de café se guardan únicamente en la memoria volátil de la sesión del navegador y no se persisten en base de datos.
4. **Política de retención y purga:** Los registros de reservas se conservan por un plazo máximo de 90 días naturales para resolución de consultas o cancelaciones, tras lo cual se eliminan de forma automatizada y permanente.
5. **Ejercicio de derechos ARCO:** Los comensales pueden solicitar en cualquier momento la consulta o borrado anticipado de sus datos mediante el correo oficial `privacidad@almaygrano.cr`.

## Alternativas descartadas

- **Externalizar reservas en plataformas masivas de terceros con venta de datos:** Descartado para mantener una relación directa y honesta con la comunidad de clientes, sin exponer sus correos a spam promocional.
- **Guardar información financiera de clientes:** Descartado por principio de minimización de riesgos: al cobrar presencialmente en el local, el sitio web se mantiene libre de contingencias de pago con tarjeta.

## Consecuencias

Se garantiza el cumplimiento cabal de la legislación costarricense de protección de datos personales, transmitiendo confianza y tranquilidad a los comensales. Como contrapartida, las reservas requieren confirmación de mesa mediante correo electrónico tradicional en lugar de cobro por adelantado.

## Cómo se verifica

La política de almacenamiento se verifica en:
- `index.html`: el formulario de reserva (`#reservaForm`) incluye casilla obligatoria de consentimiento informado con enlace visible a la política de privacidad.
- Modal de Privacidad en `index.html`: detalla los derechos ARCO y el contacto de la persona responsable de la base de datos.
- Inspección del código: ausencia de cookies de rastreo publicitario de terceros (Meta Pixel, Google Ads o trackers externos).
