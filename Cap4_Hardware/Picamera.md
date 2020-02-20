# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 4: Hardware

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
