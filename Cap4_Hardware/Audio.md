# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 4: Hardware

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



