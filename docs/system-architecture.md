## 🏗️ Arquitectura del Proyecto Indoor

### 📌 Enfoque Arquitectónico

Para el desarrollo del sistema de medición indoor estamos adoptando una **arquitectura modular basada en el patrón Cliente-Servidor con lógica Edge Computing**, lo que permite mantener una base sólida y extensible para futuras mejoras.

---

### ✅ Arquitectura seleccionada: Cliente-Servidor + Edge Computing

**Razones por las que fue elegida:**

- Es simple de implementar para un entorno de desarrollo local
- Se adapta bien al flujo físico-digital del proyecto (hardware + backend + UI)
- Permite tomar decisiones locales sin depender de la red
- Es escalable hacia arquitecturas más avanzadas como MQTT o microservicios

**Distribución de responsabilidades por capa:**

| Componente                | Rol principal                                                            |
| ------------------------- | ------------------------------------------------------------------------ |
| **Arduino**               | Lectura de sensores físicos, envía datos por puerto serial               |
| **Python (Raspberry Pi)** | Nodo de borde (edge): recibe datos, controla hardware, procesa y reenvía |
| **Node.js (API REST)**    | Core backend: recibe, valida y almacena datos en MongoDB                 |
| **React**                 | Dashboard: visualiza datos y permite interacciones remotas               |

---

### 🔧 Flujo general del sistema

```mermaid
flowchart TD
    A[Arduino] -->|Serial USB| B[Python (Raspberry Pi)]
    B -->|HTTP POST JSON| C[API REST (Node.js + Express)]
    C --> D[Base de Datos (MongoDB)]
    C --> E[Frontend React]
    E -->|HTTP GET| C
```

---

### 🧱 Arquitectura interna sugerida (Clean Architecture opcional)

Tanto para Node.js como para Python, se recomienda estructurar el código según el patrón de **Arquitectura Limpia (Clean Architecture)** o **Hexagonal**, lo que permite mantener un sistema desacoplado y testeable.

**Capas sugeridas:**

- `controllers/` → Controladores de entrada (routes en Node.js, handlers en Python)
- `usecases/` → Lógica de negocio o servicios de aplicación
- `repositories/` → Interfaces de acceso a datos (MongoDB, archivos, APIs externas)
- `entities/` → Estructuras centrales del dominio (por ejemplo: SensorData)

---

### ℹ️ Notas importantes

- Este enfoque es nuevo para el desarrollador. Python y arquitecturas como Clean Architecture son tecnologías en aprendizaje.
- Se documentará cada etapa del proceso para consolidar el conocimiento adquirido y facilitar futuras iteraciones.

---

### 📈 Futuras extensiones posibles

- Uso de MQTT para eventos en tiempo real
- Incorporación de dashboards avanzados (ej. Grafana, Plotly Dash)
- Notificaciones por correo o Telegram
- Control remoto de actuadores desde el frontend

---

Este enfoque modular y adaptable permite comenzar con una arquitectura simple pero preparada para escalar y evolucionar según las necesidades del sistema indoor.

