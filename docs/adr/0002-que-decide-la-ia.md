# ADR-0002: El recomendador sugiere cafés y maridajes, pero la compra y las reservas son 100% decisión humana

- Estado: Aceptado
- Fecha: 2026-11-13
- Decide: Krishna Nahiel Moya Cervantes, Propietaria y Líder de Proyecto

## Contexto

En el sitio web de Café Alma & Grano, los clientes buscan descubrir cafés de especialidad de Costa Rica según la hora del día y su perfil de sabor preferido. El sitio incorpora una herramienta interactiva ("Recomendador Barista") que guía al usuario hacia la bebida ideal. Para proteger la autonomía del consumidor y evitar cobros imprevistos o sesgos en el servicio, se requiere definir con precisión qué decide el sistema algorítmico y qué queda bajo control de las personas.

## Decisión

Se establece que el componente algorítmico opera únicamente como asistente consultivo y no vinculante:

1. **Recomendaciones de café y maridaje:** El sistema analiza las variables ingresadas por el cliente (momento del día, notas aromáticas deseadas) y devuelve una sugerencia de método de extracción (ej. V60, Chemex, espresso) con su repostería recomendada.
2. **Decisión de compra y consumo soberana del cliente:** La sugerencia nunca ejecuta una compra automática, no carga montos a tarjetas ni compromete al cliente. El usuario es libre de aceptar la sugerencia o pedir cualquier otro producto de la carta.
3. **Gestión de reservas y asignación de mesas:** La confirmación de mesas se basa estrictamente en la disponibilidad física del local. Ningún algoritmo filtra, descarta o discrimina clientes por edad, origen o frecuencia de consumo.
4. **Precios transparentes y sin discriminación dinámica:** Todos los precios son fijos, públicos y estandarizados en el menú, prohibiendo el aumento algorítmico de precios según el perfil del usuario.

## Alternativas descartadas

- **Pedidos y cargos automáticos por recomendación:** Descartado porque violaría la confianza del cliente y generaría fricciones por consumos no deseados.
- **Tarificación dinámica con IA según afluencia:** Descartada por atentar contra la transparencia y la equidad en el trato a los comensales habituales de la cafetería.

## Consecuencias

Se garantiza una experiencia gastronómica cálida, predecible y respetuosa de la autonomía del cliente. Como contrapartida técnica, la conversión comercial requiere la interacción manual del usuario en el formulario de reservas o en la barra, garantizando el consentimiento pleno.

## Cómo se verifica

La confirmación humana y la delimitación algorítmica se verifican en:
- `index.html`: el Recomendador Barista (`function recomendarCafe()`) únicamente actualiza el texto sugerido en pantalla sin enviar peticiones transaccionales de cobro.
- `index.html`: el formulario de reserva (`#reservaForm`) exige confirmación explícita del cliente y aceptación de términos antes de procesar la solicitud.
- Modal de Términos y Condiciones en el sitio: estipula expresamente que las sugerencias son informativas y no generan obligación contractual automática.
