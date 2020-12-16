# **Intrucciones:**

## **Intalacion de libreria [rana/ora]([https://gopkg.in/rana/ora.v4])**

### **LINUX**

**Creamos una carpeta nueva y le asignamos permisos:**

```bash
sudo mkdir /usr/local/share/pkgconfig
sudo chmod 777 /usr/local/share/pkgconfig
```

**Accedemos a la carpeta que hemos creados:**

```bash
cd /usr/local/share/pkgconfig
```

**Creamos un archivo con el nombre oci8.pc con el siguiente contenido:**

```c
prefix=/usr
version=19.3
build=client64

libdir=${prefix}/lib/oracle/${version}/${build}/lib
includedir=${prefix}/include/oracle/${version}/${build}

Name: oci8
Description: Oracle database engine
Version: ${version}
Libs: -L${libdir} -lclntsh
Libs.private:
Cflags: -I${includedir}
```

### **Validar que se tiene instalado completamente el Oracle Instant Client en su version 12.1 / 19.3:**

```bash
oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64
oracle-instantclient19.3-devel-19.3.0.0.0-1.x86_64
oracle-instantclient19.3-precomp-19.3.0.0.0-1.x86_64
oracle-instantclient19.3-sqlplus-19.3.0.0.0-1.x86_64
oracle-instantclient19.3-tools-19.3.0.0.0-1.x86_64
```

### **Validar que se posee las variables de entornos configuradas:**

```bash
sudo nano ~/.profile

export PKG_CONFIG_PATH=/usr/local/share/pkgconfig
export ORACLE_HOME=/usr/lib/oracle/19.3/client64
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib:$ORACLE_HOME

export OCI_HOME=/usr/lib/oracle/19.3/client64/lib
export OCI_LIB_DIR=$ORACLE_HOME/lib
export OCI_INC_DIR=/usr/include/oracle/19.3/client64
export OCI_INCLUDE_DIR=/usr/include/oracle/19.3/client64
export OCI_VERSION=12

export PATH=$PATH:$ORACLE_HOME/bin
export GOPATH=/home/gvalladares/Repo/goProyectos

export C_INCLUDE_PATH=/usr/include:/usr/include/oracle/19.3/client64:/usr/local/include
```

### **Si se modifico el profile, se debera de recargar las variables de entorno:**

```bash
source ~/.profile
```

### **En el proyecto que requerimo el paquete procederemos a descargarla e instalarla:**

```bash
go get -u -v gopkg.in/rana/ora.v4
```
