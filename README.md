# Demo_SNMP
Demostracion SNMP (OID Y MIB)
# Guía para instalacion SNMP 

En esta guía, aprenderás cómo instalar y configurar SNMP (Simple Network Management Protocol) en una máquina virtual (VM) con Ubuntu Server. SNMP es un protocolo ampliamente utilizado para monitorear y administrar dispositivos de red.

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
