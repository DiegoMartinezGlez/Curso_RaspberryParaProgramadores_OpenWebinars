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
