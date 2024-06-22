# 1. Utilizacion de Docker

## 1.0 Que es Docker?
**Docker** es una herramienta de virtualizacion que permite a sus usuarios ejecutar aplicaciones y/o servicios en un entorno virtualizado al nivel del sistema operativo.

Esto, en criollo, significa que se le da a uno el poder de ejecutar aplicaciones sin necesidad de **alterar al sistema operativo principal** en ningun aspecto (virtualizado).

No es lo mismo que uno instale **Python** en su PC, modificando y alterando a su propio sistema operativo para poder utilizarlo, a lo que hace Docker que es **virtualizarlo** dentro de la PC del usuario. Esto **aisla** a Python de la computadora principal, haciendo que sea ejecutado en un entorno controlado del cual el sistema operativo principal no modifica nada para posibilitar mas que alojarle recursos.

## 1.1 Para que puedo usar Docker?
Sabiendo el poder de la virtualizacion que brinda Docker como herramienta, que se puede hacer con el?

### 1.1.0 Entorno de Desarrollo
Cuando uno desarrolla aplicaciones, necesita hacer lo que se llama "*emulacion de produccion*" o mas conocido como **entorno de desarrollo**. Esto significa que la aplicacion misma disponga de otras aplicaciones o servicios (bases de datos, servicios de terceros) en un entorno local para poder *probarla* y asegurarse que esta:
1. Se comunica correctamente con la base de datos (o las multiples bases de datos).
2. Puede interactuar con los otros servicios de los cuales depende.
3. Las funcionalidades programadas en el software que necesitan de servicios externos **funcionan correctamente**.

Este entorno de desarrollo preparado sirve para **prender** o **apagar** las dependencias de tu software cuando desees, sin preocuparte de romper alguna instalacion dentro de tu sistema operativo principal.

## 1.2 Comandos Basicos
### 1.2.1 `docker run`
Inicia un contenedor a partir de una imagen especificada.

```bash
# Ejecuta un contenedor con la imagen "hello-world".
$ docker run hello-world
```

```bash
# Ejecuta un contenedor con la imagen "hello-world" y le da el nombre "hw-container" al contenedor resultante.
$ docker run --name hw-container hello-world
```

```bash
# Ejecuta un contenedor con la imagen "hello-world", le da el nombre "hw-container" al contenedor resultante y se desliga de la terminal (para que corra en el fondo sin que dependa de nuestra terminal)
$ docker run -d --name hw-container hello-world
```

Para mas informacion sobre los parametros del comando `run`, escribe `docker run --help`.

### 1.2.2 `docker pull`
Descarga una imagen desde Docker Hub o un registro de Docker disponible al publico/accesible.

```bash
# Descarga la imagen de Ubuntu desde Docker Hub.
$ docker pull ubuntu
```

```bash
# Descarga la imagen de Ubuntu (del tag jammy, generalmente una version especifica de la imagen) desde Docker Hub.
$ docker pull ubuntu:jammy
```

Para mas informacion sobre los parametros del comando `pull`, escribe `docker pull --help`.

### 1.2.3 `docker ps`
Lista los contenedores en ejecución.

```bash
# Muestra los contenedores que están actualmente en ejecución.
$ docker ps
```

```bash
# Muestra TODOS los contenedores (en ejecución y detenidos).
$ docker ps -a
```

Para más información sobre los parámetros del comando `ps`, escribe `docker ps --help`.

### 1.2.4 `docker stop`
Detiene un contenedor en ejecución.

```bash
# Detiene el contenedor con el ID especificado o nombre de contenedor.
$ docker stop container_id
```

```bash
# Detiene múltiples contenedores al mismo tiempo especificados por sus IDs/nombres.
$ docker stop container_id1 container_id2
```

Para más información sobre los parámetros del comando `stop`, escribe `docker stop --help`.

### 1.2.5 `docker start`
Inicia un contenedor detenido.

```bash
# Inicia el contenedor con el ID especificado o el nombre de contenedor.
$ docker start container_id
```

```bash
# Inicia múltiples contenedores especificados por sus IDs/nombres.
$ docker start container_id1 container_id2
```

Para más información sobre los parámetros del comando `start`, escribe `docker start --help`.

### 1.2.6 `docker rm`
Elimina un contenedor. Esto no es lo mismo que **eliminar una imagen**.

```bash
# Elimina el contenedor con el ID especificado o nombre.
$ docker rm container_id
```

```bash
# Elimina múltiples contenedores especificados por sus IDs/nombres.
$ docker rm container_id1 container_id2
```

### 1.2.7 `docker images`
Lista las imágenes descargadas en el sistema. Esto lo puedes usar para ver si ya tienes una imagen descargada en tu PC.

```bash
# Muestra todas las imágenes disponibles en el sistema local.
$ docker images
```

Para más información sobre los parámetros del comando `images`, escribe `docker images --help`.

## 1.3 Siguientes Pasos
Proximamente cuando veamos el levantamiento de una base de datos se entendera como se utiliza Docker bien en un entorno real.