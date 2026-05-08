# UNIDAD 6 - Windows - CMD y administración básica

## INTRODUCCIÓN A WINDOWS SERVER - Roles, Active Directory, DNS/DHCP

### Requisitos RECOMENDADOS para Windows Server 2019

- **Procesador:** 1,4 GHz.
- **Arquitectura:** 64 bits.
- **Memoria RAM:** 2 GB.
- **Espacio en disco:** 15 GB _(Hay que prever un espacio más o menos coherente en función del rol del servidor)_.
- **Otros dispositivos:** Monitor Super VGA (800 x 600) +, teclado y ratón.

### Instalación de Windows Server 2019

_(En una nueva máquina virtual)_

> **Recomendación:** Prestar atención a las credenciales de Administrador.

**Nombre y sistema operativo**

- **Nombre:** WindowsServer2019
- **Tipo:** Microsoft Windows (Estándar para Escritorio)
- **Versión:** Windows 2019 (64bit)
- **OMITIR INSTALACIÓN DESATENDIDA** ✅

**Características de la máquina virtual**

- **Tamaño de memoria:** 2048MB
- **Crear nuevo disco duro virtual:**
  - **Tipo:** VDI
  - **Tamaño:** 50GB
- **Sistema:** 2 procesadores
- **Red:** Adaptador puente -> tarjeta de red del equipo físico

---

## PROCESOS EN WINDOWS

Un proceso es un programa en ejecución. Si pulsamos con botón derecho sobre cualquier columna, como "Nombre" y a continuación damos en "Seleccionar columnas" podremos acceder a todas las **columnas o propiedades** que describen a los procesos:

**1. Para identificar qué es cada cosa (y buscar malware)**

- **Descripción:** Es lo primero que debes mirar. En lugar de un nombre críptico como `spoolsv.exe`, la descripción te dirá "Subsistema de cola de impresión". Te ayuda a entender rápidamente para qué sirve el proceso.
- **Nombre de ruta de la imagen:** Es vital para la seguridad. Si ves un proceso con un nombre común (como `svchost.exe` o `explorer.exe`) pero la ruta de la imagen no está en `C:\Windows\System32` o `C:\Windows`, es muy probable que sea un virus disfrazado.
- **Línea de comandos:** Súper útil para usuarios avanzados. Hay procesos genéricos como `svchost.exe` (que aloja servicios de Windows) o `chrome.exe` (que abre muchas pestañas). La línea de comandos te muestra los parámetros exactos con los que se ejecutó, ayudándote a saber exactamente qué pestaña, extensión o servicio de Windows específico está corriendo bajo ese nombre.

**2. Para controlar el rendimiento y los "cuellos de botella"**

- **Uso de CPU:** Fundamental. Si tu ordenador va lento o los ventiladores suenan muy fuerte, ordena la lista por esta columna. Te dirá qué aplicación está acaparando la capacidad de procesamiento en tiempo real.
- **Memoria: espacio de trabajo privado:** De todas las columnas de memoria, **esta es la más importante para el usuario**. Te indica la cantidad real de memoria RAM que un programa está usando de forma exclusiva y que no comparte con nadie más. Si un programa tiene una "fuga de memoria" (_memory leak_), verás que este número no para de crecer.
- **Lecturas/Escrituras de E/S (y Bytes de E/S):** Las siglas E/S significan Entrada/Salida (I/O en inglés). Estas columnas te indican qué programa está leyendo o escribiendo datos activamente en tu disco duro o a través de la red. Si el disco duro está al 100% de uso y todo va a tirones, estas columnas te dirán el culpable.

**3. Para gestión avanzada y solución de problemas**

- **Identificador de proceso (PID):** Es el "DNI" del proceso. Si tienes 15 procesos llamados `chrome.exe` y uno se ha quedado colgado, el PID es la única forma de diferenciarlos. Es imprescindible si alguna vez necesitas forzar el cierre de un programa usando la consola de comandos (CMD) con el comando `taskkill`.
- **Subprocesos (Threads):** Un proceso principal puede dividirse en múltiples tareas pequeñas (subprocesos). Si un programa tiene un número anormalmente alto de subprocesos (miles) o no para de crear nuevos sin cerrar los antiguos, indica que el programa está mal optimizado o tiene un error.

