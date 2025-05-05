# Instalación de Raspberry Pi OS Lite y Configuración Inicial (Windows)

Este documento describe los pasos para descargar, instalar y preparar una imagen Lite de Raspberry Pi OS desde una PC con Windows, dejando todo listo para usar el dispositivo sin necesidad de monitor ni teclado (headless).

---

## 1. Descargar Raspberry Pi Imager para Windows

1. Ir al sitio oficial: https://www.raspberrypi.com/software/
2. Hacer clic en "Download for Windows".
3. Ejecutar el archivo `.exe` descargado para instalar el programa.

---

## 2. Flashear Raspberry Pi OS Lite

1. Ejecutar **Raspberry Pi Imager**.
2. En "Choose OS" seleccionar:
   - `Raspberry Pi OS Lite (32-bit)` (sin entorno gráfico).
3. En "Choose Storage" seleccionar la tarjeta microSD insertada.
4. Clic en "Write" y esperar a que finalice el proceso.

---

## 3. Habilitar SSH

Una vez que el Imager haya terminado:

1. No retires la microSD aún.
2. Abrí el **Explorador de archivos** de Windows.
3. Accedé a la partición llamada `boot`.
4. Crear un archivo vacío llamado `ssh` (sin extensión):
   - Clic derecho → Nuevo → Documento de texto → Cambiar nombre a `ssh` (sin `.txt`).

Esto activa el servidor SSH en el primer arranque.

---

## 4. Configurar Wi-Fi (opcional)

1. En la misma partición `boot`, crear un archivo llamado `wpa_supplicant.conf`.
2. Contenido del archivo (editar con tus datos):

```conf
country=AR
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="TuNombreDeRedWiFi"
    psk="TuContraseñaWiFi"
    key_mgmt=WPA-PSK
}
```

> Asegurarse que la extensión sea `.conf` y no `.conf.txt`.

---

## 5. Primer Arranque del Raspberry Pi

1. Retirar la microSD de forma segura.
2. Insertarla en el Raspberry Pi.
3. Conectarlo a la corriente.
4. Esperar entre 30 segundos y 1 minuto.

---

## 6. Obtener la IP del Raspberry Pi

- Revisar dispositivos conectados en el router.
- Usar software como [Advanced IP Scanner](https://www.advanced-ip-scanner.com/).
- O si se conecta por HDMI + teclado:
  ```bash
  hostname -I
  ```

---

## 7. Establecer conexión SSH desde Windows

1. Abrir PowerShell o el Símbolo del sistema (CMD).
2. Ejecutar el comando:

```bash
ssh pi@IP_DEL_RASPBERRY
```

Ejemplo:
```bash
ssh pi@192.168.1.105
```

- Usuario por defecto: `pi`
- Contraseña por defecto: `raspberry`

3. Al conectarte por primera vez, aceptá la advertencia de autenticidad escribiendo `yes`.
4. Ingresá la contraseña cuando lo pida.

---

# 🛠️ Guía Post-Instalación para Raspberry Pi OS Lite

## 1. 🔄 Actualizar el sistema

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. 🔑 Cambiar contraseña del usuario `pi`

```bash
passwd
```

## 3. 🕒 Configurar zona horaria y localización

```bash
sudo raspi-config
```

- `1. System Options`
  - `S1 Locale` → `es_AR.UTF-8`
  - `S2 Timezone` → elegir tu región
  - `S4 Wireless LAN` → configurar Wi-Fi si no se hizo antes

## 4. 🧰 Instalar utilidades comunes

```bash
sudo apt install -y git curl vim htop net-tools unzip
```

## 5. 📁 Cambiar el hostname

```bash
sudo raspi-config
```

- `1. System Options` → `S4 Hostname` → definir un nombre de red como `indoor-server`

## 6. 🔒 Crear nuevo usuario y desactivar `pi` (opcional)

```bash
sudo adduser tu_usuario
sudo usermod -aG sudo tu_usuario
sudo passwd -l pi  # Opcional para bloquear 'pi'
```

## 7. 🌐 Configurar IP fija (opcional)

Editar:

```bash
sudo nano /etc/dhcpcd.conf
```

Agregar al final:

```conf
interface wlan0
static ip_address=192.168.1.100/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8 1.1.1.1
```

## 8. 🔁 Reiniciar para aplicar cambios

```bash
sudo reboot
```

