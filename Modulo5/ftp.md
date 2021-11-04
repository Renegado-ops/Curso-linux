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

6.  [Desinstalacion](#desinstalacion)

## Introducción

## ¿Qué es un Servidor FTP?
En inglés, las siglas **FTP** significan “File Transfer Protocol”, que se traduciría como “Protocolo de Transferencia de Archivos”. El servicio FTP es un servicio utilizado para el envío y obtención de archivos entre dos equipos remotos.

Es un Protocolo de transferencia de archivos es un protocolo de red para la transferencia de archivos entre sistemas conectados a una red TCP, basado en la arquitectura cliente-servidor.

### Orígenes

El protocolo **FTP** fue propuesto por primera vez por Abhay Bhushan, del MIT, en abril de 1971 como un medio para transferir archivos grandes entre los diferentes sistemas que componían ARPANet, precursora de Internet.

Los puertos típicos utilizados para conectarse al FTP son el 20 y el 21 para la gran mayoría de los casos, aunque en algunos proveedores esto puede variar. Por lo general se usan dos tipos de transferencia: una es la ASCII y la otra es la de tipo Binario. La primera de estas solamente transfiere texto plano del tipo ASCII, como serían por ejemplo páginas HTML sin imágenes, mientras que la segunda clase se usa para transferir archivos como imágenes, audios, videos, etc.
## Instalación

1. Actualizamos los paquetes.
```bash
$ sudo apt update
```
2. A continuación, utilizando el siguiente código, instalamos vsftpd, escribimos:
```bash
$ sudo apt install vsftpd
```
3. Creamos una copia de seguridad del archivo original.
```bash
$ sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.original
```
##  Habilitamos el puerto para el tráfico FTP desde el firewall

una vez instalado el protocolo, empezamos la configuración:

1. Primero comprobamos el estado de nuestro firewall:
```bash
$ sudo ufw status
```
2. Vamos a agregar 4 reglas más las cuales abrirán puertos específicos para que funciones correctamente nuestro servidor FTP. Escribimos cada comando y damos Enter:
```bash
$ sudo ufw allow 20/tcp
```
3. Volvemos a comprobar el estado de nuestro firewall:
```bash
sudo ufw status
```
## Configuramos el archivo vsftpd.conf

1. Ahora vamos a editar y configurar el archivo vsftpd.conf, escribimos:
```bash
sudo nano /etc/vsftpd.conf
```
2. Ahora tenemos que habilitar la escritura, con la flecha de desplazamiento hacia abajo buscamos la línea  _#write_enable=YES_  y le quitamos el signo ‘#’, también nos aseguramos que local_enable=YES este descomentado:

3. También buscamos que Chroot este descomentado de esta manera el usuario conectado por FTP lo limitaremos a que solo acceda a los archivos de la carpeta permitida:

Guardamos los cambios con CTRL O para guardar, Enter para aceptar y CTRL X para salir. Agregamos al usuario al archivo que contiene la lista:

Reiniciamos vsftpd:

`sudo service vsftpd restart`

comprobamos el estado del servidor:

`sudo service vsftpd status`

## 4. Configuramos la seguridad del FTP
  
1. Creamos el certificado SSL:
```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem
```
2. Llenamos los datos que nos solicitan, al finalizar abrimos el archivo de configuración:
```bash
sudo nano /etc/vsftpd.conf
```
3. Nos desplazamos al final del archivo y comentamos las siguientes líneas con un ‘#’.
Una vez que comentamos estas dos líneas, vamos al final del archivo y agregamos las siguiente líneas:
  `rsa_cert_file=/etc/ssl/private/vsftpd.pem`  
`rsa_private_key_file=/etc/ssl/private/vsftpd.pem`

4. Dentro del archivo buscamos ssl_enable y cambiamos su valor a YES:
  ssl_enable=YES
Agregamos las siguientes líneas al final del archivo:
`allow_anon_ssl=NO`  
`force_local_data_ssl=YES`  
`force_local_logins_ssl=YES`

5. Configuramos el servidor para que use TLS agregando al final del archivo:
`ssl_tlsv1=YES`  
`ssl_sslv2=NO`  
`ssl_sslv3=NO`

  6. Por último agregamos:
`require_ssl_reuse=NO`  
`ssl_ciphers=HIGH`

7. Guardamos los cambios y reiniciamos el servidor:

sudo systemctl restart vsftpd
## 5. Obtenemos la IP del servidor

  Para ver la ip de nuestro servidor necesitamos instalar una herramienta llamada net-tools:

`sudo apt install net-tools`

Una vez que termine la instalación buscamos la IP de nuestro servidor:

`ifconfig`

## Desinstalación

Para eliminar a ftp ponemos el siguiente comando

``` bash
sudo apt-get --purge remove vsftpd

```

Listo🔥