> **En resumen:** Si configuras tu Administrador de tareas para que muestre el **PID, la Descripción, el Uso de CPU, la Memoria (espacio de trabajo privado) y la Ruta de la imagen**, tendrás el 95% de la información que necesitas para mantener tu sistema sano y entender qué está ocurriendo bajo el capó.

---

## SERVICIOS

Son aplicaciones que se inician automáticamente cuando el equipo arranca, se pueden pausar y reiniciar, y no muestran ninguna interfaz de usuario.

### Servicios: Pestaña "General"

Los principales campos son:

- Ruta de acceso al ejecutable.
- Tipo de inicio: Automático, Manual y Deshabilitado.
- Estado del servicio.
- Botones: Iniciar / Detener / Pausa / Reanudar.

### Servicios: Pestaña "Recuperación"

Los principales campos son:

- **Primer/Segundo/Siguientes errores:** Acción o acciones que se realizarán durante los intentos de recuperación al fallar el servicio.
- **Reiniciar el servicio después de:** Número de minutos.
- **Programa:** Archivo que se ejecutará si falla el servicio.

### Servicios: Pestaña "Dependencias"

Los principales campos son:

- En la ventana superior, se muestran los servicios de los que _depende_ el servicio seleccionado.
- En la ventana inferior, se muestran los servicios que _dependen_ del servicio seleccionado.

---

## MONITORIZACIÓN DE EVENTOS

Un evento o suceso es un acontecimiento significativo del sistema o de una aplicación que requiere una notificación al usuario.

Los tipos de sucesos son: Crítico, Error, Advertencia, Información, Auditoría correcta, Error de auditoría.

### Visor de eventos

El visor de eventos es la herramienta que permite examinar y administrar los eventos ocurridos en el equipo. Los registros de eventos que se muestran en un controlador principal de dominio son:

- **Vistas personalizadas.**
- **Registros de Windows.**
- **Registros de aplicaciones y servicios.**
- **Suscripciones.**
- **Aplicación.**
- **Seguridad** -> cambios en el sistema de seguridad o fallos.
- **Instalación** -> del SO o sus componentes.
- **Sistemas** -> Componentes de Windows. (Reinicios planeados).
- **Eventos reenviados** -> Equipos remotos.

### Utilidad

Por ejemplo, si obtenemos un pantallazo azul o se nos reinicia aleatoriamente el equipo, el Visor de eventos puede darnos más información sobre la causa.

Ejemplo: un evento de error en la sección de registro del sistema puede informarnos qué controlador de hardware colapsó, lo que puede ayudar a identificar un controlador defectuoso o un componente de hardware defectuoso. Solo deberemos buscar el mensaje de error asociado con la hora en que el ordenador "petó" o reinició: un mensaje de error sobre la congelación del ordenador se marcará como Crítico.

---

## VARIABLES DE ENTORNO

Las variables de entorno son un conjunto de valores DINÁMICOS que afectan al comportamiento de los procesos. Estas variables de entorno puede ser consultadas y modificadas en scripts y en líneas de comandos.

La manera de acceder a una variable de entorno depende del SO:

- En **Windows** puedes acceder con: `echo %nombrevariable%`
- En **Linux** se accedería con: `echo $nombrevariable`

El sistema cuenta con sus propias variables, que toman valor cuando se inicia el Sistema. Si queremos ver dichas variables, podemos usar la orden `SET`, que nos muestra una lista de variables ya definidas. Podemos definir nuestras propias variables sin ningún tipo de problemas, basta con poner `SET nombre_de_variable=valor`. Es importante no dejar espacios ni delante ni detrás del símbolo `=`.

**Las variables de entorno típicas de un sistema Windows, son las siguientes:**

