# Demo_SNMP
Demostracion SNMP (OID Y MIB)
# Guía para instalacion SNMP 

En esta guía, aprenderás cómo instalar y configurar SNMP (Simple Network Management Protocol) en una máquina virtual (VM) con Ubuntu Server. SNMP es un protocolo ampliamente utilizado para monitorear y administrar dispositivos de red.

## Antes de comenzar como recomendacion utiliza estos comandos para evitar errores o atrasos.
```bash
sudo apt-get update
```
```bash
sudo apt-get upgrade
```
## Paso 1: Instalar SNMP en la VM

### 1.1. Iniciar la VM y Configurar Ubuntu Server

1. Inicia la VM y sigue las instrucciones de instalación de Ubuntu Server.
2. Configura una contraseña para el usuario root.

### Paso 2: Abrir una Terminal en la VM

Una vez instalado Ubuntu Server, abre una terminal en la VM.

### 2.3. Instalar el paquete SNMP

Ejecuta el siguiente comando para instalar el paquete SNMP:

```bash
sudo apt-get install snmpd snmp
```
### 2.4.  Configura SNMP editando el archivo de configuración con el siguiente comando:
```bash
sudo nano /etc/snmp/snmpd.conf
```
### 2.5. Añade la siguiente línea al archivo para permitir consultas SNMP desde cualquier dirección IP (esto es solo para propósitos de demostración, en un entorno real, limita el acceso):
```bash
rocommunity public
```
### 2.6. Reinicia el servicio SNMP:
```bash
sudo service snmpd restart
```
## Paso 3: Encuentra un OID y MIB
### 3.1.  Puedes explorar la estructura de los MIBs disponibles ejecutando el siguiente comando:
```bash
snmpwalk -v 2c -c public localhost
```
## Para hacer que SNMP sea accesible desde cualquier otro cliente en la red y no solo desde localhost, sigue estos pasos adicionales:
## Paso 4: Configuración de SNMP para Acceso desde Otros Clientes
### 4.1. Abre el archivo de configuración SNMP:
```bash
sudo nano /etc/snmp/snmpd.conf
```
## 4.2. Cambia la comunidad "public" por una comunidad más segura. Por ejemplo, puedes crear una comunidad llamada "mi_comunidad_segura" y definir una cadena de acceso adecuada, además, considera configurar restricciones de acceso basadas en direcciones IP para limitar el acceso solo a las máquinas que deben tenerlo. Agrega una línea como esta para permitir el acceso solo a una dirección IP específica (reemplaza "xxx.xxx.xxx" con la dirección IP del cliente que deseas permitir):
```bash
access mi_comunidad_segura xxx.xxx.xxx
```
## 4.3 Cambia el agentaddress (127.0.0.1) por la direccion de interfaz de red (0.0.0.0) para que escuche en todas las interfaces.
## 4.4. Asegúrate de que tu firewall permita el tráfico SNMP desde otras máquinas en la red hacia esta máquina. Puedes abrir el puerto UDP 161 en tu firewall. (Realizarlo en las dos maquinas para seguridad)
```bash
sudo ufw allow 161/udp
```
### Este comando se usa en la pc cliente
```bash
snmpwalk -v2c -c comunidad 192.168.175.159 
```
## 4.5. Reinicia el servicio SNMP:
```bash
sudo service snmpd restart
```
## Paso 5: Descarga de MIBs y Buenas Prácticas de Seguridad

### 5.1. Para mejorar la comprensión de la información SNMP, es recomendable descargar y configurar los MIBs relevantes. Para hacerlo, instala el paquete "snmp-mibs-downloader":
```bash
sudo apt-get install snmp-mibs-downloader
```
## 5.2. Esto descargará y configurará una serie de MIBs que hacen que los datos SNMP sean más legibles.
### Recomendaciones 


## Como mencionamos anteriormente, es crucial cambiar la comunidad "public" por una comunidad más segura en el archivo de configuración "snmpd.conf" y configurar restricciones de acceso adecuadas.

## Además, asegúrate de que los clientes SNMP (ya sea en Ubuntu o Windows) utilicen la comunidad y las configuraciones de seguridad adecuadas al realizar consultas SNMP.

