# RHCSA Rapid Track - Preparación Completa para el Examen RHCSA (RHEL 9)

Este documento es una guía rápida basada en el curso RH199 para preparar el examen RHCSA en RHEL 9.

## Tabla de Contenidos

1. Acceso a los sistemas y obtención de soporte (Importancia: 5)
2. Gestión de archivos desde la línea de comandos (Importancia: 5)
3. Gestión de usuarios y grupos locales (Importancia: 5)
4. Control de acceso a archivos (Importancia: 4)
5. Gestión de la seguridad con SELinux (Importancia: 5)
6. Ajuste del rendimiento del sistema (Importancia: 3)
7. Programación de tareas futuras (Importancia: 3)
8. Instalación y actualización de paquetes de software (Importancia: 4)
9. Gestión de almacenamiento básico (Importancia: 5)
10. Gestión de la pila de almacenamiento (Importancia: 4)
11. Servicios de control y procesos de arranque (Importancia: 5)
12. Análisis y almacenamiento de registros (Importancia: 4)
13. Gestión de redes (Importancia: 5)
14. Acceso al almacenamiento conectado a la red (Importancia: 3)
15. Gestión de la seguridad de redes (Importancia: 4)
16. Ejecución de contenedores (Importancia: 3)
17. Revisión exhaustiva (Importancia: 5)

---

## 1. Acceso a los sistemas y obtención de soporte (Importancia: 5)

### Edición de archivos de texto desde el prompt de shell (Vim)

- **Comandos básicos de Vim**:
  - `vi filename`: Abre un archivo con vi (o vim si está instalado el paquete `vim-enhanced`).
  - Modo de inserción: `i` para entrar, `Esc` para salir.
  - Guardar y salir: `:wq`.
  - Salir sin guardar: `:q!`.

### Configuración de autenticación basada en claves SSH

- **Comandos clave**:
  - `ssh-keygen -t rsa -b 2048`: Generar claves SSH.
  - `ssh-copy-id user@remotehost`: Copiar clave pública al servidor remoto.

### Creación de un informe de diagnóstico

- **Comando**: `sosreport`

---

## 2. Gestión de archivos desde la línea de comandos (Importancia: 5)

### Comandos básicos de gestión de archivos

- **Comandos clave**:
  - `cp`, `mv`, `rm`: Copiar, mover y eliminar archivos.
  - `ln -s`: Crear enlaces simbólicos.
  - `find /path -name "*.txt"`: Buscar archivos.

---

## 3. Gestión de usuarios y grupos locales (Importancia: 5)

### Creación y administración de usuarios

- **Comandos clave**:
  - `useradd username`: Crear un nuevo usuario.
  - `usermod -aG groupname username`: Agregar un usuario a un grupo.

### Obtención de acceso de superusuario

- **Comando clave**: `sudo su`

---

## 4. Control de acceso a archivos (Importancia: 4)

### Gestión de permisos de archivos

- **Comandos clave**:
  - `chmod`: Cambiar permisos de archivos.
  - `chown`: Cambiar propietario de archivos.
  - `umask`: Configurar permisos predeterminados.

---

## 5. Gestión de la seguridad de SELinux (Importancia: 5)

### Modificación de los modos de SELinux

- **Comandos clave**:
  - `getenforce`, `setenforce`: Ver y cambiar el modo de SELinux.

### Ajuste de booleanos de SELinux

- **Comando clave**: `semanage boolean`

---

## 6. Ajuste del rendimiento del sistema (Importancia: 3)

### Finalización y monitoreo de procesos

- **Comandos clave**:
  - `kill`, `top`, `htop`: Gestionar procesos.
  - `systemctl status`: Ver estado de servicios.

---

## 7. Programación de tareas futuras (Importancia: 3)

### Uso de cron

- **Comando clave**: `crontab -e`

---

## 8. Instalación y actualización de paquetes de software (Importancia: 4)

### Gestión de paquetes con DNF

- **Comando clave**: `dnf install package-name`

---

## 9. Gestión de almacenamiento básico (Importancia: 5)

### Montaje de sistemas de archivos

- **Comandos clave**:
  - `mount`, `umount`: Montar y desmontar sistemas de archivos.
  - `lsblk`: Ver dispositivos de almacenamiento.

---

## 10. Gestión de la pila de almacenamiento (Importancia: 4)

### Creación de volúmenes lógicos

- **Comando clave**: `lvcreate`

---

## 11. Servicios de control y proceso de arranque (Importancia: 5)

### Control de servicios

- **Comando clave**: `systemctl start/stop/restart service-name`

---

## 12. Análisis y almacenamiento de registros (Importancia: 4)

### Revisión de logs del sistema

- **Comando clave**: `journalctl`

---

## 13. Gestión de redes (Importancia: 5)

### Configuración de redes desde la línea de comandos

- **Comando clave**: `nmcli`

---

## 14. Acceso al almacenamiento conectado a la red (Importancia: 3)

### Gestión de almacenamiento NFS

- **Comando clave**: `mount -t nfs`

---

## 15. Gestión de la seguridad de redes (Importancia: 4)

### Configuración de firewalls

- **Comando clave**: `firewalld`

---

## 16. Ejecución de contenedores (Importancia: 3)

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
 mkdir -p ~/.config/systemd/oliva
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

## 17. Revisión exhaustiva (Importancia: 5)

### Resumen de conceptos clave y comandos

- Practicar todos los comandos esenciales mencionados en esta guía para la preparación final del examen.

## Edición de archivos de texto

Paquetes a instalar:

- básico: vim-minimal
- avanzado: vim-enhanced

## Cambiar la contraseña de root

En el inicio del sistema, editar la entrada del grub (normalmente con 'e').
Al final de la línea donde carga el kernel (normalmente tras el 'quiet') ponemos la instrucción `rd.break`.
Una vez se incie la consola de emergencia seguiremos estas instrucciones:

```bash
# Montar el sistema, hacer chroot
mount -o remount rw /sysroot
chroot /sysroot
# Entonces ya estamos como root
passwd
#Indroducimos la contraseña
# Luego indicamos que haga un relabel
touch /.autorelabel
```

> [!NOTE]
> Ojo! No es ./autorelabel sino `/.autorelabel`. Si esta instrucción no es correcta no podrás hacer loguin con la vieja contraseña ni con la nueva.

## Tema 16 - Gestión Podman