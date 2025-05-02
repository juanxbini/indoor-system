# 🌱 Sistema de Medición Indoor

Este repositorio contiene el sistema modular de monitoreo indoor, estructurado bajo una arquitectura cliente-servidor con lógica Edge Computing. El objetivo es medir variables ambientales desde sensores conectados a un Arduino, pasando por un nodo edge con Python (Raspberry Pi), una API REST con Node.js y una interfaz web con React.

---

## 🗂️ Estructura del Repositorio

```
indoor-system/
├── api-indoors/           → Backend principal (Node.js + MongoDB)
├── edge-node/             → Nodo Edge (Python en Raspberry Pi)
├── frontend-indoors/      → Interfaz web (React + Redux)
├── docs/                  → Documentación técnica
├── test/                  → Datos simulados y pruebas
└── README.md              → Este archivo
```

---

## 🔗 Índice de Módulos
- 📄 [Guía de estructura y dependencias](docs/init/README.md#4-backend-api-nodejs--express--mongodb)
- 📄 [Instalación y estructura sugerida](docs/init/README.md#6-frontend-react--redux)
- 📄 [Instalación de Raspberry Pi OS](docs/Install-RaspberryPi-OS.md)
- 📄 [Drivers USB Arduino/ESP32](docs/Drivers.md)

### 🔙 Backend API (Node.js + Express + MongoDB)
- 📁 [api-indoors/](./api-indoors)
  
### 🧠 Nodo Edge (Python + Raspberry Pi)
- 📁 [edge-node/](./edge-node)

### 💻 Frontend Web (React + Redux)
- 📁 [frontend-indoors/](./frontend-indoors)

---

## 📚 Documentación General

- 🗷️ [Arquitectura del sistema](docs/system-architecture.md)
- 🛠️ [Inicio y configuración del entorno](docs/init/README.md)
- ⚙️ [Entorno de trabajo y extensiones](README.md)
- 🔀 [Flujo de trabajo Git](docs/git-workflow.md)
- 🍓 [Guía para instalar Raspberry Pi OS](docs/Install-RaspberryPi-OS.md)
- 🧹 [Drivers para Arduino/ESP32](docs/Drivers.md)

---

## 🚧 Estado del Proyecto

| Módulo            | Estado       |
|-------------------|--------------|
| `api-indoors`     | 🟢 Base creada |
| `edge-node`       | 🟢 Base creada |
| `frontend-indoors`| 🟢 Base creada |
| `docs`            | ✅ Documentación modular activa |

---

## 🧪 Próximos Pasos

- Integrar sensores y simular lectura serial
- Configurar endpoints RESTful
- Conectar frontend con la API
- Probar flujo de extremo a extremo en entorno real

---

> Proyecto desarrollado sobre Windows utilizando Git Bash y Visual Studio Code. Cada módulo fue diseñado para ser modular, extensible y documentado desde el inicio.

