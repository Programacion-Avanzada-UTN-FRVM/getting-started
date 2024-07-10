# Ejecucion de Instancia de Base de Datos
**Si realizaste una instalacion nativa en el sistema operativo, ya automaticamente estara corriendo tu instancia de base de datos en el puerto configurado al momento de instalar. Puedes ignorar este paso.**

## 4. Ejecutar Instancia con Docker
Antes de comenzar con los pasos pensar en lo siguiente; cuando virtualizamos aplicaciones o servicios, generalmente **no son persistentes** a menos que asignemos volumenes fisicos/virtuales de donde puedan obtener su informacion.

Para nuestro caso de uso, es una necesidad que nuestro contenedor de Docker **tenga persistencia de informacion**. Por esta razon, primero nos aseguraremos de configurar el entorno de nuestra PC local para **garantizar persistencia**.

### 4.1. Volumenes en Docker
Un volumen en Docker es como "*compartir*" un pedazo de tu disco con un contenedor. Recordar que los contenedores tienen **su propio sistema de archivos**, por lo que no pueden acceder a nuestro disco de forma directa. Este sistema de archivos de los contenedores, ademas, es una copia directa del de la **imagen**, por lo que tendriamos que mantener al contenedor vivo (no necesariamente encendido) para persistir sus datos.

La solucion es **crear un volumen** que podamos montar cuando querramos de forma tal que no dependa todo del contenedor creado.

Para hacer eso comenzamos levantando una terminal (o `powershell` en Windows) y escribimos los siguientes comandos:

```bash
# Crea un nuevo volumen de Docker llamado 'volumen_base_datos'
$ docker volume create volumen_base_datos
volumen_base_datos
```

Para saber si tu volumen se creo correctamente, lista todos los volumenes y verifica que aparezca el tuyo.

```bash
$ docker volume ls
DRIVER    VOLUME NAME
local     volumen_base_datos
```

### 4.2. Crear Contenedor
Ahora con nuestro volumen creado, creamos un contenedor de la base de datos que seleccionamos para que utilice el volumen como punto de montura principal (`root`) para que cualquier cosa que hagamos dentro de el se guarde en nuestro volumen.

Nuestras necesidades son:
1. Exponer un servicio de base de datos relacional a nuestra red privada (para que la pueda acceder nuestra futura aplicacion de **Java Springboot**)
2. Controlar que funcione nuestra instancia de base de datos.
3. Poder accederla a traves de la terminal cuando deseemos.
4. Apagarla cuando no este en uso y que conserve la informacion, incluso si borramos el contenedor por alguna razon.

Todo esto se logra con el comando `docker run` y lleva ciertos pasos de configuracion. Cada configuracion nace con una pregunta, estas siendo:
1. **Cual es la imagen que voy a levantar?** Postgres, MariaDB, MySQL...
2. **Que nombre le doy al contenedor?**
3. **Que variables de entorno necesita para configurarlo?** Cosas como la contrasena del super-usuario, puerto, etcetera.
4. **Como lo expongo a la red?** Para que pueda accederlo a traves de mi red privada y no solo con una terminal.
5. **Como le indico el volumen que acabo de crear para que use eso?** Va a depender de la base de datos seleccionada, pero el parametro es el mismo.

Vamos paso a paso con el comando de creacion de Docker para entender lo que queremos hacer.
```bash
# Comando que crea un contenedor (detached) de Postgres llamado 'contenedor_postgres', expuesto a la red en el puerto 5432, montado al volumen 'volumen_base_datos' y configurado con variables de entorno especificas a Postgres para darle la contrasena por defecto del superusuario 'postgres' a 'test1234'.
$ docker run -d --name contenedor_postgres -e POSTGRES_PASSWORD=test1234 -v volumen_base_datos:/var/lib/postgresql/data -p 5432:5432 postgres:latest

# Lo mismo, pero para MariaDB (puerto 3306)
$ docker run -d --name contenedor_mariadb -e MARIADB_ROOT_PASSWORD=test1234 -v volumen_base_datos:/var/lib/mysql -p 3306:3306 mariadb:latest
```

Puede que parezca chino, pero vamos por partes para entendernos. Acordarse que las aplicaciones que se exponen a la red tienen un **puerto por defecto** en el que corren; generalmente este puerto **se puede cambiar** utilizando **variables de entorno** que la aplicacion misma define para configurar/cambiar como funciona.

A continuacion se visualizara un pequeno tutorial de networking en Docker. Si ya posees conocimientos de esto, pasa directo al punto **4.2.2**.

#### 4.2.1. Networking Basico en Docker
**Docker** tiene su propia red privada, totalmente separada de la tuya (la de tu PC real). Bajo esta concepcion, vamos a llamar a estas dos redes **red Docker** y **red PC** para diferenciarlas.

Pequeno repaso de redes:
- **Red Docker**: `10.0.0.0/16`
- **Red PC (Loopback)**: `127.0.0.1/8`

