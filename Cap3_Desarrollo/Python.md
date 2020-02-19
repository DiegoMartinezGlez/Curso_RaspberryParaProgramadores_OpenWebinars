# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 3: Desarrollo

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



