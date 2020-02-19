# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 2: Raspbian

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
