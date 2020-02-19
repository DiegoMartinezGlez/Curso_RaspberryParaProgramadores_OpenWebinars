# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 2: Raspbian

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
