# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 3: Desarrollo

En este capítulo del curso abordamos el desarrollo de ejemplos de sencillos de *backend* con Python y con NodeJS. En concreto y en cada caso, se despliega una API con varios métodos HTTP, con ejemplo de cómo ejecutar scripts .sh desde el código.

Adicionalmente se aborda también la instalación de Apache + Wordpress y Tomcat + Jenkins, para ver la instalación de estos servidores y el despliegue de dos herramientas comunes.

Finalmente se realiza la configuración de un repositorio git en una Raspberry.

### Python

Para editar Python en Raspberry puedes usar *nano* por línea de comando o Geany en entorno de escritorio. Crea ficheros con extensión .py para tus scripts y ejecutalos con *python/python3 nombre_script.py*.

Para desplegar un servidor o servicio con Python podemos usar Flask. Instala Flask con:
```
pip/pip3 install Flask
```

Con el siguiente código podemos desplegar
```
import flask
 
app = flask.Flask(__name__)
 
@app.route('/')
def index():
    return "Hello, FlaskWorld!"
 
if __name__ == '__main__':
    app.run(debug=True, host="192.168.1.150", port=8081)
```

Sustituye 192.168.1.150 por la IP desde donde se vaya a ejecutar el script.

Ejecuta con *python3 nombre_script.py"

Podrás llamar al método HTTP con la url: http://192.168.1.150:8081 (sustituye en adelante 192.168.1.150 por la IP concreta de tu Raspberry). Si la cargas en navegador, devolverá "Hello, FlaskWorldk!".

Para añadir métodos concretos y recibir parámetros por request, el siguiente código nos brinda un ejemplo:
```
@app.route('/runTask')
def runTask():
    task = flask.request.args.get('task')
    if task is None or task=="":
        return "Especifica task: /runTask?task=XXX"
    else:
        return "Tarea a ejecutar: " + task
```

Con esta función, tenemos disponible un nuevo método *runTask*, que espera un parámetro "task". Al hacer la llamada  http://192.168.1.150:8081/runTask?task=XQW devolverá "Tarea a ejecutar: XQW".

Con estos dos sencillos ejemplos, vemos cómo podemos montar una API donde gestionar diferentes órdenes a la Raspberry. Y desde este sericio podemos usar la cámara, leer información o controlar dispositivos por GPIO, ejecutar script .sh, acceder a una base de datos, conectar con otra API, ...

Para ver el ejemplo de ejecutar scripts .sh, script completo:
```
import flask
from subprocess import call

app = flask.Flask(__name__)

@app.route('/')
def index():
    return "Hello, FlaskWorld!"

@app.route('/runTask')
def runTask():
    task = flask.request.args.get('task')
    if task is None or task=="":
        return "Especifica tarea: /runTask?task=XXX"
    elif task=="1":    
        rc = call("./task.sh", shell=True)
        #print(rc)
        return "Tarea 1 ejecutada!"
    elif task=="2":    
        rc = call("./task.sh", shell=True)
        #print(rc)
        rc = call("echo \""+task+"\"", shell=True)
        #print(rc)
        return "Tarea 2 ejecutada!"
    else:
        return "Especifica tarea: 1, 2"

if __name__ == '__main__':
    app.run(debug=True, host="192.168.1.150", port=8080)
```

### NodeJS

Necesitarás instalar nodejs y npm en raspbian antes de nada:
```
sudo apt install nodejs npm
```

npm es el gestor de paquetes de nodejs. Lo usaremos para inicializar el proyecto y para instalar paquetes.

Crea un directorio y dentro de él, por línea de comando, ejecuta:
```
npm init
```

Instala express:
```
npm install --save express
```

Seguir wizard y al terminar, crea fichero index.js y añádele el siguiente contenido:
```
const express = require('express');
const app = express();
const shell = require('shelljs')

app.get('/', function(req, res){
   console.log('request!');
   res.send("express server");
});

app.get('/task', function(req, res){
   console.log('task request!');
   shell.exec('./task.sh')
   res.send("express server: task");
});

app.listen(3000);
```

