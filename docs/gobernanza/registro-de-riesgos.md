# Registro de riesgos

Al menos tres riesgos, cada uno con quién sale afectado y una mitigación que ya exista o que tenga responsable. Guía: [OWASP Top 10 para aplicaciones con LLM](https://genai.owasp.org/llm-top-10/) y [OWASP Top 10 para aplicaciones agénticas](https://genai.owasp.org/resource/2025-12-09/owasp-top-10-for-agentic-applications-for-2026).

| # | Riesgo | Quién sale afectado | Probabilidad (B/M/A) | Impacto (B/M/A) | Mitigación | Estado | Responsable |
| --- | --- | --- | --- | --- | --- | --- | --- |
| R1 | Exposición no autorizada de correos o nombres de comensales en el registro de reservas | Clientes registrados y la reputación comercial de Café Alma & Grano | B | M | Almacenamiento local con acceso exclusivo para personal autorizado, principio de mínimo privilegio y purga automática cada 90 días | Hecho | Krishna Nahiel Moya Cervantes |
| R2 | Inexactitud o falta de claridad en ingredientes o alérgenos en el recomendador de café | Comensales con intolerancias alimentarias o alergias | M | M | Advertencia explícita en el recomendador y en el menú de que toda bebida láctea ofrece alternativa vegetal (avena o almendra) bajo confirmación presencial del barista | Hecho | Krishna Nahiel Moya Cervantes |
| R3 | Saturación por reservas falsas o spam que bloquee el aforo real de mesas | Clientes reales que buscan reservar y personal de sala | M | B | Validación obligatoria de campos en el formulario, confirmación por correo y verificación telefónica para grupos mayores a 4 personas | Hecho | Krishna Nahiel Moya Cervantes |
| R4 | Falta de claridad en el consentimiento o derechos de privacidad del cliente (Ley 8968) | Usuarios que desconfíen del uso de su correo electrónico | B | M | Enlaces directos y modales emergentes con Términos y Condiciones y Política de Privacidad claros en el formulario de reserva | Hecho | Krishna Nahiel Moya Cervantes |
