# LINUX: FUNDAMENTOS Y COMANDOS BÁSICOS

## 1\. Introducción a Linux y Conceptos Básicos

- **Definición:** Cuando hablamos de Linux, nos referimos al núcleo (Kernel) del sistema operativo. Una distribución de Linux incluye este núcleo junto con paquetes de aplicaciones .
- **Distribuciones:** Existen diversas distribuciones clasificadas en genéricas (Ubuntu, Debian, CentOS), para empresas (Red Hat), seguridad (Kali, Tails) y otros usos .
- **Licencias:** El Kernel de Linux es software libre y de código abierto (GPL), garantizando a los usuarios la libertad de usar, modificar y distribuir el programa (Estas licencias deben ser aprobadas por la Open Source Initiative (OSI) y tener denominación GPL).
- Una **distribución** de Linux es el sistema operativo completo, que incluye el núcleo del sistema (Kernel), diversas aplicaciones y, habitualmente, uno de estos entornos de escritorio:  
  <br>

## **2\.** Entornos **de Escritorio**

Un entorno de escritorio es la interfaz gráfica (las ventanas, los menús, los iconos) con la que interactúas visualmente en el sistema.

- **Diversidad de interfaces:** Linux ofrece múltiples entornos gráficos adaptados a diferentes necesidades y recursos del sistema:
  - **Unity y Gnome:** Modernos, modulables y amigables para el usuario (usados frecuentemente en Ubuntu) .
  - **KDE y Pantheon:** Interfaces similares a Windows y MacOS X respectivamente .
  - **LXDE y XFCE:** Entornos ligeros diseñados para ordenadores con pocos recursos.  
    <br>

## **3\.** Paquetes

Un paquete de Linux como el equivalente a un instalador .exe en Windows o a un archivo .zip muy bien organizado. Básicamente, es un **fichero comprimido** que ya tiene todo lo necesario para "construir" y ejecutar una aplicación en tu sistema.

No todos los sistemas Linux son idénticos; existen distintas "distribuciones" (como marcas o versiones) y cada familia utiliza un tipo de paquete diferente:

- **DEB:** Es el formato que utilizan distribuciones muy populares como Ubuntu, Linux Mint, Kubuntu y ZorinOS. Este archivo ya trae la aplicación lista para usarse (ejecutables), junto con sus archivos de configuración, manuales (documentación).
- **RPM:** Este lo utilizan sistemas de la familia RedHat, como Fedora o openSUSE. Su mayor ventaja es cómo maneja las actualizaciones.
- **Ebuild:** Es un formato exclusivo de una distribución llamada Gentoo. No es un programa empaquetado como tal, sino que son _scripts de Bash_ (archivos de texto con una serie de comandos) que le dan las instrucciones exactas a tu ordenador sobre cómo descargar, preparar y compilar el programa desde cero.
- **TGZ:** A diferencia de los anteriores, estos paquetes suelen contener el **código fuente** de la aplicación, que deberá ser compilado a código máquina.  
  <br>

## **4\.** Ubuntu

Es una distribución de Linux orientada a la facilidad de uso, ideal para usuarios principiantes e intermedios.

- **Características** **técnicas**: Su interfaz predeterminada es Unity (complementada con aplicaciones de Gnome) y utiliza el formato de paquetes **.DEB** para la instalación de software.
- **Versiones principales:**
  - **Desktop:** Orientado a ordenadores de escritorio.
  - **Server:** Diseñado para servidores.
  - **Phone:** Versión para smartphones que actualmente está en desuso.
- **Principales Ventajas**
  - **Comunidad activa:** Dispone de un gran grupo de desarrolladores que se encarga de escribir código, corregir vulnerabilidades y proponer mejoras.
  - **Compatibilidad:** Permite usar aplicaciones diseñadas para otros entornos de escritorio (como Gnome) gracias a la flexibilidad de Unity.
  - **Facilidad de uso**.
  - **Seguridad y Estabilidad:** Es un sistema muy estable gracias a la potencia de los permisos de superusuario (sudo). Además, no incluye un cortafuegos por defecto porque la instalación base no instala servicios que supongan un riesgo de seguridad.
