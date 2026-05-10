# TRABAJO PRACTICO COMPUTACION APLICADA  2026
# GRUPO 6 
# INTEGRANTES:
# DE PAULA CARVALHO,  REGES ANTONIO 
# GALLARDO, CARLOS 
# JARA LOTO, CATALINA
# RUSCITTI, GIOVANNI FRANCO
# SUAREZ, TIZIANO 

# Descripción del Proyecto

Trabajo Práctico Integrador de la materia Computación Aplicada - UP .

El presente Proyecto se centra en la configuración y administración de un servidor GNU/Linux basado en **Debian 11 ("Bullseye")**, alojado en una máquina virtual.

La implementación abarca desde la configuración inicial del sistema y la red hasta el despliegue de servicios esenciales, la gestión del almacenamiento, la automatización de tareas y la creación de un sistema robusto de copias de seguridad.

**Hostname del Servidor:** `TPServer`

---

# Arquitectura y Servicios Configurados

Se ha implementado una arquitectura de servidor estándar con los siguientes componentes y servicios:

**Sistema Operativo:** Debian 11 (Bullseye)
**Servicio de Acceso Remoto:** `OpenSSH Server` configurado para autenticación segura mediante par de claves (pública/privada), deshabilitando el login por contraseña para `root`.
**Servidor Web:** `Apache2` con soporte para `PHP 7.4`, sirviendo un sitio de monitoreo desde una partición dedicada.
**Base de Datos:** `MariaDB Server`, con una base de datos de ejemplo cargada.
**Programador de Tareas:** `Cron` para la ejecución automatizada de scripts de backup.
**Red:** Configuración de red con **IP estática** para garantizar la conectividad constante desde la red física.
**Almacenamiento:** Gestión de un disco adicional con particiones dedicadas para el sitio web (`/www_dir`) y los backups (`/backup_dir`), montadas automáticamente al inicio.

---

# Repositorio y Entregables

Este repositorio contiene los siguientes archivos comprimidos, que representan las configuraciones y datos clave del servidor `TPServer`:

* root.tar.gz`: Directorio `/root`, incluyendo el historial de comandos, scripts de configuración y la clave pública SSH autorizada
* `etc.tar.gz`: Directorio `/etc`, con todos los archivos de configuración de los servicios (SSH, Apache, Red, fstab, etc.)
* `opt.tar.gz`: Directorio `/opt`, donde se aloja el script de backup principal.
* `proc.tar.gz`: Contiene el archivo `particion`, una copia persistente de la información de las particiones del sistema.
* `www_dir.tar.gz`: Directorio `/www_dir`, con el código fuente del sitio web (`index.php` y `logo.png`)
* `backup_dir.tar.gz`: Directorio `/backup_dir`, que almacena las copias de seguridad generadas.
* `var_splitted/`: Carpeta que contiene el directorio `/var` dividido en partes (`var_part_aa`, `var_part_ab`, etc.) para facilitar su subida a repositorios con límites de tamaño de archivo.

---
# Diagrama Topologico de la Infraestructura

+--------------------------+
|      Máquina Física      |
|       (PC GRUPO 6)       |
| IP: 192.168.100.83 (Host)|
+--------------------------+
             |
             | (Adaptador Puente)
             |
+--------------------------+     +------------------+     +----------------+
|     Máquina Virtual      |<--->|  Router/Gateway  |<--->|    Internet    |
|        (TPServer)        |     | IP: 192.168.100.1|     +----------------+
|--------------------------|     +------------------+
|      - Debian 11         |
|  - IP: 192.168.100.50    |
| - Mask: 255.255.255.0    |
|  - GW: 192.168.100.1     |
| - SSH, Apache, MariaDB   |
+--------------------------+
