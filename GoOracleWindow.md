# Instalacion de Golang con conexion a oracle en windows

## Esta instalacion funciona para ocupar las siguientes librerias estandar de go con oracle

* [Oci8](https://github.com/mattn/go-oci8)

* [Rana ora.v4](https://gopkg.in/rana/ora.v4)

* [GoOracle.v2](https://gopkg.in/goracle.v2)

### Pasos para la instalacion

* **Instalar Go**

Fuente:
[Golang](https://golang.org/dl/)

![text](img/go1.png)

![text](img/go2.png)

Validar version de go:

```bash
go version
```

![bash](img/go3.png)

* **Instalar Cliente de Oracle**

**Fuente:**
**Importante** la version del cliente debe ser 12.1 en adelante ya que estas librerias trabajan con **OCI8.pc** de las librerias nativas de proC en oracle

![alt](img/go4.png)

**Descargar el client basic y el sdk client**
[OracleClient](https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html)

Exportarlo en una carpeta cliente(Puede ser ne disco C o en una parte donde no se te olvide):

![alt](img/go6.png)
Se extrae completo
![alt](img/go7.png)

* **Instalar pkg-config(Windows como no tiene librerias nativas se instala para ser compatible)**
  
URLS de descarga

[pkgconfig](http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/pkg-config_0.26-1_win32.zip)
[glib](http://ftp.gnome.org/pub/gnome/binaries/win32/glib/2.28/glib_2.28.8-1_win32.zip)
[getext](http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/gettext-runtime_0.18.1.1-2_win32.zip)

![Link1](img/go8.png)

Se Extrae en una carpeta recomendado en el disco origen se llamara **pkg-config**:

![alt](img/go9.png)

* **Instalacion de MinGW-w64**

Para poder compilar nuestro proyecto o ejecutar nesecitamos las librerias nativas de gcc
[repo](https://sourceforge.net/projects/mingw-w64/files/)
[i686-win32-sjlj](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/8.1.0/threads-win32/sjlj/i686-8.1.0-release-win32-sjlj-rt_v6-rev0.7z)

![alt](img/go10.png)

Extraerlo y colocarlo en el disco origen.

![alt](img/go11.png)

* **Instalar git**

[git](https://git-scm.com/downloads)

Probar si el git instalalo correctamente:

```bash
git version
```

![alt](img/go12.png)
![alt](img/go13.png)
![alt](img/go14.png)

* **Configuracion del archivo OCI8.pc**

Crear un archivo llamado **oci8.pc** este colocarlo en las libreria pkg y colocar las siguientes configuraciones:

```C
ora=C:\oracleclient\instantclient_12_1
gcc=C:\mingw64
oralib=${ora}/sdk/lib/msvc
orainclude=${ora}/sdk/include
gcclib=${gcc}/lib
gccinclude=${gcc}/include
glib_genmarshal=glib-genmarshal
gobject_query=gobject-query
glib_mkenums=glib-mkenums
Name: OCI
Description: Oracle database engine
Version: 12.1
Libs: -L${oralib} -L${gcclib} -loci
Libs.private: 
Cflags: -I${orainclude} -I${gccinclude}
```

![alt](img/go15.png)
![alt](img/go16.png)

* **Configuracion de variables de entorno**
  
Se procesedera a configurar las 3 librerias instaladas ademas del archivo oci.pc

![alt](img/go17.png)
![alt](img/go18.png)
![alt](img/go19.png)
![alt](img/go20.png)
![alt](img/go21.png)
![alt](img/go22.png)
![alt](img/go23.png)
![alt](img/go24.png)

Validar el **OCI**

```bash
pkg-config --cflags --libs oci8
```

Validar si todo funciona

```bash
go get github.com/mattn/go-oci8
```

![alt](img/go25.png)

Si no sale ningun error ya tenemos nuestro ambiente de ejecucion o compilacion para oracle y golang si solo necesitan el ambiente para ejecutar omitir los pasos de instalacion de golang.

**Maquina de prueba:**
![alt](img/go26.png)
