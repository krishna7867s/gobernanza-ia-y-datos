# ADR-0002: La IA asiste en la detección de pausas y consultas, pero la confirmación y las decisiones laborales son 100% humanas

- Estado: Aceptado
- Fecha: 2026-11-13
- Decide: Krishna Nahiel Moya Cervantes, Líder de Desarrollo y Gobernanza

## Contexto

En Paws & Pause (C&R International), los empleados de oficina realizan pausas activas periódicas frente a su computadora para prevenir el sedentarismo y la fatiga muscular. La aplicación incorpora dos componentes inteligentes: un modelo de visión por computadora para asistir en la verificación de posturas ergonómicas y un agente conversacional para resolver dudas sobre el programa y la empresa. Existía la necesidad de delimitar qué puede decidir la tecnología para evitar discriminación, sanciones injustas o invasión indebida a la privacidad del trabajador.

## Decisión

Se establece que la inteligencia artificial opera únicamente en calidad de asistente informativo y de retroalimentación en tiempo real:

1. **Detección de posturas (MoveNet):** El modelo evalúa las coordenadas de articulaciones en el navegador para sugerir que la pose es correcta. Sin embargo, la IA **nunca confirma automáticamente una pausa ni descarta a un usuario**. La persona siempre tiene el control final de disparar la verificación o bien seleccionar el registro manual sin cámara (`method: 'manual'`).
2. **Impacto laboral cero:** Los resultados de las pausas activas, el nivel de la mascota virtual y el uso de la cámara se mantienen con carácter lúdico y motivacional. Ningún algoritmo de IA clasifica, califica, sanciona ni condiciona la continuidad laboral ni las evaluaciones de desempeño del trabajador.
3. **Agente conversacional (Gemini en n8n):** El chat flotante solo responde preguntas institucionales y de uso del sistema basadas en un prompt de sistema acotado. No ejecuta transacciones, no aprueba solicitudes de vacaciones ni modifica datos de usuarios.

## Alternativas descartadas

- **Validación automática obligatoria por visión artificial:** Descartada porque forzar a la IA a decidir si un empleado cumplió su deber laboral generaría falsos negativos por mala iluminación, cámaras de baja resolución o condiciones físicas particulares, además de violentar la autonomía del usuario.
- **Calificación algorítmica de productividad o salud:** Descartada rotundamente porque delegar diagnósticos o evaluaciones laborales en modelos automatizados viola los principios éticos y regulatorios de protección al trabajador.

## Consecuencias

Se garantiza que el empleado mantiene el control y la tranquilidad de que la herramienta es un apoyo ergonómico y no un instrumento de vigilancia patronal. Como consecuencia técnica, se debe mantener y dar soporte al flujo de registro manual alternativo (`method: 'manual'`), el cual otorga puntaje sin exigir cámara web, reduciendo fricciones de accesibilidad.

## Cómo se verifica

La separación de responsabilidades y la confirmación humana se verifican en:
- `src/features/pauses/StretchCheck.jsx`: la interfaz requiere una acción explícita del usuario para completar la pausa y ofrece un botón permanente de "Registrar manualmente".
- `server/index.js`: el endpoint `POST /api/pauses` valida que el registro provenga de una acción confirmada por el usuario (indicando método `camera` o `manual`).
- `tests/privacyAndCompliance.test.mjs`: suite de pruebas automatizadas que valida la disponibilidad del modo manual y la ausencia de penalizaciones por no usar cámara.

