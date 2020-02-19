# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 2: Raspbian

### Acceso Remoto :: SSH / VNC

Antes de nada, revisa que en la configuración de Raspberry (raspi-config) la interfaz para SSH/VNC estén activadas.

Para acceder por SSH a la Raspberry, usa la línea de comando desde un sistema operativo/terminal que permita el comando SSH (las últimas versiones de Ubuntu/Windows/iOS lo permiten en el terminal del sistema a día de hoy).
```
ssh pi@192.168.1.2
```
Pedirá introducir contraseña del usuario *pi*. 192.168.1.2 es la supuesta IP de la Raspberry a la que acceder.

Para acceder por escritorio remoto, en lugar de por terminal como con SSH, podemos usar el protocolo VNC. Necesitaremos un cliente de VNC en desde un sistema operativo con escritorio. Para Ubuntu y Windows podéis usar VNCViewer: https://www.realvnc.com/es/connect/download/viewer/

El uso es muy sencillo. Introducid la IP de la Raspberry y conectar. Podéis guardar perfiles de Raspberry, cada uno con su IP y nombre.
