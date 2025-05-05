# Arquitectura del Sistema Indoor (REST + MQTT)

Este documento reemplaza y actualiza la arquitectura anterior Cliente-Servidor con lógica Edge Computing, incorporando un único **broker MQTT centralizado** y mostrando la **estructura de carpetas actualizada** de todo el proyecto.

---

## 📌 Visión General

Se adopta un único **broker MQTT** (Mosquitto) en la Raspberry Pi, manteniendo la **API REST** de Node.js para histórico, configuración y análisis, y el **Frontend React** para visualización:

```mermaid
flowchart TD
    ESP32[ESP32s NodeMCU\n(Publisher MQTT)] -->|Wi-Fi / MQTT| Broker[Broker MQTT\n(Mosquitto en Pi)]
    Broker -->|MQTT Subscribe| Edge[Python Edge Node\n(Subscriber)]
    Broker -->|MQTT Subscribe| API[Node.js API REST\n(Subscriber)]
    Broker -->|MQTT Subscribe opcional| FE[Frontend React\n(Subscriber)]
    Edge -->|HTTP POST JSON| API
    API -->|Guardar| DB[(MongoDB)]
    API -->|HTTP GET| FE
    API -->|WebSocket Push| FE
```

---

## 🗂️ Estructura de Carpetas Actualizada

```plaintext
indoor-system/
├── api-indoors/                 # Backend principal (Node.js + Express + MongoDB)
│   ├── src/
│   │   ├── config/              # Configuración (.env, claves)
│   │   ├── services/
│   │   │   └── mqttSubscriber.js # Suscriptor MQTT
│   │   ├── controllers/         # Controladores REST
│   │   ├── routes/              # Definición de rutas
│   │   ├── usecases/            # Lógica de negocio
│   │   └── repositories/        # Acceso a datos
│   ├── .env                     # Variables de entorno
│   └── package.json
├── edge-node/                   # Nodo Edge con Python en Raspberry Pi
│   ├── services/
│   │   ├── serial_reader.py     # Lectura serie y parseo crudo
│   │   └── mqtt_publisher.py    # Publicador MQTT
│   ├── main.py                  # Entrada del módulo Edge
│   ├── requirements.txt         # Dependencias Python
│   └── .env                     # Configuración del broker y API
├── frontend-indoors/            # Interfaz web (React + Redux)
│   ├── src/
│   │   ├── app/                 # Store y configuración global
│   │   ├── features/            # Características (sensors, dashboard)
│   │   ├── components/          # Componentes UI reutilizables
│   │   ├── services/            # Axios y MQTT/WebSocket client
│   │   ├── hooks/               # Custom hooks
│   │   └── main.jsx             # Punto de entrada React
│   ├── public/
│   └── package.json
├── docs/                        # Documentación técnica
│   ├── system-architecture.md   # Este archivo actualizado
│   ├── init/                    # Configuración inicial y setup
│   └── ...                      # Otras guías (git, Install-RPi, Drivers)
├── test/                        # Simulaciones y pruebas unitarias
│   ├── dummy_inputs/
│   └── log_simulations/
└── README.md                    # Índice y descripción general
```

---

## 🔧 Componentes y Funciones


| Componente                   | Tipo       | Rol Principal                                                 |
| ---------------------------- | ---------- | ------------------------------------------------------------- |
| **ESP32s NodeMCU**           | Publisher  | Mide sensores y publica datos vía MQTT al broker              |
| **Broker MQTT (Mosquitto)**  | Servidor   | Enruta mensajes entre publishers y subscribers                |
| **Python Edge Node**         | Subscriber | Filtra/transforma lecturas y las reenvía al API REST          |
| **API REST (Node.js)**       | Subscriber | Guarda histórico, expone endpoints REST y WebSocket para FE   |
| **Frontend (React + Redux)** | Subscriber | Consume histórico por REST y datos en tiempo real por WS/MQTT |
=======
Ver documento: [`Limitaciones.md`](./docs/enviroment/Limitaciones.md)

| Recurso        | Recomendación clave                             |
| -------------- | ----------------------------------------------- |
| RAM (4 GB)     | Evitar dashboards pesados o múltiples procesos  |
| Almacenamiento | Usar MongoDB Lite y limpiar logs frecuentemente |
| SD Card        | Minimizar escrituras con `logrotate` y TTL      |


---

## 🔁 Flujo de Datos Detallado

1. **ESP32s** conecta a la red Wi‑Fi y publica en MQTT:

   ```cpp
   client.publish("sensor/temperature", "23.50");
   ```
2. **Mosquitto** recibe y reenvía a todos los suscriptores.
3. **Python Edge Node** (suscriptor) filtra, normaliza y hace POST al API:

   ```python
   client.on_message(...)
   requests.post('http://localhost:3000/api/sensors', payload)
   ```
4. **API REST** guarda en MongoDB y notifica al frontend:

   * REST: `GET /api/sensors/last`
   * WS: `socket.emit('sensorData', data)`
5. **Frontend React**:

   * Solicita histórico via REST.
   * Se suscribe al WebSocket/MQTT para datos en tiempo real.

---

## ⚙️ Configuración Básica

* **Broker Mosquitto** (Raspberry Pi):

  ```bash
  sudo apt install mosquitto
  sudo systemctl enable mosquitto
  ```

  **.env**:

  ```env
  MQTT_BROKER=mqtt://localhost:1883
  ```

* **ESP32 NodeMCU**:

  * Configurar SSID/PSK en `main.cpp`.
  * IP del broker (Pi) en `PubSubClient.setServer(...)`.

* **Python Edge Node**:

  ```bash
  pip install paho-mqtt requests
  ```

  Suscribir, procesar y reenviar al API.

* **API Node.js**:

  ```bash
  npm install mqtt express mongoose socket.io
  ```

  Importar `mqttSubscriber.js` en `server.js`.

* **React Frontend**:

  ```bash
  npm install mqtt socket.io-client axios
  ```

  Configurar cliente WS o MQTT para datos live.

---

## 📌 Próximos Pasos

1. **Test End-to-End**: ESP32 → Mosquitto → Edge Node → API → MongoDB → React.
2. **Optimización**: Añadir autenticación y TLS en MQTT.
3. **Monitoreo**: Scripts de alerta (cron, logrotate).
4. **Escalabilidad**: Contenerizar servicios y mover base de datos a servidor externo.

---

*Este documento sustituye a la versión anterior y muestra la estructura completa y actualizada del sistema indoor.*
