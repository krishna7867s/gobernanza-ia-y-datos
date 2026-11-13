# AGENTS.md — Café Alma & Grano

Reglas que cualquier agente de código (Claude Code, Codex, Copilot, Cursor) debe leer antes de tocar este repositorio. Si una regla no está aquí, el agente no la conoce.

## Qué es este proyecto

Café Alma & Grano es el sitio web oficial de una cafetería de especialidad y repostería artesanal en Costa Rica. Incluye menú interactivo de microlotes, recomendador sensorial de café para clientes, sistema de reservas de mesas y gobernanza de datos bajo la Ley N° 8968.

## Antes de escribir código

- Leer `docs/adr/` y `docs/gobernanza/`. Si un cambio contradice un ADR aceptado, no se hace: se propone un ADR nuevo.
- Comprobar que cualquier modificación visual preserve la estética cálida, humana y artesanal del café, sin estilos prefabricados ni apariencias sintéticas de IA.

## Datos

- Nunca escribir datos personales de clientes (nombres, correos, teléfonos de reservas) en logs ni en commits de Git.
- Nunca usar datos reales en pruebas de reservas: utilizar únicamente correos de prueba de formato `@ejemplo.com`.
- El recomendador de café procesa las preferencias en la memoria volátil del navegador y nunca las envía a servicios externos.

## IA y algoritmos en el producto

- El recomendador sensorial sugiere cafés y maridajes como guía amistosa; **la decisión de compra es 100% humana**. Nunca se generan cobros ni pedidos obligatorios de manera automática.
- Los precios del menú son públicos y fijos: queda terminantemente prohibida cualquier tarificación dinámica algorítmica.

## Secretos

- No versionar credenciales de correo ni accesos administrativos en el frontend ni en archivos rastreados por Git.

## Límites del agente

- No borrar archivos de documentación, hojas de estilo ni modales legales sin autorización explícita.
- Ante la duda sobre reglas de privacidad, seguridad o gobernanza, no actuar: preguntar a la responsable.

## Reglas propias de este proyecto

- Las recomendaciones de café deben ejecutarse exclusivamente en el navegador (`index.html`), prohibiendo llamadas a APIs externas de pago o rastreadores publicitarios.
- El formulario de reservas nunca debe solicitar datos de tarjetas bancarias ni números CVV; todos los cobros de consumo se realizan presencialmente en el datáfono físico del local.
- La estética visual debe mantener la identidad acogedora de la cafetería con tipografía serif editorial, tonos café, crema y terracota (`#231714`, `#8c5d43`, `#c47b59`, `#faf7f2`).
- Los modales de Términos y Condiciones y Política de Privacidad (Ley 8968) deben mantenerse siempre funcionales y enlazados en el pie de página y en el formulario de reservas.
- Toda nueva función que recolecte datos de contacto debe actualizarse primero en `docs/gobernanza/inventario-de-datos.md` respetando la clasificación legal costarricense.
