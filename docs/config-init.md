# 🛠️ Inicio del Proyecto - Sistema Indoor

## 📁 1. Crear Carpeta Raíz del Proyecto

```bash
mkdir indoor-system
cd indoor-system
```

---

## 🔧 2. Inicializar Repositorio Git

```bash
git init
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
```

---

## 🗂️ 3. Crear Subcarpetas por Módulo

```bash
mkdir api-indoors frontend-indoors edge-node
```

---

## ⚙️ 4. Backend API (Node.js + Express + MongoDB)

### 📁 Estructura sugerida: Clean Architecture

```bash
cd api-indoors
npm init -y
npm install express mongoose dotenv cors

mkdir src
cd src
mkdir controllers routes usecases repositories entities config middlewares
cd ..
touch src/server.js
```

**Archivo de entrada**: `src/server.js`

**Dependencias útiles**:

```bash
npm install nodemon --save-dev
```

**Script para desarrollo en `package.json`**:

```json
"scripts": {
  "dev": "nodemon src/server.js"
}
```

---

## 🧩 5. Edge Node (Python en Raspberry Pi)

### 📚 ¿Qué es un entorno virtual y por qué usarlo?

Un **entorno virtual** en Python es un espacio aislado donde instalás tus propias versiones de librerías sin afectar el sistema global. Esto evita conflictos entre proyectos que usan diferentes versiones de dependencias.

---

### 📁 Estructura sugerida

Antes de crear el entorno virtual, asegurate de tener Python instalado y accesible desde la terminal. En Windows, es común que `python` apunte al instalador de Microsoft Store. En su lugar, probá con:

```bash
py --version
```

Si funciona correctamente (por ejemplo, `Python 3.13.3`), usá `py` para crear el entorno virtual:

```bash
cd ../edge-node          # Entrás al directorio del módulo Edge
py -m venv venv          # Creamos el entorno virtual llamado 'venv'
source venv/Scripts/activate  # Activás el entorno en Git Bash
```

Una vez activado, instalamos las siguientes dependencias:

```bash
pip install requests pyserial python-dotenv
```

### 📦 Explicación de librerías instaladas

| Paquete         | Rol en el proyecto                                           |
|----------------|--------------------------------------------------------------|
| `requests`     | Permite hacer solicitudes HTTP (POST, GET) al backend Node.js|
| `pyserial`     | Maneja la comunicación con el puerto serial (Arduino)        |
| `python-dotenv`| Carga variables de entorno desde un archivo `.env`           |

---

### 🔁 ¿Cuándo activar y desactivar el entorno virtual?

Activá el entorno virtual **cada vez que trabajes en este módulo**, para asegurarte de usar los paquetes y versiones correctas del proyecto.

#### 🟢 Para activar:

```bash
source venv/Scripts/activate
```

Verás `(venv)` al comienzo de tu línea en la terminal. Significa que estás dentro del entorno.

#### 🔴 Para desactivar:

```bash
deactivate
```

También se desactiva si cerrás la terminal.

---

### 📄 Generar archivo `requirements.txt`

Una vez que tengas todas las dependencias instaladas dentro del entorno virtual, generá este archivo para guardar las versiones exactas:

```bash
pip freeze > requirements.txt
```

Esto va a crear un archivo como este:

```
python-dotenv==1.0.0
pyserial==3.5
requests==2.31.0
```

Luego, si reinstalás el entorno o compartís el proyecto, podés correr:

```bash
pip install -r requirements.txt
```

Esto instalará todas las dependencias necesarias automáticamente.

📌 **Consejo**: agregá la carpeta `venv/` al `.gitignore` para evitar subir archivos innecesarios al repositorio.

> 💡 Si `python` sigue sin funcionar, podés desactivar el alias conflictivo desde:
> Configuración > Aplicaciones > Configuración avanzada de aplicaciones > Alias de ejecución de aplicaciones.

**Estructura**:

```
edge-node/
│
├── main.py
├── config/
│   └── settings.py
├── services/
│   └── serial_reader.py
│   └── http_client.py
├── entities/
│   └── sensor_data.py
├── .env
```

---

## 🖥️ 6. Frontend (React + Redux)

### 📁 Estructura sugerida: Clean-ish + Feature folders

Usaremos **Bootstrap** como framework de estilos en lugar de Tailwind CSS, para simplificar la configuración y aprovechar sus componentes listos para usar.

---

### 🎨 Instalación de Bootstrap

Desde la raíz del frontend:

```bash
npm install bootstrap
```

Luego, en `main.jsx`, importamos su hoja de estilos global:

```js
import 'bootstrap/dist/css/bootstrap.min.css';
```

Opcionalmente, si querés usar componentes prearmados como `<Button>` o `<Modal>` de forma declarativa, podés instalar:

```bash
npm install react-bootstrap
```

Y luego importar en tus componentes:

```js
import { Button } from 'react-bootstrap';
```

---

### 📁 Estructura recomendada

```bash
cd ../frontend-indoors
npm create vite@latest . -- --template react
npm install
npm install redux react-redux @reduxjs/toolkit axios
```

**Estructura sugerida**:

```
frontend-indoors/
├── src/
│   ├── app/                # Store Redux y configuración global
│   ├── features/
│   │   └── dashboard/      # Vista principal
│   │   └── sensors/        # Slice y componentes relacionados a sensores
│   ├── components/         # UI reutilizable
│   ├── pages/              # Rutas principales
│   ├── services/           # Comunicación con la API
│   ├── hooks/              # Custom Hooks
│   └── main.jsx
```

---

## 🌐 7. Git: Estructura Recomendada

Usamos ramas por feature al estilo Git Flow (sin herramientas externas):

```bash
git checkout -b feature/api-setup
# trabajar...
git add .
git commit -m "init(api): estructura base y dependencias"
git push origin feature/api-setup
```

---

## ✅ 8. Checklist General Inicial

| Tarea                          | Estado |
|-------------------------------|--------|
| Carpeta principal creada      | ✅     |
| Git inicializado              | ✅     |
| Subcarpetas por módulo        | ✅     |
| API Node.js configurado       | ✅     |
| Edge (Python) configurado     | ✅     |
| Frontend React configurado    | ✅     |
| Estructuras internas creadas  | ✅     |

---

Este documento puede guardarse como `/doc/init/README.md` dentro del repositorio del proyecto para tener un punto de partida claro y documentado. ✅

