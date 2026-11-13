# Inventario de datos

No se puede gobernar lo que no se sabe que se tiene. Una fila por cada dato que el sistema guarda, recibe o envía a un tercero, incluido el proveedor del modelo de IA.

| Dato | ¿Personal? | Categoría (Ley 8968, art. 9) | De dónde viene | Dónde se guarda | ¿Sale a un tercero? ¿A quién? | Cuánto se conserva | Quién puede verlo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Nombre y apellidos del cliente | Sí | Acceso restringido | Formulario de reservas de mesa (`index.html#reservas`) | Base de datos local de reservas del café | No | 90 días tras la fecha de reserva | Personal de anfitrionía y administración |
| Correo electrónico del cliente | Sí | Acceso restringido | Formulario de reservas (`index.html#reservas`) | Registro de confirmación de reservas | No: exclusivo para enviar comprobante de mesa | 90 días tras la fecha de reserva | Administración de reservas |
| Fecha, hora y número de comensales | No | No aplica | Formulario de reservas | Calendario interno de mesas | No | 6 meses para estadísticas de aforo | Equipo de servicio y baristas |
| Preferencias de sabor y momento de consumo | No | No aplica | Recomendador interactivo Barista Alma | Memoria volátil de sesión del navegador del cliente | No | Se descarta al cerrar la pestaña | El usuario en su pantalla en tiempo real |
| Consultas y sugerencias de clientes | Sí | Acceso restringido | Buzón de contacto (`contacto@almaygrano.cr`) | Correo de atención al cliente | No | 1 año para control de calidad | Gerencia de Café Alma & Grano |

## Lo que NO recolectamos

- Datos de tarjetas bancarias, números de tarjeta o códigos CVV: Las reservas en Café Alma & Grano son 100% gratuitas. Los pagos por consumo se realizan de manera física y presencial en el datáfono del local comercial.
- Datos de salud médica o datos sensibles (art. 9, Ley 8968): No solicitamos diagnósticos médicos, historial de alergias obligatorio ni datos biomédicos. Las sugerencias de descafeinado o leche vegetal se manejan por elección voluntaria del cliente.
- Geolocalización GPS en tiempo real: La página web no rastrea coordenadas de ubicación ni monitorea al usuario fuera de su visita al sitio web.
- Imágenes o grabaciones faciales: El recomendador de café se basa en selecciones directas de menú y nunca utiliza cámaras web ni biometría visual.