| **Variable**               | **Tipo**   | **Descripción**                                                                                                    |
| :------------------------- | :--------- | :----------------------------------------------------------------------------------------------------------------- |
| `%ALLUSERSPROFILE%`        | Local      | Devuelve la ubicación de perfil Todos los usuarios.                                                                |
| `%USERPROFILE%`            |            | Apunta a la carpeta principal del usuario (`C:\Users\TuUsuario`). Muy usada en scripts y automatización.           |
| `%APPDATA%`                | Local      | Devuelve la ubicación en que las aplicaciones guardan los datos de forma predeterminada.                           |
| `%CD%`                     | Local      | Devuelve la cadena del directorio actual.                                                                          |
| `%CMDCMDLINE%`             | Local      | Devuelve la línea de comandos exacta utilizada para iniciar el `Cmd.exe` actual.                                   |
| `%CMDEXTVERSION%`          | Sistema    | Devuelve el número de versión de Extensiones del procesador de comandos actual.                                    |
| `%COMPUTERNAME%`           | Sistema    | Devuelve el nombre del equipo.                                                                                     |
| `%COMSPEC%`                | Sistema    | Devuelve la ruta de acceso exacta al ejecutable del shell de comandos.                                             |
| `%DATE%`                   | Sistema    | Devuelve la fecha actual. Utiliza el mismo formato que el comando `date /t`. Generado por `Cmd.exe`.               |
| `%ERRORLEVEL%`             | Sistema    | Devuelve el código de error del último comando utilizado. Valores distintos de cero indican error.                 |
| `%HOMEDRIVE%`              | Sistema    | Devuelve la letra de unidad del directorio principal del usuario.                                                  |
| `%HOMEPATH%`               | Sistema    | Devuelve la ruta completa del directorio principal del usuario.                                                    |
| `%HOMESHARE%`              | Sistema    | Devuelve la ruta de red del directorio principal compartido del usuario.                                           |
| `%LOGONSERVER%`            | Local      | Devuelve el nombre del controlador de dominio que validó la sesión actual.                                         |
| `%NUMBER_OF_PROCESSORS%`   | Específico | El número de procesadores instalados en el equipo.                                                                 |
| `%OS%`                     | Sistema    | Devuelve el nombre del sistema operativo.                                                                          |
| `%PATH%`                   | Sistema    | Especifica la ruta de búsqueda para los archivos ejecutables.                                                      |
| `%PATHEXT%`                | Sistema    | Devuelve una lista de extensiones de archivo consideradas ejecutables.                                             |
| `%PROCESSOR_ARCHITECTURE%` | Sistema    | Devuelve la arquitectura del procesador (x86, IA64, etc.).                                                         |
| `%PROCESSOR_IDENTIFIER%`   | Sistema    | Devuelve una descripción del procesador.                                                                           |
| `%PROCESSOR_LEVEL%`        | Sistema    | Devuelve el número de modelo del procesador.                                                                       |
| `%PROCESSOR_REVISION%`     | Sistema    | Devuelve el número de revisión del procesador.                                                                     |
| `%PROMPT%`                 | Local      | Devuelve la configuración del símbolo del sistema del intérprete actual.                                           |
| `%RANDOM%`                 | Sistema    | Devuelve un número decimal aleatorio entre 0 y 32767.                                                              |
| `%SYSTEMDRIVE%`            | Sistema    | Devuelve la unidad que contiene el directorio raíz del sistema operativo.                                          |
| `%SYSTEMROOT%`             | Sistema    | Devuelve la ubicación del directorio del sistema operativo Windows.                                                |
| `%TEMP%` y `%TMP%`         |            | Directorios temporales. Importantísimos para instalaciones, compilaciones y programas.                             |
| `%TIME%`                   |            | Muy usadas para logs, copias de seguridad y automatización.                                                        |
| `%WINDIR%`                 |            | Nos llevaría al directorio de Windows.                                                                             |
| `%USERNAME%`               |            | Devuelve el **nombre de la cuenta de usuario** que ha iniciado sesión actualmente en el sistema operativo Windows. |

> Algunas de estas variables son especialmente importantes, ya que se nos permite automatizar muchos procesos de Administración. Por ejemplo, **si tenemos que ir al directorio Windows para retocar algunos ficheros y en nuestro servidor disponemos de varios sistemas operativos y varios volúmenes de datos,** podemos perder mucho tiempo en buscar donde está situado. Pues **un simple `CD %WINDIR%` nos llevaría al directorio de Windows** sin posibilidad de error.

---

## LA LÍNEA DE COMANDOS DE WINDOWS

_(Sirve para gestionar el sistema desde una pantalla de texto plano)._

El shell de comandos es un programa de software independiente que proporciona comunicación directa entre el usuario y el sistema operativo. La línea de comandos tiene varias ventajas sobre el IGU, como pueden ser:

