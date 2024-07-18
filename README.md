<h1 align="center">
    Bienvenido a Programación Avanzada
</h1>
<p align="center">Este repositorio te ayudará a preparar todo lo necesario para cursar la materia con el menor atraso posible.</p>

## Requisitos
**Si consideras tener la experiencia suficiente para proceder sin necesidad de seguir un tutorial**, debajo te queda un listado de todas las cosas que necesitas para cursar la materia.

Recuerda, solo procede a entrar a estos links si sabes lo que haces. Es recomendable que sigas los pasos descritos en el indice para instalar los requerimientos.

- [**Docker Desktop**](https://www.docker.com/products/docker-desktop/): Plataforma de virtualizacion para levantar instancias de bases de datos principalmente.
  - [Imagen de MariaDB/MySQL](https://hub.docker.com/_/mysql): **Recomendado por la catedra utilizar MySQL**.
  - [Imagen de PostrgeSQL](https://hub.docker.com/_/postgres)
- [**JDK 21 LTS**](https://www.oracle.com/ar/java/technologies/downloads/#java21): Requerido para ejecutar aplicaciones de Spring en el sistema operativo.
- [**IntelliJ IDE**](https://www.jetbrains.com/idea/): IDE para desarrollar aplicaciones de Java con el framework de Spring, **recomendado por la catedra**.
- [**Spring Initializr**](https://start.spring.io/): Web para la inicializacion de un nuevo proyecto de Springboot.
- [**Node 20 LTS**](https://nodejs.org/en/download/prebuilt-installer): Utilizado para aplicaciones de front-end **React**; segunda parte del proyecto.

## Índice
Navega a traves de la documentacion disponible de la catedra haciendo click sobre el lugar deseado.

1. [**Preparacion**](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/blob/main/00-preparacion)
   1. [Instalacion de Docker](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/blob/main/00-preparacion/00-Virtualizacion-y-Docker.md)
   2. [Comandos basicos de Docker](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/blob/main/00-preparacion/01-Uso-Basico-Docker.md)
2. [**Base de Datos Relacional**](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/blob/main/01-base-de-datos)
   1. [Instalacion de base de datos](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/blob/main/01-base-de-datos/01-Instalacion.md)
   2. [Ejecucion de Instancia & Puertos](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/blob/main/01-base-de-datos/02-Ejecucion.md)
   3. Entorno visual (Opcional)
3. **Java SpringBoot**
   1. Instalacion y preparacion de entorno de desarrollo
   2. Conector de base de datos
   3. Dependencias (Testing, Spring Data + JPA)
   4. Aplicacion de Ejemplo (Comprueba tu instalacion)

## Cómo leer
### Bloques de Código
Si se deben ejecutar comandos o mostrar ejemplos de código, se utilizarán **bloques de código** en cada documento. Para el caso de la ejecución de comandos, cada comando singular se representa con un `$` (signo de peso). Esto indica que lo que sigue después de ese signo es **el comando en cuestión**.

## Cómo navegar
- Busca la carpeta deseada y haz clic sobre ella.
- Dentro de la carpeta, navega a través de los archivos `.md` (Markdown) para acceder a la documentacion.

## Tengo un problema
Si te encuentras con problemas, dudas o algún inconveniente en algún paso, por favor no dudes en crear una [**Issue**](https://github.com/Programacion-Avanzada-UTN-FRVM/getting-started/issues) en el repositorio para que podamos asistirte de forma asíncrona de la mejor manera. Tambien puedes crear una nueva Issue si encuentras un punto de mejora dentro de la documentacion y decides sugerir cambios.

Si es tu primera vez creando issues en un repositorio, se recomienda visualizar [**este contenido**](https://docs.github.com/es/issues/tracking-your-work-with-issues/creating-an-issue#creating-an-issue-from-a-repository) que te ayudará a entender cómo funciona. Las Issues son un concepto que la materia abarca, por lo que es importante que lo revises en caso que necesites ayuda con algo.