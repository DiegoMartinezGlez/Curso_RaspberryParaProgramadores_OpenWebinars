# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 3: Desarrollo

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