- En caso de estar usando herramientas recuperación para corregir un problema de software importante, necesitaremos la línea de comandos porque seguramente será lo único con lo que contemos (En caso de error grave y que no podamos dar solución mediante interfaz gráfica, casi con total seguridad podremos dar una solución mediante la línea de comandos).
- Muchas órdenes de gestión del sistema operativo, que se consideran de muy bajo nivel o muy peligrosas, no son accesibles desde el IGU.
- Podemos abrir sesiones remotas en nuestro equipo desde otras ubicaciones.
- Podemos tener varias sesiones con entorno de texto concurrentes.
- Podemos automatizar las órdenes usando los lenguajes de programación del propio sistema operativo (Estos programas por lotes se conocen como scripts, procesos por lotes o archivos _batch_ y nos ofrecen muchas posibilidades).

### Uso De La Ayuda En El Shell De Comandos

Una de las principales habilidades que debe desarrollar un Administrador de Sistemas, consiste en usar correctamente la ayuda.

- Disponemos de una ayuda general accesible mediante la orden `HELP`.
- Si queremos ayuda específica sobre cualquier comando, podemos ejecutar `HELP comando`.
- También podemos acceder a la ayuda de un comando escribiendo `comando /?`.

### Configuración Del Shell De Comandos

Para configurar el símbolo del sistema:

1.  Abrimos Símbolo del sistema.
2.  Hacemos clic en la esquina superior izquierda de la ventana del símbolo del sistema y, a continuación, hacemos clic en Propiedades. _(Conseguimos lo mismo si pulsamos la Tecla Alt + Barra espaciadora)._

En _Historial de comandos_, en _Tamaño del búfer_ si escribimos `999` y, a continuación, en _Número de búferes_ escribimos o seleccionamos `5` mejoraremos el tamaño y el comportamiento del buffer de comandos (que nos permite acceder a lo escrito anteriormente con los cursores).

Para salir del modo de pantalla completa: Pulsa el atajo de teclado **Alt + Enter**.

### Uso De Comodines

Los comodines son caracteres del teclado como el asterisco (`*`) o el signo de interrogación (`?`) que se pueden utilizar para representar uno o más caracteres reales al buscar archivos o carpetas. A menudo, los comodines se utilizan en lugar de uno o varios caracteres cuando no se sabe el carácter real o no se desea escribir el nombre completo.

- **Asterisco (`*`):** Podemos utilizar el asterisco como sustituto de cero o más caracteres.
  - Si buscamos un archivo que sabemos que comienza por "glos" pero no recordamos el resto del nombre del archivo, escribimos lo siguiente: `glos*`. Con esto, buscaremos todos los archivos de cualquier tipo que comiencen por "glos", incluidos _Glosario.txt_, _Glosario.doc_ y _Glos.doc_.
  - Para limitar la búsqueda a un tipo de archivo específico, escribimos: `glos*.doc`. En este caso, buscaremos todos los archivos que comiencen por "glos" pero con la extensión .doc, como _Glosario.doc_ y _Glos.doc_.

- **Signo de interrogación (`?`):** Podemos utilizar el signo de interrogación como sustituto de un único carácter en un nombre.
  - Por ejemplo, si escribimos: `glos?.doc` encontraremos los archivos _Glosa.doc_ y _Glos1.doc_, pero no _Glosario.doc_.

### Principales comandos

En el shell de comandos de Windows, existen cientos de comandos que pueden ser utilizados. Muchos de ellos se instalan directamente con Windows, mientras que otros especiales se instalan conjuntamente con otras herramientas. Veamos los más habituales:

