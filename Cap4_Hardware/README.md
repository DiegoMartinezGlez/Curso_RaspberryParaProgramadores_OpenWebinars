# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 4: Hardware

En el capítulo de Hardware se realizan ejemplos de uso de las GPIO, picamera y setup de audio

### GPIO

Script de ejemplo de control de LED con GPIO:

```
from gpiozero import LED
from time import sleep

led = LED(17)

while True:
	led.on()
	sleep(1)
	led.off()
	sleep(1)

```

Script de ejemplo de control de sensor de temperatura:

```
import board
import digitalio
import busio
import time
from adafruit_bmp280 import Adafruit_BMP280_I2C

# Create library object using our Bus I2C port
i2c = busio.I2C(board.SCL, board.SDA)
bmp280 = Adafruit_BMP280_I2C(i2c)

# change this to match the location's pressure (hPa) at sea level
# bmp280.seaLevelhPa = 1013.25

while True:
    print("\nTemperature: %0.1f C" % bmp280.temperature)
    print("Pressure: %0.1f hPa" % bmp280.pressure)
    print("Altitude = %0.2f meters" % bmp280.altitude)
    time.sleep(2)
```

### Picamera

Script de prueba de picamera:
```
from picamera import PiCamera
from time import sleep

camera = PiCamera()

camera.start_preview()
sleep(5)
camera.stop_preview()
```

Rotar cámara:
```
from picamera import PiCamera
from time import sleep

camera = PiCamera()

camera.rotation = 0
camera.start_preview()
sleep(5)
camera.stop_preview()
sleep(1)
camera.rotation = 180
camera.start_preview()
sleep(5)
camera.stop_preview()
```

Obtener varias capturas y vídeo:
```
from picamera import PiCamera
from time import sleep
from datetime import datetime

camera = PiCamera()
camera.rotation = 180

print('Capturando imagenes ...')

for i in range(5):
	now = datetime.now()
	date_time_str = now.strftime("%d_%m_%Y_%H_%M_%S")
	sleep(1)
	camera.capture('/home/pi/Desktop/captures/'+date_time_str+'.jpg')

print('Capturando video ...')


now = datetime.now()
date_time_str = now.strftime("%d_%m_%Y_%H_%M_%S")

camera.start_recording('/home/pi/Desktop/captures/video_'+date_time_str+'.h264')
sleep(15)
camera.stop_recording()

print('Fin!')
```

### Audio setup

Asegurate de revisar configuración de audio en raspi-config para la salida de audio por HDMI / mini-jack.

Para acceder al setup de audio por línea de comando puede usar:
```
alsamixer
```

También por línea de comando puedes usar aplay/arecord para reproducir o grabar audio.

Antes de grabar identifica dispositivo/tarjeta:
```
arecord –l
```

Ejemplo de grabación de 10 segundos:
```
arecord -D hw:[cardNumber],[deviceNumber] -d 10 -f cd test.wav -c 1
arecord -D hw:1,0 -d 10 -f cd test.wav -c 1
```

Reproducir:
```
aplay test.wav
```



