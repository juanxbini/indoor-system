# 🖥️ Entorno de Trabajo

Este documento describe el proceso de preparación del entorno de desarrollo para el proyecto de monitoreo indoor. Incluye herramientas, extensiones, estructuras de carpetas y configuraciones necesarias antes de la llegada del hardware.

---

## 🧩 Extensiones utilizadas en el entorno de desarrollo

Este proyecto utiliza Visual Studio Code como entorno de desarrollo principal. Para facilitar el trabajo con microcontroladores, servidores remotos y mantener una alta calidad en el código y documentación, hemos instalado las siguientes extensiones:

---

### 📦 Tabla resumen

| Extensión                | Función                         | Uso en el proyecto                      |
|--------------------------|----------------------------------|------------------------------------------|
| PlatformIO IDE           | Desarrollo de firmware avanzado  | Código principal para ESP32              |
| Arduino (Microsoft)      | Programación clásica de placas   | Tests y prototipos simples con Arduino   |
| Remote - SSH             | Conexión remota por SSH          | Gestionar Raspberry Pi desde VSCode      |
| Prettier                 | Formato automático de código     | Mantener código limpio y consistente     |
| ESLint                   | Revisión de errores y estilo     | Aplicar buenas prácticas en JS           |
| Markdown All in One      | Soporte avanzado para Markdown   | Crear y mantener documentación en GitHub |

---

### 🔧 Detalle de extensiones

#### 1. PlatformIO IDE
- **¿Qué es?** Entorno para desarrollar proyectos con microcontroladores (ESP32, STM32, etc.).
- **Uso:** Crear, compilar, subir código, monitorear puerto serie.
- **Comandos útiles:** `PlatformIO: New Project`, `PlatformIO: Upload`

#### 2. Arduino (oficial de Microsoft)
- **¿Qué es?** Extensión para programación rápida con placas Arduino.
- **Uso:** Compilar y subir sketches tradicionales.
- **Comandos útiles:** `Arduino: Upload`, `Arduino: Select Board`

#### 3. Remote - SSH
- **¿Qué es?** Herramienta para conectarse a dispositivos remotos (como una Raspberry Pi) desde VSCode.
- **Uso:** Acceder, editar, monitorear y ejecutar scripts de backend.
- **Comandos útiles:** `Remote-SSH: Connect to Host`, `Remote-SSH: Open Folder`

#### 4. Prettier
- **¿Qué es?** Formateador automático de código.
- **Uso:** Aplicar un estilo consistente al código JS/TS/HTML.
- **Comando útil:** `Format Document`

#### 5. ESLint
- **¿Qué es?** Herramienta de análisis de código para JavaScript.
- **Uso:** Detectar errores y aplicar buenas prácticas.
- **Comando útil:** `ESLint: Fix all auto-fixable problems`

#### 6. Markdown All in One
- **¿Qué es?** Extensión que mejora la edición de archivos Markdown.
- **Uso:** Crear documentación más rápida y organizada.
- **Comandos útiles:** `Markdown: Toggle Preview`, `Markdown: Create Table of Contents`

---

## 🖥️ 1. Requisitos Generales del Sistema

- Sistema operativo: **Windows**
- IDE principal: **Visual Studio Code**
- Control de versiones: **Git**
- Lenguajes principales: **C/C++ (Arduino), Python, JavaScript (Node.js)**

---

## ⚙️ 2. Instalaciones necesarias

### A. Visual Studio Code

- Descargar desde: [https://code.visualstudio.com](https://code.visualstudio.com)

### B. Git

```bash
winget install Git.Git
```

### C. Node.js + npm

- Descargar: [https://nodejs.org](https://nodejs.org)
- Verificación:

```bash
node -v
npm -v
```

### D. MongoDB (para entorno local)

- Descargar: [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)

---

## 🔌 3. Entorno para Arduino y microcontroladores

### A. PlatformIO IDE (recomendado)

- Instalar la extensión `PlatformIO IDE` desde VS Code
- Incluye automáticamente el CLI (no requiere instalación manual)
- Verificación:

```bash
pio --version
```

### B. Drivers necesarios

- **CH340/CH341:** [https://sparks.gogo.co.nz/ch340.html](https://sparks.gogo.co.nz/ch340.html)
- **CP2102:** [https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

---

## 🍓 4. Entorno para Raspberry Pi (si se usa como nodo intermedio)

### A. Raspberry Pi Imager

- [https://www.raspberrypi.com/software/](https://www.raspberrypi.com/software/)

### B. SSH y herramientas útiles

```bash
ssh pi@<IP>
sudo apt update && sudo apt install python3-pip
pip3 install flask gpiozero
```

---

## 📁 5. Estructura del Proyecto

```plaintext
indoor-system/
├── api-indoors/
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── routes/
│   │   ├── usecases/
│   │   ├── repositories/
│   │   ├── entities/
│   │   └── middlewares/
│   └── src/server.js
│   └── .env
│   └── package.json
│   └── .gitignore
│
├── edge-node/
│   ├── config/
│   ├── services/
│   ├── entities/
│   ├── main.py
│   ├── .env
│   ├── requirements.txt
│   └── venv/
│
├── frontend-indoors/
│   ├── src/
│   │   ├── app/
│   │   ├── features/
│   │   │   ├── dashboard/
│   │   │   └── sensors/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── hooks/
│   │   └── main.jsx
│   ├── public/
│   └── package.json
│
├── docs/
│   ├── wiring_diagram.png
│   ├── entorno-de-trabajo.md
│   └── init/
│       └── README.md
│
├── test/
│   ├── dummy_inputs/
│   └── log_simulations/
│
└── README.md
```

---

## 🧪 6. Simuladores recomendados (opcional)

- [Wokwi](https://wokwi.com/) — Simulador de Arduino/ESP32
- [Tinkercad Circuits](https://www.tinkercad.com/circuits)

---

## ✅ 7. Próximos pasos

- Crear primer proyecto de PlatformIO (ej. LED blink)
- Versionar estructura inicial con Git
- Documentar comandos básicos en `/docs/setup.md`

---

> 📌 **Nota:** Este entorno se irá ampliando conforme avancemos en la integración de sensores y comunicación entre nodos.

