# Manejo de Sistema Operativo Linux

  

Este curso es el Técnico en informática de INFOTEP-Noviembre 2021

  

  

#### Módulos(...de GNU/Linux)

  

  

1. Instalación.

  

2. Configuración.

  

3. Manejo.

  

4. Instalación de Servicios de Red.

  

5. Administración de Servicios de Red.

  

![img](https://nitrocdn.com/IYsgtimmdaIUwALCBttboEoaVLxVtCEY/assets/static/optimized/rev-bf47010/wp-content/uploads/elementor/thumbs/Como-funciona-el-protocolo-FTP-o1h0xe4trsdyfwb8sagoops4lvsx8yg8ujzuatpjxc.png)

  

  
  

# Manual de Instalacion y Configuracion de un servidor FTP

  
  
  

**Índice**

  
  

1.  [Introduccion](#instalacion)

2.  [¿Que es un Servidor FTP?](#queesunservidorftp)

3.  [Origenes](#origenes)

4.  [Instalacion](#instalacion)

5.  [Configuracion de Servidor FTP](#configuraciondeservidorftp)
6. [Desinstalacion](#desinstalacion)

  

## Introducción

  

## ¿Qué es un Servidor FTP?

  

  

Es un  Protocolo de transferencia de archivos es un protocolo de red para la transferencia de archivos entre sistemas conectados a una red TCP, basado en la arquitectura cliente-servidor.

  

### Orígenes

El protocolo **FTP** fue propuesto por primera vez por Abhay Bhushan, del MIT, en abril de 1971 como un medio para transferir archivos grandes entre los diferentes sistemas que componían ARPANet, precursora de Internet.



Fue creado por Andrew Tridgell.

Tridgell lo solucionó escribiendo un sniffer[^3] que permitía analizar el tráfico de datos generado por el protocolo NetBIOS. Hizo [ingeniería inversa en el protocolo SMB y lo implementó en el Unix.

  

  

## Instalación

  

1. Actualizamos los paquetes.

  

```bash

  

$ sudo apt update

  

```

  

2. A continuación, utilizando el siguiente código, instalamos Samba.

  

```bash

  

$ sudo apt-get install samba*

  

```

  

3. Con el siguiente comando podemos ver el estatus de samba.

  

```bash

  

$ sudo systemctl status nmbd

  

```

  

## Configuración del Servidor FTP

  

una vez instalado el samba, empezamos la configuración

  

1. creamos el directorio /samba

  

```bash

  

$ sudo mkdir /home/sharedfolder

  

```

  

2. hacemos una copia para tener mas seguridad, estos archivos son importantes, no se pueden instalar o descargar de nuevo.

  

```bash

  

$ sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.original

  

```

  

3. con nano debemos entrar en el fichero siguiente

  

```bash

  

sudo nano /etc/samba/smb.conf

  

```

  

4. añadir las siguientes líneas al final del fichero

  

```bash

  

[samba-share]

  

comment = Samba on Ubuntu

  

path = /home/sharedfolder

  

read only = no

  

browsable = yes

  

```

5. Guardamos los cambios con las teclas Ctrl + O y salimos del editor con las teclas Ctrl + X.

  

6. Reiniciamos el servicio de Samba con el siguiente comando:

```bash

sudo service smbd restart

```

  

7. Creamos el usuario root para Samba y otorgamos permisos. este paso puede ser omitido si asi usted desea.

```bash

sudo smbpasswd -a root

```

8. Es **importante** conceder los permisos en el Firewall del sistema con el comando:

```bash

sudo ufw allow samba

```

9. Con el comando ``` ip add ``` validamos la dirección IP de Ubuntu 21.04:

  

10. Vamos a Windows 10 y abrimos (Cmd o Ejecutar)

  

Con a combinacion de teclas: Windows + R

  

> La IP que se encuentra en nuestro ubuntu, la ponemos en windows

  

ponemos nuestra ip de linux en la CMD

  

** \\\192.0.0.0.1\compartido **

  

Esto abriria la ubicacion de donde se encuentra nuestro archivo o carpeta compartida, pedira contrasena, solo si le han puesto una.

## Desinstalación

Para eliminar a sambas ponemos el siguiente comando

  

``` bash

sudo apt-get remove --purge samba

```

Listo🔥

  

[^1]: Server Message Block

  

[^2]: Network Basic Input/Output System

  

[^3]: Pequeño programa para captura de tráfico de datos en red