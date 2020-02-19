# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 2: Raspbian

### Algunos métodos abreviados de teclado:

Abrir terminal (desde escritorio):
```
Ctrl + Alt + T
```

Salir de escritorio:
```
Ctrl + Alt + F1
```

Iniciar escritorio:
```
startx
```

Copiar/pegar en terminal:
```
Ctrl + Alt + C
Ctrl + Alt + V
```

### apt-get :: Advanced Packaging Tool:

Para instalar paquetes/liberías/aplicaciones en Raspbian, se usa el gestor de paquetes heredado de Debian: *apt-get*

Actualiza el índice de paquetes:
```
sudo apt-get update
```

Actualiza los paquetes:
```
sudo apt-get upgrade
```

Instala un paquete:
```
sudo apt-get install [paquete]
```

Instala varios paquetes:
```
sudo apt-get install [paquete1] [paquete2] … [paqueteN]
```

Instala versión específica de un paquete:
```
sudo apt-get install gparted=0.16.1-1
```


Elimina un paquete:
```
sudo apt-get remove [paquete]
```

Elimina un paquete y posible configuración relacionada (ej.: Apache, MySql):
```
sudo apt-get purge [paquete]
```

Elimina paquetes temporales que se necesitaron sólo en tiempo de instalación:
```
sudo apt-get autoremove
```

Ayuda:
```
sudo apt-get -h
```

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

### Acceso Remoto :: SSH / VNC

Antes de nada, revisa que en la configuración de Raspberry (raspi-config) la interfaz para SSH/VNC estén activadas.

Para acceder por SSH a la Raspberry, usa la línea de comando desde un sistema operativo/terminal que permita el comando SSH (las últimas versiones de Ubuntu/Windows/iOS lo permiten en el terminal del sistema a día de hoy).
```
ssh pi@192.168.1.2
```
Pedirá introducir contraseña del usuario *pi*. 192.168.1.2 es la supuesta IP de la Raspberry a la que acceder.

Para acceder por escritorio remoto, en lugar de por terminal como con SSH, podemos usar el protocolo VNC. Necesitaremos un cliente de VNC en desde un sistema operativo con escritorio. Para Ubuntu y Windows podéis usar VNCViewer: https://www.realvnc.com/es/connect/download/viewer/

El uso es muy sencillo. Introducid la IP de la Raspberry y conectar. Podéis guardar perfiles de Raspberry, cada uno con su IP y nombre.

### Gestión de usuarios

La gestión de usuario y permisos implica usuarios y grupos, para poder agrupar permisos y facilitar la gestión. Así que tenemos que tener en cuenta en la gestión de usuarios dos entidades: usuarios y grupos.

Comandos de gestión de usuarios para ejecutar desde un terminal:

Listar grupos
```
groups
```
Listar grupos de un usuario
```
groups usuario
```
Crear usuario
```
sudo adduser nuevo_usuario
```
Eliminar usuario
```
sudo userdel usuario
```
Eliminar usuario y borrar su carpeta de usuario
```
sudo userdel -r usuario
```
Añadir usuario de un grupo
```
sudo adduser usuario
```
Eliminar usuario de un grupo
```
sudo deluser usuario grupo
```
Cambiar de usuario
```
sudo su usuario
```

### Python

Raspbian viene con dos versiones de Python instaladas por defecto: 2.7 y 3.7. Cada una se ejecuta respectivamente con los comandos *python* y *python3*. Ejemplos de ejecución de script con cada versión:
```
python script.py
python3 script.py
```

En internet puedes encontrar scripts o programas para ambas versiones. Así que puede ser necesario acostumbrarse a convivir con ambas. Más adelante veremos como poder tener entornos virtuales de Python y poder tener incluso más versiones de Python y de otras librerías.

Para instalar librerías de Python se usa el gestor de paquetes *pip* para Python2 o *pip3/ para Python3. Se pueden instalar con:
```
sudo apt install python-pip
sudo apt install python3-pip
```
Ejemplo de uso:
```
pip install flask
pip3 install flask
```

Para gestionar entornos virtuales de Python instala *virtualenv* y *virtualenvwrapper*:
```
sudo apt-get install virtualenv virtualenvwrapper
```

Crear entorno:
```
mkvirtualenv demoenv
```
Salir de entorno:
```
deactivate
```
Activar entorno:
```
workon demoenv
```
Para crear un entorno con una versión de Python concreta, indica la ruta de la instalación de Python en la Raspberry:
```
mkvirtualenv --python=/usr/bin/python3 demoenv3
```
