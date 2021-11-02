#Manual de Instalacion y Configuracion de Samba


> Este manual fue realizado por para las personas que no saben buscar

**Creditos**
a mi esfuerzo exhaustivo de busqueda de Internet

*Este manual es incomporable*

´´´bash
$ sudo xd
´´´



# Manejo de Sistema Operativo Linux
Este curso es el Técnico en informática de INFOTEP-Noviembre 2021

#### Módulos(...de GNU/Linux)

1. Instalación
2. Configuración
3. Manejo...
4. Instalación de Servicios de Red... 
5. Administración de Servicios de Red...
![img](https://cdn.freebiesupply.com/logos/large/2x/samba-logo-png-transparent.png)

# Manual de Instalación y Configuración de Samba

  
  

> Este manual fue realizado por para las personas que no saben buscar

  

**Créditos**

a mi esfuerzo exhaustivo de búsqueda de Internet

*Este manual es incomparable*
```bash
s $ sudo xd
```



 Índice
 
1. [Introduccion a Samba](#introduccion)
2. [Instalacion](#instalacion)

 ## Introducción
 ## ¿Qué es Samba?

Es un conjunto de aplicaciones Linux, basada en el protocolo SMB[^1], que permite compartir archivos en red.
### Orígenes
Fue creado por Andrew Tridgell.
El necesitaba montar un espacio en disco en su computadora para un servidor Unix.

Esa computadora utilizaba el sistema de archivos NFS (*Network File System*). Sin embargo, una aplicación necesitaba soporte para el protocolo NetBIOS[^2] (no soportado por el NFS).

Tridgell lo solucionó escribiendo un sniffer^3] que permitía analizar el tráfico de datos generado por el protocolo NetBIOS. Hizo [ingeniería inversa en el protocolo SMB y lo implementó en el Unix.

 ## Instalación
 1. Actualizamos los paquetes.
```bash
$ sudo apt update
```
2. A continuación, utilizando el siguiente código, instalamos Samba.
 ```bash
$ sudo apt-get install samba
```
3. Con el siguiente comando podemos ver el estatus de samba.
 ```bash
$ sudo systemctl status nmbd
```
 
 ## Configuración de Servidor Samba
 una vez instalado el samba, empezamos la configuración
 1. creamos el directorio /samba
  ```bash
$ sudo mkdir /samba
```
2.  hacemos una copia para tener mas seguridad, estos archivos son importantes, no se pueden instalar o descargar de nuevo.
 ```bash
$ sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.original
```
3. con nano debemos entrar en el fichero siguiente
  ```bash
sudo nano /etc/samba/smb.conf
```
4.  añadir las siguientes líneas al final del fichero
 ```bash
[samba-share]
comment = Samba on Ubuntu
path = /samba
read only = no
browsable = yes
```
 ## Desinstalación
  
 Listo🔥
 
 [^1]: Server Message Block
[^2]: Network Basic Input/Output System
[^3]: Pequeño programa para captura de tráfico de datos en red