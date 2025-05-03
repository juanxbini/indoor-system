# 🧠 Arquitectura Edge Computing en el Sistema Indoor

## 📌 ¿Qué es Edge Computing?

**Edge Computing** es un enfoque arquitectónico donde el procesamiento de datos ocurre **lo más cerca posible del origen** (por ejemplo, sensores o dispositivos físicos), en lugar de enviar toda la información a un servidor central o la nube. En nuestro sistema, ese “borde” es una Raspberry Pi ejecutando Python, entre el Arduino y el backend.

---

## 🧩 ¿Por qué elegimos Edge Computing?

Ventajas clave para nuestro proyecto:

| Beneficio                     | Ejemplo concreto en el sistema                                          |
| ----------------------------- | ----------------------------------------------------------------------- |
| ✅ Reducción de latencia       | El nodo Edge puede decidir cuándo y qué datos enviar al backend         |
| ✅ Tolerancia a errores de red | Si no hay conexión, los datos pueden almacenarse o actuar localmente    |
| ✅ Escalabilidad modular       | Se pueden añadir más nodos Edge sin afectar la API principal            |
| ✅ Procesamiento previo        | Los datos crudos del Arduino se pueden filtrar o transformar localmente |
| ✅ Desacoplamiento             | Cada capa cumple una función clara e independiente                      |

---

## 🏗️ Componentes de la arquitectura Edge-Node

```
indoor-system/
├— Arduino                 → Captura de sensores físicos (analógico/digital)
├— edge-node/ (Python)    → Nodo Edge en Raspberry Pi: procesamiento + reenvío HTTP
├— api-indoors/ (Node.js) → Backend: validación, lógica, almacenamiento en MongoDB
└— frontend-indoors/      → Dashboard web para visualización e interacción
```

---

## ➞ Flujo de Datos en la Arquitectura Edge

```mermaid
flowchart TD
    A[Arduino] -->|Serial USB| B[Raspberry Pi (Nodo Edge)]
    B -->|POST /data| C[API REST (Node.js)]
    C --> D[MongoDB]
    C --> E[Frontend Web (React)]
    E -->|GET /data| C
```

---

## 🧠 Responsabilidades del Nodo Edge

El módulo `edge-node/` en Raspberry Pi es el corazón de esta arquitectura. Sus tareas principales:

| Tarea                          | Implementación sugerida (Python)              |
| ------------------------------ | --------------------------------------------- |
| Leer datos por puerto serial   | `pyserial` desde `/dev/ttyUSB0`               |
| Validar o filtrar información  | Clases en `entities/` + lógica en `services/` |
| Enviar datos al backend        | `requests.post()` a la API REST en Node.js    |
| Manejar fallos o desconexiones | Reintentos, almacenamiento local temporal     |

---

## 📁 Estructura interna del módulo `edge-node/`

```plaintext
edge-node/
├— main.py                   # Punto de entrada
├— config/settings.py       # Configuración general y .env
├— services/
│   ├— serial_reader.py     # Lectura desde Arduino
│   └— http_client.py       # Comunicación con la API REST
├— entities/sensor_data.py  # Modelo de datos
└— requirements.txt         # Dependencias Python
```

---

## ⚠️ Limitaciones del Nodo Edge (Raspberry Pi 4)

Ver documento: [`docs/Limitaciones.md`](./Limitaciones.md)

| Recurso        | Recomendación clave                             |
| -------------- | ----------------------------------------------- |
| RAM (4 GB)     | Evitar dashboards pesados o múltiples procesos  |
| Almacenamiento | Usar MongoDB Lite y limpiar logs frecuentemente |
| SD Card        | Minimizar escrituras con `logrotate` y TTL      |

---

## 🔎 Casos de uso comunes para Edge Computing

| Caso de uso                 | ¿Cómo lo resolvemos?                               |
| --------------------------- | -------------------------------------------------- |
| Conexión intermitente       | Se puede usar buffer local en el nodo Edge         |
| Lecturas de alta frecuencia | Se filtran los datos antes de enviarlos            |
| Control local de actuadores | Python puede interactuar directamente con GPIO     |
| Expansión modular           | Se puede agregar otro nodo Edge sin cambiar la API |

---

## 🚀 Escalabilidad futura

Esta arquitectura permite migrar fácilmente a:

* MQTT para comunicación en tiempo real
* Balanceo de carga con múltiples Edge Nodes
* Backends desacoplados por microservicios
* Dashboards avanzados externos (Grafana, Dash)

---

## ✅ Conclusión

Edge Computing nos permite construir un sistema indoor:

* Robusto frente a fallos
* Modular y escalable
* Ideal para entornos híbridos físico-digitales

> 📌 Esta arquitectura es especialmente adecuada para prototipos evolucionables, y se puede adaptar fácilmente a proyectos más grandes o críticos.