- `VER` - Muestra la versión del sistema operativo
- `Unidad:` - Cambia la unidad activa - `C:` `D:` `E:` `A:`
- `HELP` - Muestra una pequeña ayuda sobre los comandos
- `DIR` - Visualiza el contenido de un directorio
- `ECHO` - Muestra mensajes o activa/desactiva el eco local
- `FORMAT` - Formatea una unidad (¡¡¡cuidaooo!!!)
- `DISKCOPY` - Copia un disquete - `DISKCOPY A: B:`
- `CHKDSK` - Comprueba el estado de un disco - `CHKDSK A:`
- `VOL` - Muestra la etiqueta de un disco
- `LABEL` - Cambia la etiqueta de un disco
- `CLS` - Limpia la pantalla
- `TIME` - Muestra y permite cambiar la hora
- `DATE` - Muestra y permite cambiar la fecha
- `COPY` - Permite copiar ficheros
- `XCOPY` - Copy extendido. Dispone de modificadores exclusivos. RECURSIVIDAD.
- `ROBOCOPY` - Toma las cualidades de los conocidos COPY y XCOPY y las perfecciona al máximo.
- `MOVE` - Mueve ficheros
- `DEL` - Borra ficheros
- `REN` - Renombra ficheros
- `ATTRIB` - Muestra o cambia los atributos del archivo
- `TYPE` - Permite visualizar (leer) por pantalla el contenido de archivos de texto
- `CHDIR` - Directorio actual
- `&` - Para concatenar dos comandos en uno
- `^` - Para escapar un carácter especial
- `MKDIR` (`MD`) - Crea un directorio
- `RMDIR` (`RD`) - Borra directorios
- `CHDIR` (`CD`) - Cambia de directorio actual
- `TREE` - Muestra la estructura de directorios
- `COPY CON <nombrefichero>` - Permite crear un nuevo fichero con contenido desde el propio CMD de una manera sencilla y rápida: Para finalizar la edición del fichero pulsaremos **CTRL+Z** seguido de **INTRO**.
- `DOSKEY` - Utilidad para recordar líneas de comandos.
  - _Ej: Si hacemos `DOSKEY c= calc.exe` ; Ahora escribiendo la letra `c` y presionando la tecla Enter, se abre la Calculadora._
  - _(Con DOSKEY se pueden crear macros, pequeñas funciones que se cargan en la memoria de la consola y al ejecutarlos reproducen los comandos que los componen)._
- `PAUSA` - Podemos pausar la salida de una ejecución que vaya a devolver una gran cantidad de información.
  - _Por ejemplo, si accedemos a la ruta `C:\Windows\System32` y hacemos un `DIR` para listar todo su contenido, obtendremos un gran listado que pasará por pantalla "súper rápido". Para solucionarlo, debemos colocar el parámetro `/p` junto a `DIR`:_

---

## REDIRECCIONAMIENTOS Y TUBERÍAS

Cualquier software que ejecutemos en nuestro sistema informático, va a procesar una información que le llega desde una ENTRADA y va a enviar el resultado del proceso a una SALIDA. Si no indicamos nada, se supone que la entrada será desde el dispositivo por defecto de entrada (`stdin`) y la salida será al dispositivo por defecto de salida (`stdout`).

**`stdin` y `stdout` se refieren a la consola.**

Con los redireccionamientos, podemos indicar a las órdenes qué entrada, salida y salida de errores deben usar, evitando que usen las Standard. Estos redireccionamientos son los siguientes:

| **Operador** | **Descripción**                                                                                                                                                                      |
| :----------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     `>`      | Redirecciona `stdout`. Es decir, nos permite indicar una salida para la orden que no sea CON (monitor).                                                                              |
|     `2>`     | Redirecciona `stderror`. Es decir, nos permite indicar una salida para los errores de la orden que no sea CON (monitor).                                                             |
|     `<`      | Redirecciona `stdin`. Es decir, nos permite indicar una entrada para la orden que no sea CON (teclado).                                                                              |
|     `>>`     | **Igual que `>`, pero la salida de la orden se añade a la salida que indiquemos. Con `>` la salida de la orden reescribe la salida que indiquemos.**                                 |
|   `&#124;`   | **El indicador de tubería.** Nos permite indicar que la entrada de una orden será la salida de otra orden. Es decir, **el `stdout` de la 1ª orden, será el `stdin` de la 2ª orden.** |

### Filtros

- `SORT` - Nos permite ordenar una salida alfabéticamente. Con `HELP SORT` podemos ver todos sus posibles parámetros.
- `FIND` - Nos permite filtrar una salida, haciendo que solo aparezcan las líneas que contengan una palabra, las que no contengan una palabra, que contemos las líneas que contienen una palabra, etc.
- `MORE` - Nos permite obtener una salida por pantalla paginada. Es decir, cada vez que la pantalla se llene, nos pide que pulsemos una tecla antes de continuar escribiendo texto.
