# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 3: Desarrollo

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









