# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 5: IoT

En el capítulo de IoT se instala ThingsBoard, plataforma que permite integrar dispositivos IoT para controlarlos, recibir y monitorizar datos. También se simula el envío de datos de un sensor de temperatura y se monitoriza por un panel de control definido en Thingsboard.

Raspberry se puede usar como servidor de ThingsBoard para pequeños proyectos o prototipos. Pero téngase en cuenta que para cierta carga de datos y usuarios conviene tener más potencia de hardware.

Al mismo tiempo Raspberry se puede usar como dispositivo IoT, enviar datos de ThingsBoard e incluso recibir órdenes desde ThingsBoard.

### ThingsBoard

Para la instalacción de ThingBoard en Raspberry seguir la documentación oficial: https://thingsboard.io/docs/user-guide/install/rpi/

Documentación de inicio: https://thingsboard.io/docs/getting-started-guides/helloworld/

### Sensores

En la clase de sensores simulamos el envío de datos de temperatura desde un script de Python, para no depender de un sensor de temperatura para realizar el ejemplo. Si dispones de un sensor de temperatura o de otro tipo, puedes adaptar el siguiente script a tus necesidades. Ten en cuenta que necesitas instalar las librerías y/o código necesario para controlar y obtener datos de tu sensor, y evidentemente eliminar toda la parte de generación de temperatura aleatoria y el envío de dato.

Es necesario instalar librería para enviar datos por protocolo *mqtt*. Si quieres usar protocolos HTTP o CoAP consulta la doc de ThingsBoard.
```
sudo pip install paho-mqtt
```

El script:

```
import os
import time
import sys
#import Adafruit_DHT as dht
import paho.mqtt.client as mqtt
import json
from random import randrange

THINGSBOARD_HOST = 'localhost'
ACCESS_TOKEN = 'DHT11_DEMO_TOKEN'

# Data capture and upload interval in seconds. Less interval will eventually hang the DHT22.
INTERVAL=2

sensor_data = {'temperature': 0}

next_reading = time.time() 

client = mqtt.Client()

# Set access token
client.username_pw_set(ACCESS_TOKEN)

# Connect to ThingsBoard using default MQTT port and 60 seconds keepalive interval
client.connect(THINGSBOARD_HOST, 1883, 90)

client.loop_start()

try:
    while True:
        temperature = 20 + randrange(10)
        sensor_data['temperature'] = temperature

        client.publish('v1/devices/me/telemetry', json.dumps(sensor_data), 1)

        next_reading += INTERVAL
        sleep_time = next_reading-time.time()
        if sleep_time > 0:
            time.sleep(sleep_time)
except KeyboardInterrupt:
    pass

client.loop_stop()
client.disconnect()
```

