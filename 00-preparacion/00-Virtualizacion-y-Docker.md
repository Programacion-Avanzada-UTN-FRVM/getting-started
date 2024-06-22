# 0. Preparacion

## 0.0 Introduccion
Bienvenido a **Programacion Avanzada**.

La catedra espera de sus alumnos una predisposicion para aprender, desarrollar, cuestionar y impulsar su capacidad profesional en el rubro. Por ello, lo invitamos a practicar y realizar a conciencia cualquier actividad de la materia predispuesta para el alumnado.

## 0.1 Virtualizacion (Docker)
Para comenzar, ya sea que utilice un sistema operativo basado en UNIX (**Linux**) o **Windows**, le recomendamos **activar la virtualizacion en su computadora** para hacer uso de **Docker**.

Docker le permitira **levantar bases de datos temporales** sin instalar nada nativamente en su sistema operativo, siendo esto mucho mas resiliente, rapido y sencillo que una instalacion comun. Esto facilitara la interaccion con el equipo docente fuera a ocurrir un problema en su instalacion inicial / levantamiento.

### 0.1.0 Pasos Previos
Antes de proceder con la instalacion del entorno virtualizable, asegurate de haber activado la **virtualizacion** en su **BIOS**.

Para poder verificar esto, [sigue los pasos en este video](https://www.youtube.com/watch?v=MJ1HGrM5D3Y).

### 0.1.1 Windows
#### 0.1.1.0 Windows Subsystem for Linux (WSL)
Para instalar **Docker** en Windows debes tener el **sub-sistema de Linux para Windows (WSL)** instalado en tu computadora. Para verificar si ya posees una instalacion valida de WSL, ejecuta los pasos 1, 2 y 3 debajo y escribe el comando `wsl -l`.

Si el comando tira una distro de Linux (como Ubuntu, Debian o similar) significa que tienes una instalacion valida y puedes saltearte la instalacion de WSL.

En caso contrario, sigue los siguientes pasos:
1. Presiona las teclas **WIN + R** para abrir la ventana de ejecucion.
2. Escribe `powershell` y presiona la combinacion de teclas en el orden provisto **CTRL + SHIFT + ENTER**.
3. En la caja de otorgar permisos de administrador haz click en **si**.
4. Dentro de la terminal, escribe el comando `wsl --install`

Comenzara el proceso de instalacion (Ubuntu por defecto) que debe visualizarse de la siguiente forma:

<img alt="WSL Installation" src="https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/07/a2-install-wsl-and-ubuntu.png?q=50&amp;fit=crop&amp;w=750&amp;dpr=1.5">

Una vez finalizado, reinicia tu computadora y ya deberias poder gozar de utilizar **Ubuntu** en tu instalacion de Windows. Valida que se ha instalado correctamente ejecutando el comando `wsl -l` en una terminal de **Powershell**.

#### 0.1.1.1 Docker
Dirigete a [la documentacion oficial de **Docker**](https://docs.docker.com/desktop/install/windows-install/) y haz click sobre el boton **Download Docker Desktop for Windows**.

Sigue los pasos de instalacion y deberia finalizar correctamente, pidiendo que reinicies tu computadora.

Si te has perdido en algun paso, o no sabes que hacer y no esta detallado aqui, por favor visualiza el paso a paso [en este video](https://www.youtube.com/watch?v=ZO4KWQfUBBc).

### 0.1.2 Linux
Dentro de Linux puedes optativamente **solo instalar el Docker Engine** para utilizar Docker desde la terminal (usuarios intermedios a avanzados). Esto lo puedes hacer [buscando tu distro en esta lista y siguiendo los pasos](https://docs.docker.com/engine/install/).

El tutorial debajo seguira la instalacion de **Docker Desktop** (con entorno visual) para mas principiantes.

**NOTA**: Si ya has intentado instalar Docker en tu instalacion de Linux y no lo has logrado, ejecuta este comando antes de comenzar para eliminar dependencias mal instaladas o left-over. Si no lo has hecho y es tu primera vez, no hagas este paso
```bash
$ for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

#### 0.1.2.0 Ubuntu
La instalacion en Ubuntu es muy similar al resto de los distros, por favor no asustarse con los comandos a ejecutar (son copy & paste y se ejecutan una sola vez para instalar todo).

1. Agrega el repositorio `apt` de Docker a tu lista de fuentes.
```bash
# Sigue paso a paso estos comandos para agregar los certificados oficiales de Docker a tu OS (estos son utilizados por los pasos siguientes para agregar el repositorio correcto).
$ sudo apt-get update
$ sudo apt-get install ca-certificates curl
$ sudo install -m 0755 -d /etc/apt/keyrings
$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
$ sudo chmod a+r /etc/apt/keyrings/docker.asc

# Ahora, ejecuta estos dos comandos para agregar al repositorio de Docker oficial en tu lista de fuentes de apt.
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt-get update
```

2. Descarga el paquete `deb` de **Docker Desktop** mas reciente desde [la pagina oficial de Docker](https://docs.docker.com/desktop/install/ubuntu/) haciendo click en el boton **DEB Package**.
3. Localiza el paquete que acabas de descargar en tu sistema de archivos (generalmente `/home/usuario/Downloads`).
4. Parate sobre la carpeta donde se encuentra el archivo y anota su nombre completo con extension.
5. Instala el paquete.
```bash
# Actualizar y asegurarse que los repositorios estan cargados.
$ sudo apt-get update

# El ./ seguido del nombre del archivo .deb descargado recientemente.
$ sudo apt-get install ./docker-desktop-1234-x64.deb
```

Docker Desktop & Engine deberian estar disponibles desde el explorador de aplicaciones de tu entorno grafico de Ubuntu.

#### 0.1.2.1 Debian, Fedora, Arch
Para otros distros, seguir los pasos detallados en [la pagina oficial de Docker](https://docs.docker.com/desktop/install/linux-install/). Son identicos a los de Ubuntu con algunos cambios de repositorio.