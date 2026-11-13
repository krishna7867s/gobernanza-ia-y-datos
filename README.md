# Café Alma & Grano — Especialidad y Repostería Artesanal

Sitio web oficial de **Café Alma & Grano**, una cafetería de especialidad y tostaduría de micro-lotes en San José, Costa Rica.

El portal ofrece una experiencia digital cálida y artesanal para los amantes del buen café, incorporando un recomendador sensorial, gestión transparente de reservas de mesas y un paquete completo de gobernanza tecnológica y protección de datos personales conforme a la Ley N° 8968.

---

## Características Principales

* ☕ **Carta Seleccionada de Cafés:** Granos de origen costarricense (Tarrazú, Naranjo), métodos de filtrado manual (V60, Chemex) y repostería horneada a diario.
* 🌿 **Recomendador Barista:** Guía interactiva que sugiere cafés y maridajes según el momento del día y las notas aromáticas preferidas del cliente.
* 📅 **Sistema de Reservas:** Formulario accesible con confirmación y casilla de consentimiento informado.
* 📜 **Términos y Condiciones y Privacidad (Ley 8968):** Modales legales claros, comprensibles y sin letra pequeña sobre el uso de datos.
* 🛡️ **Governance Pack Integrado:** Decisiones de arquitectura (ADRs), inventario de datos y registro de riesgos alineados con las mejores prácticas de gobernanza tecnológica.

---

## Estructura del Proyecto

```text
├── index.html                           # Sitio web completo con menú, recomendador y modales legales
├── AGENTS.md                            # Reglas de desarrollo y límites de IA para el repositorio
├── .github/
│   ├── governance-pack/
│   │   └── verificar-pack.mjs           # Script de validación de estándares del Governance Pack
│   ├── pull_request_template.md         # Plantilla formal de revisión de cambios
│   └── workflows/
│       └── governance-pack.yml          # Flujo de CI automatizado para Pull Requests
└── docs/
    ├── adr/
    │   ├── 0001-modelo-y-proveedor-de-ia.md   # Modelo de recomendación en cliente y uso de herramientas
    │   ├── 0002-que-decide-la-ia.md           # Autonomía humana vs sugerencias algorítmicas
    │   ├── 0003-donde-viven-los-datos.md      # Residencia local de reservas y derechos ARCO
    │   └── README.md
    └── gobernanza/
        ├── inventario-de-datos.md             # Inventario de datos según Ley 8968 (art. 9)
        └── registro-de-riesgos.md             # Matriz de riesgos mitigados
```

---

## Ejecución y Verificación

Para abrir el sitio web en tu navegador:
Abre el archivo `index.html` con cualquier navegador web (Chrome, Edge, Firefox).

Para correr el verificador de gobernanza:
```bash
node .github/governance-pack/verificar-pack.mjs
```

---

**Responsable del Proyecto y Datos:** Krishna Nahiel Moya Cervantes