Cuando uno corre un contenedor en Docker, ese contenedor (a menos que se especifique) existe unicamente en la **red de Docker**. Para accederlo a traves de la red, uno tiene que especificar **la direccion IP que se le asigno al contenedor** y que esta fuera de la red de tu PC.

Es importante **siempre saber en que puerto corre la aplicacion de un contenedor**. Por ejemplo:
- Un contenedor de Postgres donde no se cambie la variable de entorno `PGPORT` estara escuchando en el puerto `5432`.
- De la misma manera, uno de MariaDB donde no se cambia la variable de entorno `MYSQL_TCP_PORT` y/o `MYSQL_UNIX_PORT` estara escuchando en el puerto `3306`.

Estos puertos corren sobre la **red de Docker**; para poder alcanzarlos en **nuestra red** debemos hacer algo conocido como **mapping**.

#### 4.2.2. Desglose del Comando de Ejecucion
Tomemos el comando de **Postgres** como ejemplo:

`docker run -d --name contenedor_postgres -e POSTGRES_PASSWORD=test1234 -v volumen_base_datos:/var/lib/postgresql/data -p 5432:5432 postgres:latest`
1. **`docker`**: Incluido en todos los comandos de Docker, invoca el **CLI** del motor de Docker.
2. **`run`**: Sub-comando de Docker para crear un contenedor.
3. **`-d`**: Parametro **detach**; causa que cuando se ejecute la creacion del contenedor, no este ligado de forma directa a la terminal actual.
   1. Si no se escribe este parametro, el contenedor ocupa nuestra terminal totalmente y si fueramos a cerrarla, se apaga el contenedor y muere.
4. **`--name contenedor_postgres`**: Parametro que asigna un nombre al contenedor (para que no sea generado automaticamente).
5. **`-e POSTGRES_PASSWORD=test1234`**: Parametro **variable de entorno**.
   1. Podemos escribir la cantidad de `-e` que querramos para cada variable de entorno que queremos establecer.
   2. En este comando, solo establecemos la variable `POSTGRES_PASSWORD` que controla la contrasena del superusuario de Postgres.
6. **`-v volumen_base_datos:/var/lib/postgresql/data`**: Parametro de **volumen**.
   1. El formato es `-v <origen_local>:<destino_contenedor>`, donde `origen_local` es una ruta del disco de tu PC real (o el nombre de un volumen de Docker) y `destino_contenedor` la ruta del sistema de archivos del contenedor a donde se montara el volumen.
   2. Para Postgres, siempre guarda toda la informacion de la base de datos en la ruta `/var/lib/postgresql/data`, mientras que MySQL y MariaDB lo hacen en `/var/lib/mysql`.
   3. Se pueden montar multiples volumenes para un mismo contenedor si se quisiera.
7. **`-p 5432:5432`**: Parametro de **mapping de puerto**.
   1. El formato es `-p <puerto_red_pc>:<puerto_red_docker>` donde `puerto_red_pc` es el puerto de **tu red** donde estara el `puerto_red_docker` que es de la red del contenedor.
   2. Uno puede, por ejemplo, "*cambiar el puerto*" mappeandolo a un puerto diferente de la red de tu PC; `-p 444:5432` haria que el contenedor exponga su puerto `5432` en el puerto `444` de la red de tu PC.
   3. Alternativamente si no entiendes muy bien esto, reemplaza este parametro por `-P` solamente; esto expone todos los puertos en escucha del contenedor directo a tu red sin mappear.
8. **`postgres:latest`**: El nombre de la imagen acompanado, opcionalmente, de un tag/etiqueta deseado.

Para un listado completo y mas detallado de **todos los parametros** que acepta `docker run`, [consulta la documentacion oficial de Docker](https://docs.docker.com/reference/cli/docker/container/run/).

#### 4.2.3. Consultar por Contenedores Creados
`docker container ls -a` es el comando que te mostrara todos los contenedores que creaste (hasta los apagados) en una lista, con sus IDs unicos y el estado de cada uno.

Puedes usar esto para validar que efectivamente se han creado tus contenedores.

### 4.3. Acceder Contenedor de Base de Datos
En el caso que uno quisiera acceder al servicio de base de datos a traves del **shell** (con terminal), lo puede hacer haciendo uso del comando `docker exec`.

#### 4.3.1. Shell en Postgres
`docker exec -it contenedor_postgres psql -U postgres`

Con esto uno accede al servicio de Postgres directo adentro del contenedor con un shell interactivo (introduzca la contrasena configurada en las variables de entorno previamente).

#### 4.3.2. Shell en MariaDB
`docker exec -it contenedor_mariadb mariabd -u root -p`

### 4.4. Ver logs
En algunos casos, si un error ocurriera en el proceso, puede uno visualizar los logs que genera un contenedor con el comando `docker logs`.

`docker logs contenedor_postgres`

## 5. Debugging con Docker Desktop
Si tienes Docker Desktop, puedes visualizar todas estas cosas directo en la interfaz.