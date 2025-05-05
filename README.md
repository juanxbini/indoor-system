# 🌱 Sistema de Medición Indoor

Sistema modular para monitoreo ambiental en interiores, con arquitectura cliente-servidor y lógica Edge Computing.

---

## 📚 Tabla de Contenidos

- [🌱 Sistema de Medición Indoor](#-sistema-de-medición-indoor)
  - [📚 Tabla de Contenidos](#-tabla-de-contenidos)
  - [1. 📌 Resumen del Proyecto](#1--resumen-del-proyecto)
  - [2. 📂 Estructura del Repositorio](#2--estructura-del-repositorio)
  - [3. 📦 Guías por Módulo](#3--guías-por-módulo)
    - [3.1. 🔙 Backend API (Node.js + Express + MongoDB)](#31--backend-api-nodejs--express--mongodb)
    - [3.2. 🧠 Nodo Edge (Python + Raspberry Pi)](#32--nodo-edge-python--raspberry-pi)
    - [3.3. 💻 Frontend Web (React + Redux)](#33--frontend-web-react--redux)
  - [4. 📚 Documentación General](#4--documentación-general)
  - [5. 🚧 Estado del Proyecto](#5--estado-del-proyecto)
  - [6. 🤪 Próximos Pasos](#6--próximos-pasos)

---

## 1. 📌 Resumen del Proyecto

Este sistema mide variables ambientales desde sensores conectados a un Arduino, los procesa en una Raspberry Pi (Python), los envía a una API REST (Node.js) y visualiza los datos en una app web (React).

> Arquitectura modular, escalable, documentada paso a paso. Ideal para entornos indoor de desarrollo y prototipado.

---

## 2. 📂 Estructura del Repositorio

```plaintext
indoor-system/
├── api-indoors/           → Backend principal (Node.js + MongoDB)
├── edge-node/             → Nodo Edge (Python en Raspberry Pi)
├── frontend-indoors/      → Interfaz web (React + Redux)
├── docs/                  → Documentación técnica
├── test/                  → Datos simulados y pruebas
└── README.md              → Este archivo principal
```

---

## 3. 📦 Guías por Módulo

### 3.1. 🔙 Backend API (Node.js + Express + MongoDB)

* 📁 [Código fuente](./api-indoors)
* 📄 [Guía de estructura y dependencias](docs/init/README.md#4-backend-api-nodejs--express--mongodb)

### 3.2. 🧠 Nodo Edge (Python + Raspberry Pi)

* 📁 [Código fuente](./edge-node)
* 📄 [Python](./edge-node/docs/Python.md)
* 📄 [Arquitectura Edge](./edge-node/docs/architecture-edge.md)
* 📄 [Instalación del OS](docs/enviroment/Install-RaspberryPi-OS.md)
* 📄 [Drivers USB Arduino/ESP32](docs/enviroment/Drivers.md)
* 📄 [Limitaciones técnicas Raspberry Pi](docs/enviroment/Limitaciones.md)

### 3.3. 💻 Frontend Web (React + Redux)

* 📁 [Código fuente](./frontend-indoors)
* 📄 [Estructura recomendada y configuración](docs/init/README.md#6-frontend-react--redux)

---

## 4. 📚 Documentación General

* 🧱 [Arquitectura del sistema](docs/system-architecture.md)
* 🛠️ [Inicio y configuración del entorno](docs/init/README.md)
* 🤩 [Entorno de trabajo y extensiones VSCode](/docs/enviroment/README.md)
* 🔀 [Flujo de trabajo Git](docs/git-workflow.md)

---

## 5. 🚧 Estado del Proyecto

| Módulo             | Estado                 |
| ------------------ | ---------------------- |
| `api-indoors`      | 🟢 Base creada         |
| `edge-node`        | 🟢 Base creada         |
| `frontend-indoors` | 🟢 Base creada         |
| `docs`             | ✅ Documentación activa |

---

## 6. 🤪 Próximos Pasos

* 🔌 Integrar sensores físicos y pruebas de lectura
* 🌐 Configurar endpoints y validaciones REST
* 🖥️ Conectar frontend con el backend
* 🧪 Simular flujo de extremo a extremo en entorno real

---

> 🛠️ Proyecto desarrollado sobre Windows con Git Bash + VSCode. Cada módulo fue diseñado bajo principios de modularidad, escalabilidad y buena documentación.
