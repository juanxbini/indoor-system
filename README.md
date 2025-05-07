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
* [Configuración detallada inicial de Raspberry Pi](docs/raspberry-init.md)
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

## 🔗 Índice de Módulos

### 🔙 Backend API (Node.js + Express + MongoDB)
- 📁 [api-indoors/](./api-indoors)
- 📄 [Guía de estructura y dependencias](docs/init/README.md#4-backend-api-nodejs--express--mongodb)

### 🧠 Nodo Edge (Python + Raspberry Pi)
- 📁 [edge-node/](./edge-node)
- 📄 [Instalación de Raspberry Pi OS](docs/Install-RaspberryPi-OS.md)
- 📄 [Drivers USB Arduino/ESP32](docs/Drivers.md)

### 💻 Frontend Web (React + Redux)
- 📁 [frontend-indoors/](./frontend-indoors)
- 📄 [Instalación y estructura sugerida](docs/init/README.md#6-frontend-react--redux)

---

## 📚 Documentación General

- 🗷️ [Arquitectura del sistema](docs/system-architecture.md)
- 🛠️ [Inicio y configuración del entorno](docs/init/README.md)
- ⚙️ [Entorno de trabajo y extensiones](README.md)
- 🔀 [Flujo de trabajo Git](docs/git-workflow.md)
- 🍓 [Guía para instalar Raspberry Pi OS](docs/Install-RaspberryPi-OS.md)
- 🧹 [Drivers para Arduino/ESP32](docs/Drivers.md)

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

> Este sistema está desarrollado sobre Windows, utilizando Git Bash en Visual Studio Code. Todos los pasos están documentados en archivos `.md` con estructura modular y comentarios detallados para facilitar el aprendizaje y la futura extensión del sistema.
