# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 3: Desarrollo

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
