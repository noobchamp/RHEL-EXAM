# RHCSA Rapid Track - Preparación Completa para el Examen RHCSA (RHEL 9)

- [RHCSA Rapid Track - Preparación Completa para el Examen RHCSA (RHEL 9)](#rhcsa-rapid-track---preparación-completa-para-el-examen-rhcsa-rhel-9)
  - [1. Acceso a los sistemas y obtención de soporte](#1-acceso-a-los-sistemas-y-obtención-de-soporte)
    - [Edición de archivos de texto desde el prompt de shell (Vim)](#edición-de-archivos-de-texto-desde-el-prompt-de-shell-vim)
    - [Configuración de autenticación basada en claves SSH](#configuración-de-autenticación-basada-en-claves-ssh)
    - [Creación de un informe de diagnóstico](#creación-de-un-informe-de-diagnóstico)
  - [2. Gestión de archivos desde la línea de comandos](#2-gestión-de-archivos-desde-la-línea-de-comandos)
    - [Comandos básicos de gestión de archivos](#comandos-básicos-de-gestión-de-archivos)
  - [3. Gestión de usuarios y grupos locales](#3-gestión-de-usuarios-y-grupos-locales)
    - [Creación y administración de usuarios](#creación-y-administración-de-usuarios)
  - [4. Control de acceso a archivos](#4-control-de-acceso-a-archivos)
    - [Gestión de permisos de archivos](#gestión-de-permisos-de-archivos)
    - [Permisos especiales](#permisos-especiales)
  - [5. Gestión de la seguridad de SELinux](#5-gestión-de-la-seguridad-de-selinux)
    - [Modificación de los modos de SELinux](#modificación-de-los-modos-de-selinux)
    - [Crear una nueva etiqueta](#crear-una-nueva-etiqueta)
    - [Ajuste de booleanos de SELinux](#ajuste-de-booleanos-de-selinux)
    - [Comando clave](#comando-clave)
  - [6. Ajuste del rendimiento del sistema](#6-ajuste-del-rendimiento-del-sistema)
    - [Finalización y monitoreo de procesos](#finalización-y-monitoreo-de-procesos)
    - [Tuned](#tuned)
  - [7. Programación de tareas futuras](#7-programación-de-tareas-futuras)
    - [Uso de cron](#uso-de-cron)
    - [Archivos temporales](#archivos-temporales)
  - [8. Instalación y actualización de paquetes de software](#8-instalación-y-actualización-de-paquetes-de-software)
    - [Gestión de paquetes con DNF](#gestión-de-paquetes-con-dnf)
  - [9. Gestión de almacenamiento básico](#9-gestión-de-almacenamiento-básico)
    - [Montaje de sistemas de archivos](#montaje-de-sistemas-de-archivos)
    - [Crear particiones de disco](#crear-particiones-de-disco)
  - [10. Gestión de la pila de almacenamiento](#10-gestión-de-la-pila-de-almacenamiento)
    - [Creación de volúmenes lógicos](#creación-de-volúmenes-lógicos)
  - [11. Servicios de control y proceso de arranque](#11-servicios-de-control-y-proceso-de-arranque)
    - [Control de servicios](#control-de-servicios)
    - [Configuración de un target](#configuración-de-un-target)
      - [Comandos clave](#comandos-clave)
    - [Restablecer contraseña de root](#restablecer-contraseña-de-root)
  - [12. Análisis y almacenamiento de registros](#12-análisis-y-almacenamiento-de-registros)
    - [Rsyslog](#rsyslog)
    - [Journalctl](#journalctl)
    - [Timedatectl](#timedatectl)
  - [13. Gestión de redes](#13-gestión-de-redes)
    - [Configuración de redes desde la línea de comandos](#configuración-de-redes-desde-la-línea-de-comandos)
      - [Validación](#validación)
      - [Configuración](#configuración)
      - [Resolución de nombres](#resolución-de-nombres)
  - [14. Acceso al almacenamiento conectado a la red](#14-acceso-al-almacenamiento-conectado-a-la-red)
    - [Gestión de almacenamiento NFS](#gestión-de-almacenamiento-nfs)
  - [15. Gestión de la seguridad de redes](#15-gestión-de-la-seguridad-de-redes)
    - [NFS](#nfs)
    - [AutoFS](#autofs)
    - [Firewalld y Selinux](#firewalld-y-selinux)
  - [16. Ejecución de contenedores](#16-ejecución-de-contenedores)
    - [Uso de contenedores](#uso-de-contenedores)
      - [Aislamiento de contenedores](#aislamiento-de-contenedores)
        - [Ajustar permisos con `podman unshare`](#ajustar-permisos-con-podman-unshare)
        - [Montar el volumen en el contenedor](#montar-el-volumen-en-el-contenedor)
    - [Crear una red](#crear-una-red)
    - [Gestión de contenedores como servicios del sistema](#gestión-de-contenedores-como-servicios-del-sistema)
      - [Ejecución independiente del login](#ejecución-independiente-del-login)
  - [Repaso](#repaso)

---

## 1. Acceso a los sistemas y obtención de soporte

### Edición de archivos de texto desde el prompt de shell (Vim)

- **Comandos básicos de Vim**:
  - `vi filename`: Abre un archivo con vi (o vim si está instalado el paquete `vim-enhanced`).
  - Modo de inserción: `i` para entrar, `Esc` para salir.
  - Guardar y salir: `:wq`.
  - Salir sin guardar: `:q!`.

### Configuración de autenticación basada en claves SSH

- **Comandos clave**:
  - `ssh-keygen -f .ssh/key-with-pass`: Generar ficheros de claves.
  - `ssh-keygen -t rsa -b 2048`: Generar claves SSH de 2048.
  - `ssh-copy-id -i .ssh/key-with-pass.pub user@remotehost`: Copiar clave pública al servidor remoto.
  - `eval $(ssh-agent)`: Inicar ssh-agent. Con eval hacemos que las variables que imprime las insertemos directamente.
  - `ssh-add .ssh/key-with-pass`. Añadir la parafrase en caché para el archivo _key-with-pass_.

### Creación de un informe de diagnóstico

- **Comando**:
  - `sos report`. Reporte del nodo local.
  - `sos collect`. Reporte de un cluster.
  - `sos clean /var/tmp/sos-report.tgz`. Eliminar la información confidencial de un sos report.
  - `systemctl start cockpit.socket`. Iniciar la consola web cockpit.
  - `insights-client --register`. Registrar en insights.

---

## 2. Gestión de archivos desde la línea de comandos

### Comandos básicos de gestión de archivos

- **Comandos clave**:
  - `ln fichero.txt enalce_duro.txt`. Crear un enlace duro (tienen el mismo inodo).
  - `ln -s /home/user/fichero.txt /tmp/enlace_simbolico.txt`. Crear un enlace simbólico.

> [!TIP]
> `cd -P` te lleva al directorio real si lo ejecutas sobre un directorio "simbólico".
> Las comillas dobles (") interpretan variables mientras que comillas simple (') NO las interpretan.

---

## 3. Gestión de usuarios y grupos locales

### Creación y administración de usuarios

- **Comandos clave**:
  - `chage -d 0 cloudadmin10`: El usuario debe cambiar la contraseña en el próximo inico de sesión.
  - `usermod -L`: Bloquea la cuenta del usuario.
  - `usermod -U`: Desbloquea la cuenta.
  - `usermod -L -e 2022-08-14 cloudadmin10`: Bloquear la cuenta el día 14/08/2022.
  - `usermod -s /sbin/nologin newapp`: Cuenta sin login.

Opciones del comando usermod:

| Opción del comando usermod  | Descripción                                                                                                     |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------|
| `-a, --append`              | Se utiliza con la opción `-G` para agregar los grupos complementarios                                           |
| `-c, --comment COMMENT`     | Agregar el texto `COMMENT` en el campo de comentarios.                                                          |
| `-d, --home HOME_DIR`       | Especificar un directorio de inicio para la cuenta de usuario.                                                  |
| `-g, --gid GROUP`           | Especificar el grupo principal para la cuenta de usuario.                                                       |
| `-G, --groups GROUPS`       | Especificar una lista de grupos complementarios separados por comas para la cuenta de usuario.                  |
| `-L, --lock`                | Bloquear la cuenta de usuario.                                                                                  |
| `-m, --move-home`           | Mover el directorio de inicio del usuario a una nueva ubicación. Debe usarlo con la opción `-d`.                |
| `-s, --shell SHELL`         | Especificar una shell de inicio de sesión particular para la cuenta de usuario.                                 |
| `-U, --unlock`              | Desbloquear la cuenta de usuario.                                                                               |

chage -m 0 -M 90 -W 7 -I 14 sysadmin05:

- `-m 0`: Establece el **mínimo número de días entre cambios de contraseña**. Un valor de `0` significa que el usuario puede cambiar su contraseña en cualquier momento.  
- `-M 90`: Especifica el **máximo número de días que una contraseña puede ser utilizada**. La contraseña caducará después de 90 días.  
- `-W 7`: Define el **número de días de advertencia antes de la caducidad de la contraseña**. El usuario recibirá una notificación 7 días antes de que la contraseña expire.  
- `-I 14`: Establece el **número de días de inactividad permitidos después de la caducidad de la contraseña**. Si el usuario no cambia su contraseña en los 14 días posteriores a la caducidad, la cuenta será bloqueada.  


> [!TIP]
 Puedes cambiar la configuración de vigencia de la contraseña predeterminada en el archivo /etc/login.defs. Las opciones PASS_MAX_DAYS y PASS_MIN_DAYS establecen la antigüedad máxima y mínima predeterminada de la contraseña, respectivamente. PASS_WARN_AGE define el período de advertencia predeterminado de la contraseña.

---

## 4. Control de acceso a archivos

### Gestión de permisos de archivos

- **Comandos clave**:
  - `chmod`: Cambiar permisos de archivos.
  - `chown`: Cambiar propietario de archivos.
  - `umask`: Configurar permisos predeterminados.

### Permisos especiales

- **SUID (Set User ID):**  
  Permite que un programa se ejecute con los permisos del propietario del archivo en lugar del usuario que lo ejecuta.  
  **Se aplica a:** Archivos ejecutables.  
  **Uso típico:** Programas que necesitan privilegios elevados, como `passwd`.  
  **Cómo funciona:** Si un archivo tiene SUID activo y es ejecutado por un usuario, el proceso se ejecutará con los permisos del propietario del archivo.  
  **Ejemplo:**  

  ```bash
  -rwsr-xr-x 1 root root 12345 /usr/bin/passwd
  ```  

  La "s" en los permisos del propietario indica que el bit SUID está activo.  
  **Comando para establecer SUID:**  

  ```bash
  chmod u+s archivo
  ```

- **SGID (Set Group ID):**
  En archivos ejecutables, permite que el programa se ejecute con los permisos del grupo propietario. En directorios, asegura que los nuevos archivos creados hereden el grupo del directorio.  
  **Se aplica a:** Archivos ejecutables y directorios.  
  **Uso típico:**  
  - En archivos ejecutables: Para ejecutar programas con permisos de grupo específicos.  
  - En directorios: Para compartir archivos con un grupo sin necesidad de cambiar manualmente el grupo de cada archivo.  
  **Cómo funciona:**  
  - En un archivo ejecutable: El proceso pertenece al grupo propietario del archivo, no al grupo del usuario.  
  - En un directorio: Los nuevos archivos o subdirectorios creados heredan el grupo propietario del directorio principal.  
  **Ejemplo:**  

  ```bash
  drwxrwsr-x 2 user grupo 4096 /shared
  ```  

  La "s" en los permisos del grupo indica que el bit SGID está activo.  
  **Comando para establecer SGID:**  

  ```bash
  chmod g+s archivo_o_directorio
  ```

- **Sticky Bit:**  
  Restringe el borrado de archivos en un directorio solo al propietario del archivo o a `root`.  
  **Se aplica a:** Directorios.  
  **Uso típico:** Directorios compartidos como `/tmp`.  
  **Cómo funciona:** Cuando Sticky Bit está activo en un directorio, solo el propietario del archivo (o root) puede eliminar o renombrar archivos dentro del directorio.  
  **Ejemplo:**  

  ```bash
  drwxrwxrwt 2 root root 4096 /tmp
  ```

  La "t" en los permisos de otros indica que el Sticky Bit está activo.  
  **Comando para establecer Sticky Bit:**  

  ```bash
  chmod +t directorio
  ```

---

## 5. Gestión de la seguridad de SELinux

**Estructura de selinux:**
  unconfined_u:object_r httpd_sys_content_t:s0 /var/www/html/File2
  user:role:type:security_level:file

### Modificación de los modos de SELinux

- **Comandos clave**:
  - `getenforce`, `setenforce`: Ver y cambiar el modo de SELinux.
  - `semanage fcontext`
  - `semanage fcontext -l`: Lista todos los contextos y path.
  - `semanage fcontext -l -C`: Listar solo las políticas creadas.
  - `restorecon`
  - `restorecon -Rv /var/www/`: Restaura el contexto recursivamente. -R [recursive] -v [verbose]
  - `chcon`

`chcon` permite cambiar en contexto de un fichero o directorio temporalmente (se usa de manera temporal para depurar), sin embargo, `restorecon`volverá a poner en contexto original.

```bash
mkdir /virtual
ls -Zd /virtual/
# unconfined_u:object_r:default_t:s0 /virtual/
chcon -t httpd_sys_content_t /virtual/
ls -Zd /virtual/
# unconfined_u:object_r:httpd_sys_content_t:s0 /virtual/
restorecon -v /virtual/
# Relabeled /virtual from unconfined_u:object_r:httpd_sys_content_t:s0 to unconfined_u:object_r:default_t:s0
```

>[!WARNING]
>Los archivos copiados cambian de contexto pero los archivos movidos no cambian de contexto.

>[!TIP]
>La expresión regular de los contextos más conocida es el `PIRATA` **(/.*)?**
>
>**/var/www/cgi-bin(/.*)?**
>
>Un conjunto de caracteres que comienza con una barra y va seguido de cualquier número de caracteres, donde el conjunto puede existir o no

### Crear una nueva etiqueta

Creamos un directorio nuevo. Posteriormente asignamos el contexto para ese directorio y aplicamos.

```bash
[root@central ~]$ mkdir /app
[root@central ~]$ ls -ldZ /app/
drwxr-xr-x. 2 root root unconfined_u:object_r:default_t:s0 6 ene 12 01:13 /app/
[root@central ~]$ semanage fcontext -a -t httpd_sys_content_t '/app(/.*)?'
[root@central ~]$ restorecon -Rv /app
Relabeled /app from unconfined_u:object_r:default_t:s0 to unconfined_u:object_r:httpd_sys_content_t:s0
[root@central ~]$ ls -ldZ /app/
drwxr-xr-x. 2 root root unconfined_u:object_r:httpd_sys_content_t:s0 6 ene 12 01:13 /app/
```

### Ajuste de booleanos de SELinux

Permite **habilitar/deshabilitar** funciones de selinux.

### Comando clave

- `getsebool -a`: Ver todas las políticas.
- `getsebool httpd_enable_homedirs`: Ver solo una política concreta
- `semanage boolean -l`: Ver todas las políticas. Además si están activas y arranque. Además de una breve descripción.
  - httpd_enable_homedirs  (apagado,apagado)  Allow httpd to enable homedirs.
- `semanage boolean -l -C`. Ver las políticas modificadas.
- `setsebool -P httpd_enable_homedirs on`: Establecer la política. **Con `-P` ES PERMANENTE**
- `ausearch -m AVC -ts recent`: Ver eventos recientes. -m [módulo AVC] ts recent [recientes].

---

## 6. Ajuste del rendimiento del sistema

### Finalización y monitoreo de procesos

- **Comandos clave**:
  - `kill`. kill -l para mostrar todas las señales disponible (-9 la más comun SIGKILL).
  - `pkill`. Matar todos los procesos asociados a un programa.
    - `pkill -SIGKILL -u usuario`.
  - `pgrep`. Ver los procesos con nombre.
  - `ptree`. Ver el árbol de procesos.
  - `kill`, `top`, `htop`: Gestionar procesos.
  - `systemctl status`: Ver estado de servicios.

>[!TIP]
>Los administradores suelen usar SIGKILL.
>Siempre es grave porque la señal SIGKILL no puede manipularse ni ignorarse.
>Sin embargo, obliga a la finalización sin permitir que el proceso terminado ejecute rutinas de autolimpieza.
>Red Hat recomienda enviar primero SIGTERM, a continuación intentar con SIGINT y, solo si falla en ambos casos, volver a intentar con SIGKILL.
---

### Tuned

Ajusta un perfil de rendimiento.
Puedes hacer un ajuste dinámico (según como el sistema esté funcionando en ese momento) en el archivo de configuración `cat /etc/tuned/tuned-main.conf`.

```bash
dynamic_tuning = 1
update_interval = 10
```

```bash
dnf install tuned
systemctl enable --now tuned
```

```bash
#VER EL PERFIL ACTUAL
[root@central]$ tuned-adm active
Current active profile: virtual-guest
```

Otros comandos:

- `tuned-adm list`: Listar perfiles.
- `tuned-adm profile_info`: Proporciona información del perfil actual.
- `tuned-adm profile otro_perfil`. Activar otro perfil.
- `tuned-adm recommend`. Te recomienda un perfil.
- `tuned-adm off`. Apagar tuned. Se reactiva aplicando un perfil.

## 7. Programación de tareas futuras

### Uso de cron

- **Comando clave**: `crontab -e`

### Archivos temporales

Crear un archivo de configuracion en `/etc/tmpfiles.d/archivo.conf`
```
d /run/momentary 0700 root root 30s
```

```bash
# Crear
systemd-tmpfiles --create /etc/tmpfiles.d/archivo.conf
# Limpiar
systemd-tmpfiles --clean /etc/tmpfiles.d/archivo.conf
```
---

## 8. Instalación y actualización de paquetes de software

### Gestión de paquetes con DNF

- **Comando clave**:
  - `dnf install package-name`: Instalar paquete.
  - `dnf list kernel`: Listar todos los paquetes kernel instalados y disponibles.
  - `dnf group list`: Nombre de grupos isntalados y disponibles.
  - `dnf group info "RPM Development Tools"`: Información de un grupo.
  - `tail -5 /var/log/dnf.rpm.log`: Ver log.
  - `dnf history`: Historial de instalaciones de paquetes.
  - `dnf history undo 2`: Revierte a un punto de la instalación.

---

## 9. Gestión de almacenamiento básico

### Montaje de sistemas de archivos

- **Comandos clave**:
  - `mount`, `umount`: Montar y desmontar sistemas de archivos.
  - `lsblk -fp`: Ver dispositivos de almacenamiento. -p [path] y -f _ver información del disco cono UUID_.
  - `parted /dev/vda print`: Imprimir particiones.
  - `parted /dev/sda unit s print`: Imprimir particiones por sectores. s [sector] b [bloque] Mib MB Gib GB.

### Crear particiones de disco
  
Crear la tabla de particiones y particiones.

```bash
[root@host ~]$ parted /dev/sdb mklabel [gpt] [msdos]
[root@host ~]$ parted /dev/sdb
GNU Parted 3.4
Using /dev/sdb
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) mkpart
# Para que el sistema lea la nueva particion
[root@host ~]$ udevadm settle
```

Todo junto:

- MSDOS: `parted /dev/vdb mkpart primary xfs 2048s 1000MB`.
- GPT: `parted /dev/vdb mkpart datos xfs 2048s 1000MB`.

Eliminación:

- Interactivo con parted, rm [numero], ejemplo: rm 2.
- `parted /dev/vdb rm 1`.
- Borrar el disco completo: wipefs -a /dev/sda

> [!IMPORTANT]
> Para crear particiones de **swap** debemos de usar el tipo de partición `linux-swap`. Para formatearlas con `mkswap`.
> En el FSTAB pondremos por defecto o con prioridad:
> UUID=39e2667a-9458-42fe-9665-c5c854605881   swap   swap   defaults   0 0
> UUID=39e2667a-9458-42fe-9665-c5c854605881   swap   swap   pri=10     0 0

---

## 10. Gestión de la pila de almacenamiento

### Creación de volúmenes lógicos

Aunque no es necesario, se puede crear particiones y marcarlas para LVM _set 1 lvm on_ donde "1" es el número de la partición.

```bash
parted /dev/sdb mklabel gpt mkpart primary 1MiB 769MiB
parted /dev/sdb mkpart primary 770MiB 1026MiB
parted /dev/sdb set 1 lvm on
parted /dev/sdb set 2 lvm on
fdisk -l /dev/sdb
/dev/sdb1      2048 1574911  1572864   768M Linux LVM
/dev/sdb2   1576960 2101247   524288   256M Linux LVM
```

Crear volumen VDO: `lvcreate --type vdo --name vdo-lv01 --size 5G vg01`.

> [!TIP]
> Arrancar en modo de emergencia por fallo del fstab: `systemd.unit=emergency.target`
---

## 11. Servicios de control y proceso de arranque

### Control de servicios

**Comando clave**:

- `systemctl start/stop/restart service-name`.
- `systemctl list-units --type=service`: Listar todos los servicios **activos**.
- `systemctl list-units --type=service`: Listar todos los servicios **activos y no activos**.
- `systemctl`: Unidades cargadas y activas.

### Configuración de un target

Se puede iniciar un target aislado `systemctl isolate multi-user.target`, siempre que tengan la propiedad **AllowIsolate=yes** cuando se ejecuta `systemctl cat graphical.target`.
Target Comunes:

- multi-user.target: Modo texto.
- graphical.target: Modo GUI.
- rescue.target: Para reparar el sistema.
- emergency.target: Componente mínimos.
  
#### Comandos clave

- `systemctl get-default`: Ver el target por defecto.
- `systemctl set-default graphical.target`: Establecer un target por defecto.

### Restablecer contraseña de root

- Arrancar y editar la entrada del kernel `rd.break`. Esto hace un quiebre del sistema antes de entregarlo a initramfs.
- `mount -o remount,rw /sysroot`.
- `chroot /sysroot`.
- `passwd root`.
- `touch /.autorelabel`.
- `exit`.

>[!TIP]
>Para habilitar una debug shell en el kernel durante el arranque incidia con `systemd.debug-shell`.

---

## 12. Análisis y almacenamiento de registros

### Rsyslog

Configuración de rsyslog, mensajes populares

- kern
- user
- mail
- auth

Nivel de criticidad:

- emerg
- crit
- alert
- info
- debug

Ejemplo de configuracion **authpriv.\*   /var/log/secure**.
Ejemplo de logger **logger -p user.debug "Log entry created on host"**.

### Journalctl

- -n5: Muestra las últimas 5 líneas.
- -f: follow.
- -p err: Muestra priridad error.
- -u ssh.service: Unidad ssh.
- --since today. Desde hoy.
- --since "2022-03-11 20:30" --until "2022-03-14 10:00": Desde X hasta X.
- --since "-1 hour": Desde hace una hora.
- --list-boots. Listar arranques.

Otros más especiales:

_COMM: nombre del comando.
_EXE: ruta hacia el archivo ejecutable para el proceso
_PID: PID del proceso.
_UID: UID del usuario que ejecuta el proceso.
_SYSTEMD_UNIT: unidad systemd que inició el proceso

Ejemplos:

- journalctl _SYSTEMD_UNIT=sshd.service _PID=2110
- journalctl _UID=81
- journalctl _PID=1

Los logs de journal son volátiles, se debe configurar en **/etc/systemd/journald.conf**. Para hacerlo persistente a los reinicios, se debe configurar el parámetro **Storage**:

- auto: Por defecto, si existe /var/log/journal. Entonces guarda los logs.
- persistent: Los guarda en /var/log/journal. Si no existe el directorio, lo crea.
- volatile: Almacena los diarios en el directorio /run/log/journal volátil.
- none: Sin registros.

### Timedatectl

- timedatectl list-timezones
- timedatectl set-timezone America/Phoenix
- timedatectl set-ntp [true] [false]
- chronyc sources -v

---

## 13. Gestión de redes

### Configuración de redes desde la línea de comandos

#### Validación

- ip link show: Ver las interfaces.
- ip link -s show ens3: ver la ens3 con estadísticas.
- ip addr show ens3: Ver la IP de ens3.
- ip route: Ver tabla de enrutamiento.
- tracepath access.redhat.com: Rastreo de las rutas.
- ss -ta. Igual que **netstat**.

#### Configuración

- nmcli dev status: Estado (conectado/no conectado) de los dispositivos.
- nmcli conn show [--active]: Lista todas las conexiones.
- nmcli conn [up] [down] [reload]: Activar / desactivar / recargar.
- nmcli dev disconnect ens3: Dessconectar la interfaz (mejor que down).
- nmcli con del ens3: Borrar una conexión.
- nmcli con add \
  con-name lab \
  type ethernet \
  ifname eth0 \
  ipv4.method manual \
  ipv4.addresses 192.168.1.10 \
  ipv4.gateway 192.168.1.1
- nmcli con mod ID +ipv4.dns IP: Añadir DNS. Si no se pone "+" lo sobrescribe.
- ip -br addr show enp0s3: Ver la IP y estado de enp0s3.

#### Resolución de nombres

- hostname: Consulta el nombre.
- hostnamectl status: Ver el nombre stático y transient.
- hostnamectl hostname host.example.com: Establece un nombre.
- getent hosts hostname: Busca resolver un nombre **primero mira /etc/hosts**.
- host marca.com: Resolver nombre **no consulta /etc/hosts**
- dig marca.com: Resolver nombre **no consulta /etc/hosts**

---

## 14. Acceso al almacenamiento conectado a la red

### Gestión de almacenamiento NFS

- **Comando clave**: `mount -t nfs`

---

## 15. Gestión de la seguridad de redes

### NFS

- showmount --exports server: Ver los FS que se sirven desde el host.
- mount -t nfs -o rw,sync server:/export /mountpoint: Montaje de un nfs.

### AutoFS

Mapa indirecto: /etc/auto.master.d/demo.autofs + /etc/auto.demo

```bash
# /etc/auto.master.d/demo.autofs
/externo /etc/auto.demo
```

```bash
# /etc/auto.demo
work  -rw,sync  serverb:/shares/work
holydays  -r,sync  serverb:/shares/holydays
```

Por tanto todo estará en _externo_:
/externo/work
/externo/holydays

Mapa directo: /etc/auto.master.d/demo.autofs + /etc/auto.direct

```bash
# /etc/auto.master.d/demo.autofs
/- /etc/auto.direct
```

```bash
# /etc/auto.direct
/mnt/work  -rw,sync  serverb:/shares/work
/home/holydays  -r,sync  serverb:/shares/holydays
```

Las rutas son absolutas.

### Firewalld y Selinux

- firewall-cmd --get-services: Obtener servicios
- semanage port -l: Enumerar asignaciones de etiquetas de puerto actuales.
- semanage port -a -t port_label -p tcp|udp PORTNUMBER: Agregar un puerto a Selinux. Ej: semanage port -a -t gopher_port_t -p tcp 71
- semanage port -l -C: Ver los cambios en la política predeterminada.
- semanage port -d -t gopher_port_t -p tcp 71: Eliminar la etiqueta de un puerto.
- semanage port -m -t http_port_t -p tcp 71: Modificar la etiqueta de un puerto.

---

## 16. Ejecución de contenedores

Instalar las herramientas:

```bash
dnf install container-tools
```

Registro automático con `/etc/containers/registries.conf` como plantilla, copiar el archivo a `~/.config/containers/registries.conf`.

### Uso de contenedores

Tipos:

- `ROOTLESS` Usuario sin privilegios.
- `ROOTFUL` Usuario con privilegios.

- **Comando clave**:
  - `podman`
  - `podman info` Información sobre podman
  - `podman search python` Buscar imágenes de "python"
  - `podman create --name nombre_contenedor tag` Crear un contenedor
  - `podman start nombre_contenedor` Arrancar un contenedor
  - `podman stop nombre_contenedor` Parar un contenedor
  - `podman exec nombre_contenedor ps -ax` Lanzar un comando a un contenedor (sin entrar)
  - `podman rmi nombre_imagen` Borrar una imagen
  - `podman rm nombre_contenedor` Borrar un contenedor
  - `podman port nombre_contenedor` `podman port -a` Ver los puertos de un/todos contenedor/es
  - `sudo loginctl enable-linger 1000` Esto hace que desaparezcan los warning iniciales con un usuario. Sirve para que se puedan quedar procesos en segundo plano sin necesidad de tener activa la sesión del usuario.
  -

```bash
# Login con la contraseña en variable de entorno (passsword-stdin)
echo $PASSWORDVAR | podman login --username oliva_rh --password-stdin registry.access.redhat.com
# Ver cuenta logueada
podman login registry.access.redhat.com --get-login
```

El archivo de configuración está en /etc/containers/registries.conf, pero es `sobrescrito` por $HOME/.config/containers.
Se usa para ejecutar podman en modo `ROOTLESS`.

Se debe instalar las utilidades de contenedores `dnf install container-tools`.

El comando `podman ps -a` enumera los contenedores en todos sus estados:

- Creado
- En Ejecución
- Detenido
- En pausa
- Eliminado

Se puede crear un contenedor directamente desde el repositorio y hacer que esté en ejecución `podman run -d --name nombre_contenedor repositorio comando`.
Por ejemplo podemos crear un contenedor de python38 que no salga `podman run -d --name python38 registry.access.redhat.com/ubi8/python-38 sleep infinity`.

#### Aislamiento de contenedores

Cuando ejecutamos un contenedor con un usuario del sistema, es posible que no tenga los permisos necesarios para acceder a directorios en el host. Esto sucede porque **Podman utiliza espacios de nombres de usuario (user namespaces)**, que aíslan los IDs de usuario dentro del contenedor del host.

Para que el contenedor pueda acceder a un directorio en el host, debemos ajustar los permisos del sistema de archivos. Además, si **SELinux** está habilitado, es necesario ajustar los contextos de seguridad.

Por ejemplo, si necesitamos montar `/var/lib/mysql_data` de forma persistente para un contenedor MySQL, debemos asegurarnos de que los permisos del directorio sean compatibles con el usuario que ejecuta MySQL dentro del contenedor.

Primero, podemos verificar el ID de usuario utilizado por MySQL en el contenedor:

```bash
podman exec -it db01 grep mysql /etc/passwd
mysql:x:27:27:MySQL Server:/var/lib/mysql:/sbin/nologin
```

---

##### Ajustar permisos con `podman unshare`

El comando `podman unshare` permite ejecutar comandos dentro del espacio de nombres del usuario de Podman, mapeando los IDs de usuario y grupo del contenedor al host. Esto nos permite cambiar los permisos de un directorio en el host para que sean accesibles desde el contenedor.

1. Crear el directorio para almacenar los datos de MySQL:

    ```bash
    mkdir /home/oliva/db_data
    ```

2. Ajustar los permisos utilizando `podman unshare`:

    ```bash
    podman unshare chown 27:27 /home/oliva/db_data
    ```

    Ahora el directorio será propiedad del usuario `mysql` dentro del contenedor. Podemos verificarlo:

    ```bash
    ls -l /home/oliva/
    drwxrwxr-x. 3 27 27 18 May  5 14:37 db_data
    ```

---

##### Montar el volumen en el contenedor

Podemos iniciar el contenedor y montar el directorio como un volumen persistente. Si **SELinux** está habilitado, es importante agregar el sufijo `:Z` al volumen para ajustar automáticamente los contextos de **SELinux**:

```bash
podman run -d --name db01 \
  -e MYSQL_USER=student \
  -e MYSQL_PASSWORD=student \
  -e MYSQL_DATABASE=dev_data \
  -e MYSQL_ROOT_PASSWORD=redhat \
  -v /home/oliva/db_data:/var/lib/mysql:Z \
  registry.redhat.io/rhel9/mariadb-105
```

---

> [!TIP]
> **¿Qué hace el sufijo `:Z`?**
>
> El sufijo `:Z` ajusta los contextos de **SELinux** del directorio en el host (`/home/oliva/db_data`) para que el contenedor pueda acceder a él. Esto asegura que **SELinux** no bloquee la operación y mantiene la seguridad del sistema.

Podemos verificar los contextos de **SELinux** después de montar el volumen:

```bash
ls -Z /home/oliva/db_data
unconfined_u:object_r:container_file_t:s0 /home/oliva/db_data
```

### Crear una red

A partir de RHEL9 el backend de red por defecto es `netavark`.
Puedes ejecutar **podman info** para consultar el backend de red. En caso de no ser `netvar` puedes indicarlo en el fichero de configuración _/usr/share/containers/containers.conf_

```bash
podman network create --gateway 10.87.0.1 --subnet 10.87.0.0/16 db_net
#####################
podman inspect db_net
[
     {
          "name": "db_net",
...output omitted...
          "subnets": [
               {
                    "subnet": "10.87.0.0/16",
                    "gateway": "10.87.0.1"
               }
          ],
...output omitted...
          "dns_enabled": true,
...output omitted...
#####################
podman run --replace -d --name db01 \
  -e MYSQL_USER=student \
  -e MYSQL_PASSWORD=student \
  -e MYSQL_DATABASE=dev_data \
  -e MYSQL_ROOT_PASSWORD=redhat \
  -v /home/oliva/db_data:/var/lib/mysql:Z \
  registry.redhat.io/rhel9/mariadb-105
```

> [!NOTE]
> Si no especifica las opciones **--gateway --subnet**, se crean con los valores predeterminados..

para conectar una red a un contenedor `podman network connect red01 contenedor01`.

### Gestión de contenedores como servicios del sistema

> [!WARNING]
> Se debe hacer ssh usuario@host para iniciar una sesión completa.
> NO SE PUEDE hacer _sudo o su_ para cambiar de usuario.

Se debe definir el directorio manualmente ~/.config/systemd/user/

> [!IMPORTANT]
> El directorio _user_ es tal cual!!, no es el nombre de usuario, no funciona si es otro nombre!!

```bash
 mkdir -p ~/.config/systemd/user
```

Use el comando `podman generate systemd --name nombre_contenedor`. El resultado te dará la salida por pantalla de lo que debería ser el archivo.
> [!NOTE]
> Si se añade la opción `--new`, va a generar una salida que elimina el contenedor.
> La opción `--files` genera el archivo.
> Comando completo `podman generate systemd --name contenedor --new --files`.

A continuación recarga el daemon y activa el servicio con `--user`.

```bash
systemctl --user daemon-reload
systemctl --user start contenedor.service
systemctl --user status contenedor.service
```

#### Ejecución independiente del login

Cuando se ejecuta un contenedor con systemd, si el usuario sale, se apaga.
Para evitar esto, usamos linger desde el mismo usuario.

```bash
# Ver si está "Lingering"
loginctl show-user oliva
# Activar Lingering
loginctl enable-linger
# Desactivar Lingerin
loginctl disable-linger 
```

---

## Repaso

- BLoquea y desbloquea un usuario.
