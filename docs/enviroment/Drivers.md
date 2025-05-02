## Problemas de conexión USB con placas Arduino o ESP32

En algunos casos, al conectar placas como Arduino UNO, Nano, ESP32 o ESP8266, puede que el sistema no detecte el puerto COM. Esto suele deberse a la falta de drivers necesarios para el chip conversor USB-Serial que integra la placa.

### ¿Qué drivers pueden ser necesarios?

#### CH340 / CH341
- Usados frecuentemente en **placas Arduino clonadas** o algunas placas ESP.
- Si al conectar tu placa no aparece el puerto en el IDE de Arduino, puede que estés usando una placa con este chip.
- Driver: [CH340/CH341 Driver](https://sparks.gogo.co.nz/ch340.html)

#### CP2102
- Común en algunas versiones de **ESP8266**, **ESP32** y módulos como NodeMCU.
- Driver: [CP2102 USB to UART Bridge VCP Drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

### ¿Cómo saber cuál necesitas?
- Podés **leer el chip impreso físicamente** en la placa (ejemplo: `CH340G`, `CP2102`, etc).
- Si no lo sabés, **podés instalar ambos drivers sin problemas**, ya que no se interfieren entre sí.

### Recomendación
Instalá estos drivers si:
- El **IDE de Arduino no muestra el puerto COM** después de conectar la placa.
- Ves un **dispositivo desconocido** en el Administrador de dispositivos de Windows.
- Recibís errores al intentar subir el código.

---

> ⚠️ Nota: Esta recomendación es especialmente útil si estás usando placas económicas o clones. Las placas oficiales de Arduino suelen ser reconocidas automáticamente por Windows o instalar su driver al conectar.

