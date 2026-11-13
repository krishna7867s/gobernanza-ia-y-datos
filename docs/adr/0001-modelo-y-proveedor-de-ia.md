# ADR-0001: Motor de recomendación de café en cliente y reglas de uso de herramientas de IA en el desarrollo

- Estado: Aceptado
- Fecha: 2026-11-13
- Decide: Krishna Nahiel Moya Cervantes, Propietaria y Líder de Proyecto

## Contexto

Café Alma & Grano necesita orientar a sus clientes en la elección de cafés de especialidad (variedades Geisha, Caturra, tuestes claros y medios) sin sobrecargar la infraestructura del sitio con servicios externos costosos ni exponer la privacidad de los usuarios. Además, para el diseño y construcción del portal se utilizaron herramientas de desarrollo asistidas por IA que requieren reglas claras de gobernanza de código.

## Decisión

Se adopta una arquitectura liviana, privada y ética:

1. **Recomendador de café en el cliente (Browser Engine):** El sistema de sugerencias se ejecuta íntegramente en el navegador web del usuario a través de lógica determinista inspirada en la rueda de sabores de la SCA (Specialty Coffee Association). No requiere llamadas a APIs de pago ni servidores externos, garantizando respuesta instantánea y privacidad total de la navegación.
2. **Herramientas de IA en el desarrollo:** Se emplearon asistentes de código (Antigravity e IA generativa) exclusivamente para la aceleración en maquetación visual accesible y estructuración semántica de componentes.
3. **Regla de autoría humana:** Todo código, término legal y estilo generado con apoyo de IA fue revisado, probado y validado manualmente por el equipo antes de publicarse en el repositorio oficial.

## Alternativas descartadas

- **Llamar a un LLM en la nube (OpenAI / Anthropic) por cada consulta de café:** Descartado por el costo recurrente injustificado, alta latencia de respuesta para el usuario y el riesgo de alucinación en notas de cata o ingredientes no disponibles en cocina.
- **Widgets de chat de terceros invasivos:** Descartados para preservar una estética limpia, acogedora y libre de rastreadores comerciales de publicidad.

## Consecuencias

Se obtiene un sitio web ultrarrápido, de costo operativo cero en computación en la nube para recomendaciones, y con máxima confiabilidad sobre el inventario real de la cafetería. Como contrapartida, las recomendaciones se limitan a los perfiles predefinidos en la carta de la temporada, requiriendo actualización manual al incorporar nuevos micro-lotes de café.

## Cómo se verifica

La implementación de la decisión se verifica en:
- `index.html`: función `recomendarCafe()`, que procesa los gustos localmente en el DOM sin realizar peticiones de red `fetch` a servidores externos.
- `index.html`: ausencia de scripts externos o SDKs de rastreo publicitario de terceros en las etiquetas `<head>`.
- Auditoría de red en las herramientas de desarrollo del navegador: 0 llamadas salientes a APIs externas durante el uso del recomendador.
