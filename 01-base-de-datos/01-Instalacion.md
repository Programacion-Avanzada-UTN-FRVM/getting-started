# Instalación de Base de Datos Relacional

## 1. Selección
Dentro de la cátedra, estarás realizando con un grupo a determinar un **proyecto integrador** de 4 entregas como máximo. Este proyecto requerirá el uso de una **base de datos relacional** a elección del grupo.

Lo recomendado es que todos los integrantes preparen el entorno de desarrollo local en sus computadoras de forma tal que no existan inconvenientes para que un integrante clone y ejecute el proyecto en cualquier instancia de tiempo. En este documento se detallará cómo instalar las bases de datos relacionales más utilizadas y recomendadas por la cátedra.

Cabe destacar que si el grupo decide utilizar una base de datos no listada en este documento, recibirá mínima asistencia por parte del equipo docente en problemas que encuentre con ella.

## 2. Instalación
Los pasos de instalación estarán dados tanto para **Windows**, **Linux** y **Docker** (OS-agnostic).

Se aconseja el uso de **Docker** para evitar instalaciones fijas que pueden causar problemas en su uso.

### 2.1. PostgreSQL
#### 2.1.1. Descarga de Imagen
Para comenzar, primero debes descargar la imagen que contiene la última versión de **Postgres** a tu disco local. Esto te ahorrará el tiempo de descarga. Puedes saltarte este paso, pero es aconsejable hacerlo.

Levanta una **terminal** (`powershell` en Windows) y escribe el siguiente comando: `docker pull postgres`

Comenzará a descargarse la imagen de Postgres más reciente a tu disco local. Espera a que termine el proceso y ya tienes la imagen.

##### 2.1.1.1. Versiones Específicas
Si por alguna razón necesitas obtener una imagen específica de Postgres, por favor revisa [el directorio oficial de **tags** de la imagen](https://hub.docker.com/_/postgres/tags) para buscar la que necesitas.

Una vez encuentres el tag, descargas la imagen a tu disco con esa etiqueta utilizando el mismo comando de la forma siguiente:

```bash
# Descargar imagen de Postgres con etiqueta '11.4-alpine' (Versión 11.4 de Postgres)
$ docker pull postgres:11.4-alpine
```

### 2.2. MySQL
De la misma forma que Postgres, para **MySQL** puedes descargar la imagen utilizando el comando `docker pull mysql`.

Listado de Tags: https://hub.docker.com/_/mysql/tags

### 2.3. MariaDB
`docker pull mariadb`

Listado de Tags: https://hub.docker.com/_/mariadb/tags

## 3. Instalaciones Sin Docker
**Se desaconseja instalar las bases de datos directamente en el sistema operativo padre.**

En todo caso, puede lograr lo mismo que con Docker con una **instalación nativa**.

### 3.1. Windows
Para instalar PostgreSQL en Windows, simplemente [descarga el instalador desde aquí](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

Sigue los pasos del instalador. En la ventana de **Selección de Componentes** podrás elegir si quieres o no la interfaz visual de Postgres en la caja de **pgAdmin**. 

![alt text](components.png)

Si no quieres interfaz visual, destickea la caja y continúa. El resto déjalo todo marcado.

En la sección de **puerto** deja el por defecto; no necesitarás cambiarlo y si lo cambias deberás recordar cuál pusiste.