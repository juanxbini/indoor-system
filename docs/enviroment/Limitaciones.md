# 📉 Limitaciones y Recomendaciones de Uso - Raspberry Pi 4 (4 GB RAM / 64 GB SD)

Este documento describe las **limitaciones reales** y **buenas prácticas** al utilizar una **Raspberry Pi 4 con 4 GB de RAM y una tarjeta microSD de 64 GB**, como nodo Edge dentro del sistema de monitoreo indoor.

---

## 🧠 Limitaciones por Memoria RAM (4 GB)

| Área                              | Impacto                                                        |
|----------------------------------|----------------------------------------------------------------|
| Multitarea intensiva             | Puede correr servicios como Python, Node.js y MongoDB simultáneamente, pero puede saturarse si se agregan dashboards pesados o procesos no optimizados. |
| Contenedores o virtualización    | No se recomienda ejecutar múltiples contenedores Docker pesados. Se puede usar 1 o 2 livianos, pero con cuidado. |
| Procesamiento de datos o imágenes| Limitado para tareas pesadas como análisis de video o IA. No apto para ML local. |
| Sensores en paralelo             | Si el código no libera recursos o acumula datos en memoria, puede provocar cuelgues o latencia. |

---

## 💾 Limitaciones por Almacenamiento (microSD 64 GB)

| Uso                              | Consideración                                                  |
|----------------------------------|----------------------------------------------------------------|
| Base de datos (MongoDB)          | MongoDB Lite funciona correctamente. Si se acumulan datos históricos sin limpieza, se puede llenar la SD. |
| Escritura frecuente              | Las SD se degradan con muchas escrituras. Usar `logrotate`, TTL en MongoDB o mover los datos a un disco externo. |
| Velocidad de acceso              | Lenta comparada con un SSD. Puede haber cuellos de botella si hay mucha concurrencia o grandes volúmenes. |
| Durabilidad                      | Las SD no son ideales para servidores de producción a largo plazo sin respaldo. |

---

## ✅ Recomendaciones de Optimización

1. **Minimizar escrituras** innecesarias:
   - Habilitar `logrotate`.
   - Usar `tmpfs` para logs temporales.
   - Evitar almacenar logs en tiempo real sin compresión o rotación.

2. **Limitar la persistencia en MongoDB**:
   - Usar TTL en documentos antiguos.
   - Registrar solo datos esenciales o hacer backups periódicos.

3. **Optimizar código en Python y Node.js**:
   - Liberar recursos y evitar ciclos innecesarios.
   - Usar `async` y control de errores para evitar bloqueos.

4. **Monitorear recursos** regularmente:
   - Usar `htop`, `iotop`, `df -h`, `free -m`, etc.
   - Configurar alertas simples con scripts en cron o logs.

5. **Evitar uso de interfaz gráfica** en la Pi:
   - Usar Raspberry Pi OS Lite.
   - Acceder por SSH desde otra máquina (`Remote - SSH` en VSCode).

6. **Agregar archivo de swap (opcional)**:
   - Si hay problemas de RAM, se puede configurar swap adicional, aunque degrada el rendimiento de la SD.

7. **Desarrollar con vistas a escalar**:
   - Si el sistema crece, mover MongoDB o la API a un servidor más robusto o nube.

---

## 🧪 ¿Qué se puede hacer con esta configuración?

✔️ Ejecutar `main.py` en Python con `pyserial` y `requests`  
✔️ Enviar datos al backend REST en Node.js  
✔️ Correr MongoDB local con datos limitados  
✔️ Hacer scraping o análisis de datos simple  
✔️ Acceder a la Pi desde VSCode con `Remote - SSH`  
✔️ Mostrar dashboards simples o enviar datos a uno externo

---

> 📌 Este entorno es ideal para desarrollo y validación de prototipos. Si se planea un uso continuo en producción, evaluar migración progresiva de funciones a hardware más robusto o segmentación de servicios.

