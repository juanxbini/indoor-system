# 🛠️ Configuración Inicial de Raspberry Pi para el Proyecto Indoor

Este documento resume todos los pasos recomendados para dejar una Raspberry Pi lista para desarrollo y ejecución del sistema de monitoreo indoor basado en REST + MQTT.

---

## ✅ 1. Acceso y Actualización

```bash
passwd                            # Cambiar contraseña del usuario actual
sudo apt update && sudo apt upgrade -y  # Actualizar sistema
```

Instalar herramientas útiles:

```bash
sudo apt install git curl vim htop net-tools unzip -y
```

Verificar IP local y hostname:

```bash
hostname -I
hostname
```

---

## ✅ 2. Personalización del Sistema

Cambiar hostname (opcional):

```bash
sudo raspi-config
# System Options > Hostname > indoor-pi
```

Configurar zona horaria y localización:

```bash
sudo raspi-config
# Localisation Options > Timezone / Locale / Keyboard Layout
```

Habilitar interfaces necesarias:

```bash
sudo raspi-config
# Interfacing Options > I2C, SPI, Serial, etc.
```

---

## ✅ 3. Servicios para el Proyecto Indoor

### 🟡 Mosquitto (Broker MQTT)

```bash
sudo apt install mosquitto mosquitto-clients -y
sudo systemctl enable mosquitto
```

### 🐍 Python y entorno virtual (Edge Node)

```bash
sudo apt install python3-venv python3-pip -y
mkdir -p ~/indoor-system/edge-node/logs
```

---

## ✅ 4. Logging y Protección de la microSD

Instalar `logrotate`:

```bash
sudo apt install logrotate -y
```

Crear configuración personalizada:

```bash
sudo nano /etc/logrotate.d/indoor-system
```

Contenido:

```conf
/home/pi/indoor-system/edge-node/logs/*.log {
    weekly
    rotate 4
    compress
    missingok
    notifempty
    copytruncate
}
```

---

## ✅ 5. Seguridad adicional (opcional)

Crear nuevo usuario con permisos sudo:

```bash
sudo adduser miusuario
sudo usermod -aG sudo miusuario
```

Desactivar usuario `pi` (opcional):

```bash
sudo passwd -l pi
```

---

## ✅ 6. IP Estática (opcional)

Editar configuración:

```bash
sudo nano /etc/dhcpcd.conf
```

Agregar al final:

```conf
interface wlan0
static ip_address=192.168.100.99/24
static routers=192.168.100.1
static domain_name_servers=8.8.8.8 1.1.1.1
```

---

## ✅ 7. Script de bienvenida al iniciar sesión (opcional)

Este paso permite que cada vez que inicies sesión por SSH se muestre automáticamente información útil del sistema.

Editar el archivo `~/.bashrc` con:

```bash
nano ~/.bashrc
```

Ir al final del archivo y agregar estas líneas:

```bash
echo "🔧 Raspberry Pi $(cat /proc/device-tree/model)"
echo "📡 IP: $(hostname -I)"
echo "📛 Hostname: $(hostname)"
echo "🕒 Fecha/hora: $(date)"
```

Guardar con `Ctrl + O`, salir con `Ctrl + X`.

La próxima vez que te conectes por SSH, verás esta información automáticamente.

---

> 📌 Esta configuración base permite tener una Raspberry Pi segura, optimizada y lista para ejecutar los módulos `edge-node`, `mosquitto`, y comunicación con `api-indoors` desde el entorno indoor.