Crea un fichero task.sh en el proyecto que ejecute alguna tarea simple para usar como ejemplo (ej.: echo "ejecutando tarea ..."). Darles permisos de ejecución. Levanta el servicio de express con "node index.js" y podrás acceder por HTTP a los métodos "/" y "/task" desde la IP de tu Raspberry (ej.: http://192.168.1.150:3000/task).

### Apache + PHP + MYSQL + WORDPRESS

Instalar apache:
```
sudo apt install apache2 -y
```

Instalar mysql:
```
sudo apt-get install mysql-server php-mysql -y
sudo apt-get install mariadb-server-10.0 php-mysql -y
sudo service apache2 restart
```

Instalar PHP:
```
sudo apt install php libapache2-mod-php -y
```

Instalar Wordpress: ir a /var/www/html/
```
sudo wget http://wordpress.org/latest.tar.gz
sudo tar xzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
sudo chown -R www-data: .
```

Configurar MySQL:
```
sudo mysql_secure_installation
```
Al terminar crear base de datos para Wordpress:
```
sudo mysql -uroot -p
create database wordpress;
GRANT ALL PRIVILEGES ON wordpress.* TO 'root'@'localhost' IDENTIFIED BY 'wordpress';
```

Reiniciar apache (sudo service apache2 restart) y cargar la IP de las Raspberry en el navegador (ej.: http://192.168.1.150)

Verás disponible el wizard de configuración de Wordpress para conectar con la base de datos y empezar a gestionar Wordpress.

### Tomcat + Jenkins

Instalar tomcat:
```
sudo apt-get install tomcat8
```

Al instalarse tomcta se despliega como servicio. Puedes ver log mientras se despliega con:
```
tail -400f /var/log/tomcat8/catalina.out
```

Tras instalación, puedes parar, arrancar, reiniciar o compronbar status por línea de comando:
```
sudo systemctl stop tomcat8.service
sudo systemctl start tomcat8.service
sudo systemctl restart tomcat8.service
sudo systemctl status tomcat8.service
```

Descarga jenkins: https://jenkins.io/download

Copia archivo .war a carpeta de aplicaciones de tomcat (puede que las rutas cambien, contrasta nombre de fichero .war y ruta de descarga en tu Raspberry):
```
sudo cp /home/pi/Downloads/jenkins.war /var/lib/tomcat8/webapps
```

Para evitar errores en el despliegue, otorga permisos al usuario de tomcat y reinicia servicio:
```
cd /var/lib/tomcat8/ 
sudo chown tomcat8 tomcat8/
sudo systemctl restart tomcat8.service
```

Reiniciar tomcat y acceder a jenkins tras despliegue (monitorizar log) en la url: http://localhost:8080/jenkins/ (desde la raspberry, http://{raspi_ip}:8080/jenkins/ desde fuera).

### Repositorio git

Para montar un repositorio git en Raspberry es necesario instalar *git-core*:
```
sudo apt-get install wget git-core
```

Crea usuario git (para ejemplo, contraseña también "git"):
```
sudo adduser git 
```

Cambia a usuario git:
```
sudo su git
```

Crea carpeta e inicializala como repositorio sin nada:
```
mkdir gitpi-server.git
cd gitpit-server.git/
git init --bare
```

Ahora podemos configurar esa carpeta como escritorio remoto con git. Puedes usar la propia Raspberry u otra máquina. Crea una carpeta y desde dentro, por línea de comando:
```
git remote add pi-repo git@192.168.1.150:/home/git/gitpi-server.git
```

Crea algún fichero en la carpeta, has commit y push para probar el repositorio. Si quieres clonar el repositorio:
```
git clone git@192.168.1.150:/home/git/gitpi-server.git
```
