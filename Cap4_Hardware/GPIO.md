# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 4: Hardware

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
