# Instalacion de NodeJS 20

## 1. Prefacio

Esta pagina te explicara como instalar **NodeJS** para ambas plataformas; Linux y Ubuntu.

Es requisito tener una instalacion valida de **NodeJS** para poder desarrollar en **React** durante la catedra.

## 1.1. Validacion

Es posible que ya poseas una instalacion de **NodeJS** en tu sistema. Verificaremos esto primero para ver como proceder.

Para comprobar si tienes una instalacion de **NodeJS** en tu sistema, abre una terminal (o Powershell/CMD en Windows) y escribe el comando `node --version`.

```bash
$ node --version
v20.16.0
```

Si tu version es `v20.x.x` puedes ignorar esta pagina. En caso de ser diferente, debes desinstalarla para utilizar la correcta.

### 1.1.1. Desinstalacion
#### 1.1.1.1. Ubuntu, CentOS, Debian
1. Abre una terminal.
2. Escribe los siguientes comandos.
```bash
$ sudo apt-get remove nodejs
$ sudo apt-get remove npm
```

3. Comprueba que no poseas mas versiones de Node ejecutando el comando `node --version`. Si obtienes un error o el comando no existe, ya lo has desinstalado.

#### 1.1.1.2. Windows
1. Abre la aplicacion de **Configuracion** o **Settings**.
2. Dirigete a **Aplicaciones > Aplicaciones instaladas** o **Apps > Installed apps**.
3. Busca en la caja de busqueda `node` o `nodejs`.
4. Da click derecho sobre los resultados y presiona en **Desinstalar** o **Uninstall**.
5. Sigue los pasos del desinstalador.

## 2. Instalacion

Para instalar **NodeJS** utilizaremos **Node Version Manager (NVM)**. Esta herramienta te permitira administrar la version de NodeJS que tu sistema utiliza en un momento dado, permitiendote no desinstalar luego versiones previas y poder utilizar la que tu proyecto requiera en el momento.

Para el caso de la catedra, utilizaremos **NodeJS 20** ya que es la version **Long Term Support (LTS)** del framework.

Dividiremos la instalacion en **2 segmentos**; NVM y luego como administrar las versiones.

### 2.1. Instalacion de Node Version Manager (NVM)

#### 2.1.1. Ubuntu, CentOS, Debian
1. Abre una terminal.
2. Actualiza tus repositorios ejecutando `sudo apt update`.
3. Ejecuta el siguiente comando para descargar e instalar NVM.
```bash
# Con WGET
$ wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
# Con cURL
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
```

**Nota**: Al momento de redactar esto, la ultima version de NVM es la **v0.40.0**. Verifica porfavor [en el repositorio oficial de NVM](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script) cual es la ultima version para ejecutar el comando correcto.

4. Ejecuta el comando `nvm list available` para comprobar la instalacion correcta de NVM. En caso de que diga que es desconocido, cierra y vuelve a abrir la terminal.
```bash
$ nvm list available

|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|    22.5.1    |   20.16.0    |   0.12.18    |   0.11.16    |
|    22.5.0    |   20.15.1    |   0.12.17    |   0.11.15    |
|    22.4.1    |   20.15.0    |   0.12.16    |   0.11.14    |
|    22.4.0    |   20.14.0    |   0.12.15    |   0.11.13    |
|    22.3.0    |   20.13.1    |   0.12.14    |   0.11.12    |
|    22.2.0    |   20.13.0    |   0.12.13    |   0.11.11    |
|    22.1.0    |   20.12.2    |   0.12.12    |   0.11.10    |
|    22.0.0    |   20.12.1    |   0.12.11    |    0.11.9    |
|    21.7.3    |   20.12.0    |   0.12.10    |    0.11.8    |
|    21.7.2    |   20.11.1    |    0.12.9    |    0.11.7    |
|    21.7.1    |   20.11.0    |    0.12.8    |    0.11.6    |
|    21.7.0    |   20.10.0    |    0.12.7    |    0.11.5    |
|    21.6.2    |    20.9.0    |    0.12.6    |    0.11.4    |
|    21.6.1    |   18.20.4    |    0.12.5    |    0.11.3    |
|    21.6.0    |   18.20.3    |    0.12.4    |    0.11.2    |
|    21.5.0    |   18.20.2    |    0.12.3    |    0.11.1    |
|    21.4.0    |   18.20.1    |    0.12.2    |    0.11.0    |
|    21.3.0    |   18.20.0    |    0.12.1    |    0.9.12    |
|    21.2.0    |   18.19.1    |    0.12.0    |    0.9.11    |
|    21.1.0    |   18.19.0    |   0.10.48    |    0.9.10    |

This is a partial list. For a complete list, visit https://nodejs.org/en/download/releases
```

