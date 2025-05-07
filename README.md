# 🌱 Sistema de Medición Indoor

Este repositorio contiene un sistema modular de monitoreo ambiental indoor basado en una arquitectura REST + MQTT, con procesamiento en el borde (Edge Computing) y visualización en tiempo real. El sistema permite medir variables desde sensores conectados a un ESP32, procesarlas en una Raspberry Pi con Python, almacenarlas en una base de datos MongoDB mediante una API Node.js y mostrarlas en un dashboard React + Redux.

---

## 📚 Documentación principal

La documentación detallada se encuentra organizada en la carpeta `/docs` y cubre todas las etapas del proyecto:

* [Visión general y arquitectura REST+MQTT](docs/architecure-system.md)
* [Instrucciones del proyecto y metodología Git](docs/project-instructions.md)
* [Limitaciones y optimizaciones para Raspberry Pi](docs/Limitaciones.md)
* [Guía de instalación de Raspberry Pi OS](docs/Install-RaspberryPi-OS.md)
* [Configuración inicial del sistema](docs/config-init.md)
* [Entorno de desarrollo y extensiones recomendadas](docs/enviroment.md)
* [Drivers necesarios para placas Arduino/ESP32](docs/Drivers.md)
* [Guía de trabajo con Python en el nodo Edge](docs/Python.md)
* [Guía completa de integración Git](docs/merge-git.md)
* [Flujo Git basado en Git Flow](docs/git-workflow.md)

---

## 🗂 Estructura del Proyecto

```plaintext
indoor-system/
├── api-indoors/         # Backend (Node.js + Express + MongoDB)
├── edge-node/           # Nodo Edge (Python sobre Raspberry Pi)
├── frontend-indoors/    # Dashboard Web (React + Redux)
├── docs/                # Documentación técnica y guías paso a paso
├── test/                # Datos simulados y pruebas
└── README.md            # Este archivo
```

---

## 🧱 Arquitectura del Sistema (resumen)

```flowchart TD
    ESP32[ESP32 NodeMCU] -->|Wi-Fi / MQTT| Broker[Broker MQTT (Mosquitto en Pi)]
    Broker -->|MQTT Subscribe| Edge[Python Edge Node]
    Broker -->|MQTT Subscribe| API[API REST Node.js]
    Edge -->|HTTP POST JSON| API
    API -->|Guardar| DB[(MongoDB)]
    API -->|HTTP GET| FE[Frontend React]
    API -->|WebSocket Push| FE
```

---

## 🧪 Estado actual y próximos pasos

| Módulo             | Estado                 |
| ------------------ | ---------------------- |
| `api-indoors`      | 🟢 Base creada         |
| `edge-node`        | 🟢 Base creada         |
| `frontend-indoors` | 🟢 Base creada         |
| `docs`             | ✅ Documentación activa |

### Tareas en curso:

* Integrar sensores al ESP32 y simular lecturas
* Probar flujo MQTT completo (ESP32 → Broker → Edge/API)
* Conectar dashboard React al backend (REST + WebSocket)
* Test de extremo a extremo (lectura → visualización)

---

> Este sistema está desarrollado sobre Windows, utilizando Git Bash en Visual Studio Code. Todos los pasos están documentados en archivos `.md` con estructura modular y comentarios detallados para facilitar el aprendizaje y la futura extensión del sistem