- **Requisitos de Instalación:** Los requisitos técnicos varían dependiendo de la versión exacta que se quiera instalar. Como ejemplo, para **Ubuntu Server 12.04 LTS**, las especificaciones recomendadas son muy ligeras:
  - **Procesador de 32 bits a 700 MHz.**
  - 512 MB de memoria RAM.
  - 5 GB de espacio libre en el disco duro.
  - Tarjeta gráfica y monitor compatibles con una resolución mínima de 1024x768.  
    <br>

## **5\.** Sistema **de archivos en Linux**

Esta organización no es una coincidencia, sino que se rige por un documento oficial llamado **FHS (Filesystem Hierarchy Standard o Estándar de Jerarquía del Sistema de Archivos)**.

- **Programas y Ejecutables**
  - /**bin**: Contiene los comandos y programas esenciales para el uso básico de la máquina.
  - /**sbin**: Guarda las órdenes y programas destinados exclusivamente a la administración del sistema.
  - /**usr**: Aloja programas esenciales de la máquina, típicamente utilizado en redes de ordenadores.
  - /**usr**/**local**: Aquí se guardan los programas que tú instalas manualmente y que no venían por defecto con tu distribución de Linux.
- **Configuración y Sistema Base**
  - /**boot**: Almacena toda la información necesaria para el arranque (inicio) del sistema.
  - /**etc**: Contiene los ficheros de configuración del sistema operativo.
  - /**lib**: Guarda las bibliotecas (librerías) esenciales que necesitan los programas para funcionar.
- **Usuarios y Datos Variables**
  - /**home**: Es el directorio donde se guardan las carpetas y archivos personales de cada usuario.
  - /**var**: Almacena información que cambia constantemente, como los buzones de correo o los registros (logs) del sistema.
  - /**tmp**: Carpeta destinada a guardar ficheros temporales.
- **Dispositivos y Procesos**
  - /**dev**: Contiene los ficheros que representan los dispositivos físicos de hardware conectados.
  - /**mnt**: Es el directorio o carpeta principal que se usa como "punto de montaje" para acceder a dispositivos externos (como USBs) o recursos de red.
  - /**proc**: Es un directorio virtual. No ocupa espacio real en el disco, sino que muestra información en tiempo real sobre el hardware y los programas que se están ejecutando.  
    <br>

## **6\. Administración del Sistema**

- **Usuarios y Permisos (Root):**
  - **Root:** Es el superusuario o administrador con acceso total al sistema (Este usuario tiene permisos de lectura, escritura y ejecución de cualquier aplicación del sistema)
  - Se utilizan los **comandos su** o **su \[nombre del usuario\]** para cambiar temporalmente de usuario en un terminal (Generalmente de un usuario normal a root), o **sudo** para ejecutar comandos individuales con privilegios de administrador sin cambiar la sesión actual .

Esto es útil para administrar bases de datos, servidores web y otros servicios que disponen de usuarios específicos para realizar diferentes tareas de administración.

- Después de ingresar tu contraseña tendrás 15 minutos para seguir utilizando la cuenta como superusuario. Pasado este tiempo volverás a tener los privilegios de tu cuenta de usuario normal.

Pero si queremos tener privilegios de superusuario de forma permanente sin necesidad de ingresar SUDO varias veces podemos ejecutar en la terminal: **sudo su .**

- En algunas distribuciones de Linux (Ubuntu, Kubuntu) la cuenta de superusuario viene desactivada por defecto. En estos casos, la cuenta de usuario que creamos al instalar la distribución no es la misma que la cuenta de root o superusuario, sino que pertenece al grupo de administradores. Para obtener privilegios de root se utiliza el comando SUDO.
  - Antes de cerrar el terminal, es recomendable volver a nuestro propio usuariocon un simple exit.

Para saber con qué usuario estás logueado, basta con observar el símbolo de la línea de comandos:

usuario@usuario-desktop:~\$ Es la cuenta del usuario normal (\$).root@usuario-desktop:~# Es la cuenta de root (#).

- Las cuentas de usuario y contraseñas (cifradas) se gestionan a través de los ficheros /etc/passwd y /etc/shadow.  
  <br>

## **7\. Variables de Entorno:** Son valores dinámicos o "contenedores" de parámetros que modifican el comportamiento de los procesos en el sistema.

Actúan como atajos de texto fáciles de recordar. Te permiten acceder a rutas o configuraciones extremadamente largas y complejas (como la variable Path) usando una sola palabra, lo que ahorra tiempo y evita errores.

- **Gestión de Variables (Comandos)**
  - **Ver o acceder a una variable:** Se utiliza el símbolo de dólar \$ seguido del nombre de la variable.
  - **Crear o establecer una variable:** Se utiliza el comando export seguido del nombre y el valor que le quieras asignar.  
    <br>

## **8\. Ayuda en línea:** Linux proporciona páginas de manuales de ayuda en línea para describir comandos y aplicaciones del sistema con bastante detalle.

- **man \[sección\] &lt;orden&gt;:** Es la herramienta clásica de Linux. Muestra el "manual" (man pages) de un comando.
  - **Orden info:** Es una alternativa al comando man. Mientras que man muestra una sola página larga, info suele ofrecer documentación más moderna y estructurada en formato hipertexto.  
    <br>

## **9\. ¿Qué es el PATH?**

El **PATH** es una variable de entorno fundamental que actúa como un "mapa" para el intérprete de comandos (el _shell_, que generalmente es BASH). Su función principal es decirle al sistema en qué carpetas debe buscar los programas (binarios) cuando se escribe una orden en la terminal.

(Gracias al PATH se evita tener que escribir la ruta absoluta de donde está guardado un programa cada vez que se quiera usarlo.

- **Explicación paso a paso con un ejemplo:**

Para saber dónde está instalado un comando, usamos whereis.

(Si usamos \$ whereis ls , el sistema nos dirá que el archivo binario ejecutable de ls está guardado en la ruta /usr/bin/ls).

- **Dos formas de ejecutar un programa:**
  - **Ruta absoluta:** Se puede llamar al programa escribiendo su dirección completa: \$ /usr/bin/ls.
  - **Ejecución directa:** Simplemente escribiendo \$ ls.

Precisamente gracias al PATH. Al escribir ls, el sistema lee la variable PATH y empieza a buscar el archivo "ls" carpeta por carpeta en el orden en el que están listadas. Como la carpeta /usr/bin (donde sabemos que está ls) forma parte del PATH, el sistema lo encuentra y lo ejecuta automáticamente sin tener que decirle dónde está.

Para ver las carpetas donde el sistema busca los programas se ejecuta \$ echo \$PATH.  
<br>

## **10\. Ejecución en segundo plano**

**Ejecutar** un programa de forma "invisible" (en segundo plano) para que siga trabajando y consumiendo recursos. **Liberar** la terminal para poder seguir escribiendo otros comandos sin tener que esperar a que termine la tarea anterior.

- **Lanzar un proceso en segundo plano**
  - Añadir el **símbolo &** (ampersand) justo al final del comando para enviarlo al fondo.
  - Realizar tareas largas silenciosamente sin bloquear la **pantalla (por ejemplo: find / -iname "\*.sh" > listadescripts.txt &).**
  - Utilizar el **comando jobs para comprobar y listar** rápidamente las tareas enviadas al segundo plano.
- **Monitorizar el estado de los procesos**
  - Comprobar el estado en el que se encuentran todos los procesos de la máquina, tanto los de segundo plano como los normales.
  - Utilizar herramientas de visualización del sistema, como el **comando** clásico **ps** (**o top**), para obtener esta información.
- **Detener o eliminar un proceso**
  - Utilizar la **orden kill** seguida del identificador del proceso (PID) para cancelar la ejecución, detener un programa bloqueado o corregir una equivocación.
  - Escribir **kill %1 para mandar la señal de terminación de forma rápida y directa al trabajo que se encuentra en la parte superior de la pila** de trabajos en segundo plano.  
    <br>

## **11\. Permisos y Propiedad de Archivos**

- **Niveles de Permiso:** Se aplican al Usuario Propietario (u), Grupo (g) y Resto de usuarios (o).

En Unix no existe la posibilidad de asignar permisos a usuarios concretos ni a grupos concretos, tan solo se puede asignar permisos al usuario propietario, al grupo propietario o al resto de usuarios.

- **Lectura (r / 4):** Permite ver contenido o listar directorios .
  - **Escritura (w / 2):** Permite modificar, añadir o borrar .
  - **Ejecución (x / 1):** Permite ejecutar programas o entrar en directorios.  
    <br>

```text
-   rw-  r--  r--
┬    ┬    ┬    ┬
│    │    │    └──────> Acceso permitido a alguien que no es dueño - other
│    │    └───────────> Acceso permitido a los miembros del grupo - group
│    └────────────────> Acceso permitido al dueño - user
└─────────────────────> Tipo de archivo (archivo, directorio, dispositivo, etc)
```

<br>

**El primer carácter indica de qué tipo de archivo se trata:**

\- Si es un **guión** '-' significa que se trata de un **archivo normal.**

\- La **letra 'd'** significa que se trata de una **carpeta (directory).**

\- La **letra 'l'** significa que se trata de un **enlace (link).**

\- Otros valores son **s, p, b que se refieren a sockets, tuberías (pipe) y dispositivos de bloque respectivamente.**  
<br>

## **12\. Cambio de permisos**

**Requisito indispensable:** Para modificar los permisos de un archivo o carpeta, debes tener el permiso de escritura (w) sobre el mismo.

**Comando y sintaxis:** Se utiliza el **comando chmod siguiendo la estructura: chmod \[opciones\] permiso nombre_archivo_o_carpeta.**

**Tipos de representación:** Los permisos se pueden configurar de forma manual (ideal para entornos de servidores) utilizando dos métodos principales: el simbólico y el numérico.

- **Método Simbólico**

Este método utiliza letras para definir quién recibe el permiso, qué acción se realiza y qué tipo de permiso se otorga:

- **A quién:** u (usuario/dueño), g (grupo), o (otros/resto).
  - **Acción:** + (añadir permiso) o - (quitar permiso).
  - **Tipo de permiso:** r (lectura), w (escritura), x (ejecución).

**Ejemplo:** chmod ug+rw notas.txt (Añade permisos de lectura y escritura al usuario y al grupo).

- **Método Numérico**

Utiliza un código de tres cifras (del 0 al 7) para asignar permisos rápidamente. El orden de las cifras siempre es: **1º Usuario, 2º Grupo, 3º Otros**.

Los números surgen de una lógica binaria donde cada bit representa un permiso. Los valores resultantes más importantes son:

- **0**: Ningún permiso (---).
  - **4**: Sólo lectura (r--).
  - **5**: Lectura y ejecución (r-x).
  - **6**: Lectura y escritura (rw-).
  - **7**: Todos los permisos (rwx).

**Ejemplos prácticos de modo numérico:**

chmod 700 examenSI.txt: Todos los permisos para el usuario, ninguno para el grupo ni el resto.

chmod 755 /usr/bin/games/csgo: Todos los permisos al usuario; lectura y ejecución al grupo y al resto.

chmod 744 \*: Todos los permisos al usuario; sólo lectura al resto, aplicándolo a todos los archivos.  
<br>

## **13\. Cambio de propietarios**

Además de los permisos, el sistema permite cambiar de forma directa qué usuario y qué grupo son los propietarios legítimos de un fichero o de un directorio mediante el comando **chown.**

La estructura básica para utilizarlo es:

**chown \[opciones\] usuario\[:grupo\] fichero**

Ejemplo

\>/ chown aitor.users prueba  
<br>

## **14\. Gestión de Dispositivos y Almacenamiento**

- **Sistemas de Ficheros:** Para acceder a una unidad (como un CD, disco duro o pendrive) es necesario montarla en un directorio usando mount y desmontarla con umount.
- **Arranque y Mantenimiento:** El archivo /etc/fstab controla los dispositivos montados al arrancar, mientras que comandos como fsck y mkfs se utilizan para verificar y formatear unidades.  
  <br>

## **15\. Comandos Básicos para la Administración**

- **Navegación y Archivos:** cd (cambiar directorio), ls (listar), mkdir (crear carpetas), rm (borrar), cp (copiar), y mv (mover/renombrar) .
- **Visualización y Texto:** cat, more, less, head, tail (para ver archivos) y grep, sed (para filtrar o manipular texto) .
- **Búsqueda:** find, locate, whereis .
- **Procesos y Rendimiento:** ps, top y htop para ver recursos, y kill para terminar tareas, además del envío de procesos a segundo plano usando &.
- **Paquetes:** Uso de apt-get (descarga e instalación en red) o dpkg (archivos locales .deb) para gestionar software.
- **Compresión:** Utilidades como tar, gzip, zip y rar para agrupar y comprimir datos .
- **Redes:** Comandos como ifconfig (interfaces de red), route (rutas), netstat (conexiones) e iptables (configuración del cortafuegos).  
  <br>

**Gestión de Archivos y Directorios**

| **Comando** | **Función principal**                   | **Ejemplo**                       |
| ----------- | --------------------------------------- | --------------------------------- |
| **pwd**     | Muestra la ruta actual                  | pwd                               |
| **cd**      | Cambia de directorio                    | cd /home/usuario                  |
| **ls**      | Lista archivos y carpetas               | ls -l                             |
| **mkdir**   | Crea un directorio nuevo                | mkdir carpeta                     |
| **touch**   | Crea archivos vacíos o actualiza fechas | touch nuevo.txt                   |
| **cp**      | Copia archivos o carpetas               | cp origen destino                 |
| **mv**      | Mueve o renombra archivos               | mv viejo.txt nuevo.txt            |
| **rm**      | Elimina archivos o carpetas             | rm archivo.txt                    |
| **tar**     | Comprime o descomprime archivos         | tar -czvf archivo.tar.gz carpeta/ |

**Visualización y Búsqueda**

| **Comando** | **Función principal**                       | **Ejemplo**               |
| ----------- | ------------------------------------------- | ------------------------- |
| **cat**     | Muestra contenido de un archivo             | cat archivo.txt           |
| **less**    | Visualiza archivos por páginas              | less archivo.log          |
| **head**    | Muestra las primeras líneas de un archivo   | head -n 10 archivo.txt    |
| **tail**    | Muestra las últimas líneas (útil para logs) | tail -f /var/log/syslog   |
| **find**    | Busca archivos y carpetas                   | find /home -name "\*.txt" |
| **grep**    | Busca texto dentro de archivos              | grep "error" log.txt      |
| **echo**    | Imprime texto o variables                   | echo "Hola Mundo"         |

**Administración del Sistema y Procesos**

| **Comando** | **Función principal**                    | **Ejemplo**     |
| ----------- | ---------------------------------------- | --------------- |
| **whoami**  | Muestra el usuario actual                | whoami          |
| **df**      | Muestra espacio libre en discos          | df -h           |
| **du**      | Muestra el tamaño de archivos o carpetas | du -sh carpeta/ |
| **ps**      | Muestra procesos activos                 | ps aux          |
| **top**     | Monitorea recursos en tiempo real        | top             |
| **htop**    | Versión visual de top                    | htop            |
| **pstree**  | Muestra procesos en forma de árbol       | pstree          |

**Permisos y Paquetes**

| **Comando** | **Función principal**                             | **Ejemplo**                    |
| ----------- | ------------------------------------------------- | ------------------------------ |
| **sudo**    | Ejecuta comandos con privilegios de administrador | sudo apt update                |
| **chmod**   | Cambia permisos de archivos                       | chmod 755 script.sh            |
| **apt**     | Gestor de paquetes                                | apt-get install/update/upgrade |

**Utilidades y Ayuda**

| **Comando** | **Función principal**             | **Ejemplo** |
| ----------- | --------------------------------- | ----------- |
| **man**     | Muestra el manual de un comando   | man ls      |
| **history** | Muestra el historial de comandos  | history     |
| **clear**   | Limpia la pantalla de la terminal | clear       |
