# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 2: Raspbian

### Configuración Raspberry :: raspi-config

Desde el escritorio de Raspbian puedes acceder a algunos parámetros de configuración de la Raspberry. Pero algunas opciones sólo están disponibles por línea de comando. Por eso disponemos de *raspi-config*: una aplicación sencilla de configuración.

Algunas de las opciones de configuración que hemos visto durante el curso:

- Opciones de red: especialmente útil si usamos Raspbian sin escritorio y queremos configurar una red inalámbria a la que conectarnos.
- Opciones de arranque: se puede configurar arranque en escritorio o en consola, y en ambos casos se puede configurar autologin o login obligatorio
- Opciones de interfaz: recuerda habilitar la interfaz que necesites para poder usar el bus para cámaras, acceso remoto con SSH y/o VNC, uso de SPI e I2C en la GPIO, entre otras opciones avanzadas que nos hemos visto en el curso
- Opciones avanzadas: contiene, entre otras cosas, configuración de audio (se pueder alternar entre HDMI, salida mini-jack, forzar alguna en concreto), de vídeo y la opción de forzar la expansión de la memoria de la tarjeta (especialmente interesante si flasheamos una imagen de backup de X Gb en una tarjeta de Z Gb, con X<Z)

### Configurar IP estática

El procedimiento consiste en configurar una IP estática para la Raspberry en una red DHCP (con asignación automática de IP). La mayoría de redes domésticas y routers son así por defecto. En redes corporativas puede complicarse el asunto, consultar al administrador de tu red en cualquier caso.

Básicamente la configuración consiste en editar un fichero del sistema en el que indicar la configuración de red. 

- Abrir un terminal
- Editar dhcpcd.conf:
```
sudo nano /etc/dhcpcd.conf
```
- Introducir las siguientes líneas:
```
ip_address=192.168.1.XX/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1
```

En el propio fichero podéis encontrar comentadas 3 líneas similares como ejemplo.
En *XX* podéis poner el número personalizado dentro de la red. El resto de números (192.168.1) puede variar en función del dominio de la red. Ante cualquier duda consulta al administrador de tu red.