Hasta este punto ya tienes el administrador de versiones instalado, **pero no NodeJS**.

#### 2.1.2. Windows

1. Dirigete al repositorio de la implementacion de NVM para Windows [haciendo click aqui](https://github.com/coreybutler/nvm-windows/releases/latest).
2. Descarga el archivo `nvm-setup.exe` de la lista debajo.
3. Ejecuta el instalador y sigue los pasos.

Hasta este punto ya tienes el administrador de versiones instalado, **pero no NodeJS**.

### 2.2. Instalacion de NodeJS (Administracion de Versiones)

A partir de ahora, sin importar si estas en **Windows** o **Linux** los comandos son iguales. Procede a abrir una terminal o Powershell/CMD.

#### 2.2.1. Validar version actual
Para conocer cual es la version actual de NodeJS que estas utilizando, escribe el comando `nvm current`.
```powershell
PS C:\Users\puntero> nvm current
v20.16.0
```

Si la salida es `vxx.xx.xx` o similar, estas actualmente utilizando una version de Node. En la salida de ejemplo, esta es la `20.16.0`.

#### 2.2.2. Instalar una nueva version
Para instalar una version deseada de Node utilizamos el comando **`nvm install`**.

Primero, enlista las versiones actuales de NodeJS con el comando `nvm list available`.
```bash
$ nvm list available

|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|    22.5.1    |   20.16.0    |   0.12.18    |   0.11.16    |
|    22.5.0    |   20.15.1    |   0.12.17    |   0.11.15    |
|    22.4.1    |   20.15.0    |   0.12.16    |   0.11.14    |
|    22.4.0    |   20.14.0    |   0.12.15    |   0.11.13    |
|    22.3.0    |   20.13.1    |   0.12.14    |   0.11.12    |
|    22.2.0    |   20.13.0    |   0.12.13    |   0.11.11    |
|    22.1.0    |   20.12.2    |   0.12.12    |   0.11.10    |
|    22.0.0    |   20.12.1    |   0.12.11    |    0.11.9    |
|    21.7.3    |   20.12.0    |   0.12.10    |    0.11.8    |
|    21.7.2    |   20.11.1    |    0.12.9    |    0.11.7    |
|    21.7.1    |   20.11.0    |    0.12.8    |    0.11.6    |
|    21.7.0    |   20.10.0    |    0.12.7    |    0.11.5    |
|    21.6.2    |    20.9.0    |    0.12.6    |    0.11.4    |
|    21.6.1    |   18.20.4    |    0.12.5    |    0.11.3    |
|    21.6.0    |   18.20.3    |    0.12.4    |    0.11.2    |
|    21.5.0    |   18.20.2    |    0.12.3    |    0.11.1    |
|    21.4.0    |   18.20.1    |    0.12.2    |    0.11.0    |
|    21.3.0    |   18.20.0    |    0.12.1    |    0.9.12    |
|    21.2.0    |   18.19.1    |    0.12.0    |    0.9.11    |
|    21.1.0    |   18.19.0    |   0.10.48    |    0.9.10    |

This is a partial list. For a complete list, visit https://nodejs.org/en/download/releases
```

Luego, selecciona la version que quieres instalar. En la catedra, utilizaremos **la ultima version de Node 20**, por lo que en este momento elegimos la `20.16.0`.

Ahora, escribes el comando de instalacion con el numero de version deseado.
```bash
$ nvm install 20.16.0
Downloading node.js version 20.16.0 (64-bit)...
Extracting node and npm...
Complete
npm v20.16.0 installed successfully.


Installation complete. If you want to use this version, type

nvm use 20.16.0
```

#### 2.2.3. Cambiar de version de Node
Primero, enlista las versiones que tienes actualmente instaladas en tu sistema con el comando `nvm list`.
```bash
$ nvm list

  * 20.16.0 (Currently using 64-bit executable)
    18.20.4
```

Tu version actual **en uso** sera marcada con un asterisco. Busca la version que quieres utilizar por numero, y utiliza el comando `nvm use` para activarla.
```bash
$ nvm use 20.16.0
Now using node v20.16.0 (64-bit)
```

Comprueba que se este utilizando la version correcta de Node con el comando `node --version`
```bash
$ node --version
v20.16.0
```