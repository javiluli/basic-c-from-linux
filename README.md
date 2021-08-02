# C / C++ desde consola Linux (básico)

## 1. Instalación del IDE Codelite / compilador gcc

En primer lugar, vamos a verificar si la distribución debian ya trae incluido el compilador

```console
gcc
```

---

La instalación de Codelite se va a realizar desde repositorios de internet:

- Iniciar una sesión de terminal en nuestro equipo Linux.
- Ganar acceso de administrado: sudo su.

```console
sudo su
```

- Actualizar repositorios: apt-get update.

```console
apt-get update
```

- Instalar el paquete: apt-get install codelite.

```console
apt-get install codelite
```

---

Si el gestor de instalación no es capaz de localizar el IDE, prueba a incluir los siguientes repositorios.

- Añadir las claves de acceso al repositorio:

```console
apt-key adv --fetch-keys http://repos.codelite.org/CodeLite.asc
```

Añadir en el fichero `/etc/apt/sources.list` el repositorio para codelite, incluyendo la entrada:

```bash
deb http://repos.codelite.org/debian/ jessie contrib
```

Actualizar repositorios: apt-get update
Instalar paquetes:

```console
apt-get install codelite
```

---

Los ejecutables del IDE y del compilador quedan instalados en la ruta `/usr/bin`.

Podrás encontrar un icono de **Codelite** en `/usr/share/icons/hicolor/64x64@2x/apps/codelite.png`

Si deseas crear un acceso directo en el escritorio como se hacía para Eclipse, crea el fichero codelite.desktop en /home/debian/Escritorio/ con el siguiente contenido:

```bash
[Desktop Entry]
Name=Codelite
Comment=Codelite
Exec="/usr/bin/codelite"
Icon=/usr/share/icons/hicolor/64x64@2x/apps/codelite.png
Terminal=false
Type=Application
Enconding=UTF-8
Categories=
```

## 2. Crear y compilar un programa desde consola

**Aplicación HolaMundo.**

- Crea el fichero main.c y guárdalo en cualquier ruta del sistema de archivos. Puedes utilizar el editor nano en Linux.

```c
#include <stdio.h>
int main(int argc, char **argv)
{
printf("Hola mundo\n");
return 0;
}
```

- Abrir una consola y nos movemos a la ruta donde se ha creado el fichero main.c.
- Ejecutando el comando `gcc` para compilar, obtendremos el fichero ejecutable salida.exe.

  - Obtener código objeto desde el código fuente:

  ```console
  gcc –c main.c -o holamundo.o.
  ```

- Obtener el fichero ejecutable utilizando como origen código objeto:

  ```console
  gcc holamundo.o –o salida.exe.
  ```

---

**Compilación por lotes. Fichero make.**

Si el programa está formado por múltiples ficheros con código fuente deberemos hacer uso del ejecutable gcc en multitud de ocasiones.

Es posible agrupar secuencias de órdenes de compilación en un fichero, que será posteriormente utilizado por el programa make para realizar la
compilación completa del proyecto. La aplicación make busca en el fichero makefile las pautas a seguir durante la compilación.

Para el ejercicio actual podemos crear el fichero **makefile** con la siguiente información:

```bash
salida.exe: holamundo.o:
  gcc holamundo.o -o salida.exe
holamundo.o: main.c:
  gcc -c main.c -o holamundo.o
```
