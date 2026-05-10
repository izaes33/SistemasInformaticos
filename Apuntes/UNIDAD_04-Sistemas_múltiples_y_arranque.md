# UNIDAD 04 - Gestión de Sistemas múltiples y arranque

En la práctica, todos los ordenadores modernos (PCs, Mac, portátiles, servidores) necesitan de forma obligatoria un sistema de particiones en su unidad de almacenamiento principal (ya sea un disco duro, un SSD o un M.2) para poder funcionar.

Un disco recién salido de fábrica es básicamente un espacio de almacenamiento en bruto, como un inmenso terreno vacío. El sistema de particiones (los famosos MBR o GPT) es el "plano" o "mapa" que organiza ese terreno.  
<br>

## Tablas de Particiones: MBR vs. GPT

Para organizar los discos duros, existen dos estándares principales:

- **MBR (Master Boot Record):** Introducido en 1983, es un estándar antiguo que soporta discos de hasta un máximo de 2 TB y solo permite 4 particiones primarias. Funciona con sistemas BIOS Legacy y tiene la desventaja de ser un punto único de fallo al no tener redundancia.
- **GPT (GUID Partition Table):** Introducido en el año 2000, es el estándar moderno que requiere UEFI para arrancar. Soporta discos de tamaño prácticamente ilimitado (9.4 Zettabytes), permite hasta 128 particiones primarias, tiene copias de respaldo (redundancia) y detección de errores (CRC32). Además, es **obligatorio para instalar Windows 11**.

(Windows 11 requiere que el ordenador arranque en modo UEFI para garantizar funciones de seguridad avanzadas como el _Secure Boot_ (Arranque Seguro). El estándar UEFI está diseñado para trabajar de forma nativa con GPT).  
<br>

**Caso práctico de particionado (Disco de 1 TB para Win 11 y Ubuntu):**

- **EFI (512 MB, FAT32):** Necesaria para el arranque UEFI.
- **Windows 11 (250 GB, NTFS):** Para el sistema y juegos.
- **Datos Compartidos (350 GB, NTFS):** Accesible desde ambos sistemas para documentos y descargas.
- **Ubuntu / (80 GB, ext4):** Partición raíz para el sistema Linux y aplicaciones.
- **Ubuntu /home (315 GB, ext4):** Para configuraciones personales y archivos, lo que permite reinstalar Linux sin perder datos de usuario.
- **Swap (4 GB, linux-swap):** Partición de intercambio de Linux.  
  <br>

_(La memoria RAM es superrápida, pero su capacidad es limitada.  
Si el sistema operativo se queda sin RAM, el equipo podría bloquearse. Para evitar esto, Linux entra en acción y mueve los "bloques" de memoria (páginas) que llevan un rato sin usarse desde la RAM hacia la partición SWAP en el disco duro. Esto libera espacio en la RAM para los programas que estás utilizando activamente en ese momento._  
<br>

**Verificar si el sistema usa UEFI**

- **En Windows:** Presionar Win + R y Escribir: msinfo32
- **En Linus (Ubuntu):** \[ -d /sys/firmware/efi \] && echo "UEFI" || echo "BIOS Legacy"  
  <br>

## Arranque Dual y Múltiple (Dual Boot / Multi-boot)

El arranque dual permite tener dos o más sistemas operativos (por ejemplo, Windows y Ubuntu) instalados en el mismo ordenador, dándote a elegir cuál iniciar al encender el equipo.

El arranque múltiple (multi-boot) es el mismo concepto, pero con más de dos SO.

El principal requisito de hardware es tener suficiente espacio en disco. Otros requisitos son la planificación y el gestor de arranque GRUB.  
<br>

- **Gestor de arranque (GRUB2):** Es el primer programa que se ejecuta al encender el equipo y se encarga de cargar y transferir el control al _kernel_ del sistema operativo.

  Desde Fedora 16, GRUB2 ha sido el gestor de arranque predeterminado en sistemas x86 BIOS. Para las actualizaciones de los sistemas BIOS lo predeterminado es instalar también GRUB2, pero puede optarse por omitir por completo la configuración del gestor de arranque

- **Consejos clave de instalación:** Si vas a instalar Windows y Linux, **instala siempre Windows primero**. El instalador de Windows tiende a sobrescribir el gestor de arranque, mientras que GRUB (de Linux) detectará a Windows y lo añadirá al menú de inicio automáticamente. Además, es recomendable **desactivar el "Fast Startup" de Windows** para evitar problemas al acceder a las particiones desde Linux.

  Antes de intentar un arranque dual, haz una copia de seguridad completa de tu sistema.

- **Mitos desmentidos:** El arranque dual **no** ralentiza el ordenador, ya que mientras un sistema operativo está en uso, el otro está inactivo y no consume recursos.

  Tampoco es cierto que no se puedan compartir archivos: Linux puede leer y escribir sin problemas en particiones NTFS de Windows. Desde Windows, se pueden usar herramientas como ext2fsd para acceder a particiones EXT4 (Linux), aunque es menos común.

- **System76:** System76 es un fabricante de ordenadores estadounidense que vende portátiles y servidores con Linux preinstalado (su propia distribución, Pop!\_OS).

  System76 proporciona guías detalladas y soporte para configurar un arranque dual de Pop!\_OS y Windows, asegurando que el hardware (especialmente los gráficos híbridos de NVIDIA) funcione correctamente en ambos sistemas operativos.  
  <br>

## Ficheros de arranque en Linux

Un sistema de ficheros es un dispositivo que se formatea para guardar información. Linux soporta una gran cantidad de sistemas de ficheros.

En Linux, para poder usar un sistema de ficheros es imprescindible **montarlo** previamente en un "punto de montaje" (un directorio) usando el comando mount. (Se puede ver cuántos sistemas de ficheros hay montados y sus puntos de montaje con el comando mount).

Montar cualquier sistema de ficheros requiere tener privilegios de root y especificar cierta información como el tipo de sistema de ficheros, dispositivo donde se encuentra y punto de montaje.

Para desmontarlo se usa umount.  
<br>

- **Fichero /etc/fstab:** Especifica qué sistemas de ficheros se montan automáticamente durante el arranque del sistema.
- **Automontaje:** Herramientas como autofs permiten montar sistemas de ficheros (como USBs) automáticamente solo cuando se accede a ellos.
- **Reparación:** El comando fsck se utiliza para comprobar y reparar sistemas de ficheros dañados.  
  <br>

En el directorio personal de cada usuario existen unos ficheros de arranque que en ocasiones son útiles para ciertas tareas como definir un nuevo PATH o exportar algunas variables de entorno. los ficheros más importantes son:

- **bash_profile:** Se lanza en cada inicio de sesión que realiza el usuario.
- **bashrc**  
  <br>

## Sistemas RAID (Redundant Array of Independent Disks)

El sistema RAID agrupa varios discos físicos para conseguir redundancia de datos frente a fallos, o ambas cosas a la vez de manera que, cuando una unidad física de disco falle o se venga abajo, los datos que se encontraran en dicha unidad no se pierdan sino que se reconstruyan usando la paridad de los mismos.

Existen más de 15 tipos de RAID distintos o variaciones de ellos, aunque cada uno de ellos se puede incluso bifurcar en múltiples niveles RAID.  
<br>

- **RAID 0 (Striping):** Divide la información entre todos los discos para lograr alta velocidad y usar el 100% de la capacidad. **Desventaja:** No tiene tolerancia a fallos; si un disco se rompe, se pierde todo. (RAID 0 significa que no se implementa RAID).
- **RAID 1 (Espejo/Mirroring):** Duplica la misma información en dos discos (existe un disco primario, donde se leen y se escriben los datos, y un disco espejo, donde solamente se escriben las modificaciones y en el que se leerán datos cuando el primario falle. ). **Ventaja:** Alta seguridad frente a fallos. **Desventaja:** Pierdes el 50% de la capacidad total del almacenamiento. Coste económico.
- **RAID 5 (Paridad):** Reparte los datos y la "paridad" (códigos de recuperación) entre al menos 3 discos. Ofrece un gran equilibrio: es rápido en lectura y permite que **falle 1 disco** sin perder datos.
- **RAID 6:** Necesita un **mínimo de 4 discos.** Similar al RAID 5 pero con doble paridad, lo que permite que **fallen 2 discos** simultáneamente sin perder información.
- **RAID 10:** Es una combinación de RAID 1 y RAID 0 que requiere un número par de discos (mínimo 4). Ofrece un rendimiento muy alto y alta seguridad, pero con un coste elevado (solo aprovecha el 50% del espacio).
  <br>

_Más allá de que RAID 1 necesita un mínimo de 2 discos y RAID 5 un mínimo de 3, las diferencias reales entre ellos radican en_ **_cómo protegen la información, el espacio que desperdician y su rendimiento_**_._

**_El mecanismo de protección (Espejo vs. Paridad)_**

- **_RAID 1 (Espejo):_** _Funciona mediante la copia exacta y literal de los datos. Tienes un disco primario donde escribes, y un disco secundario (espejo) que es un clon idéntico. Si el primario falla, el sistema lee directamente del espejo._
- **_RAID 5 (Paridad):_** _No clona archivos enteros. En su lugar, divide los datos en fragmentos pequeños y calcula "códigos de error" matemáticos (llamados paridad). Esta paridad se distribuye estratégicamente entre todos los discos. Si un disco se rompe, el sistema coge los datos que quedan y la paridad para "adivinar" y reconstruir matemáticamente la información perdida._

**_Aprovechamiento del espacio (Capacidad útil)_**

- **_RAID 1:_** _Es muy ineficiente con el espacio, ya que siempre_ **_pierdes exactamente el 50%_** _de la capacidad total bruta._
- **_RAID 5:_** _Aprovecha mucho mejor el almacenamiento. En esta configuración, la paridad ocupa el espacio equivalente a_ **_un solo disco_**_, independientemente de cuántos discos tengas en total._

**_Rendimiento (Velocidad de escritura)_**

- **_RAID 1:_** _Ofrece una arquitectura más rápida en la tolerancia a fallos y escribir datos no supone un esfuerzo extra para el procesador del ordenador (simplemente guarda lo mismo dos veces)._
- **_RAID 5:_** _Es excelente para leer datos (muy rápido), pero_ **_penaliza las operaciones de escritura_** _(bajo rendimiento al escribir). Esto ocurre porque cada vez que guardas un archivo nuevo, el ordenador tiene que hacer cálculos matemáticos sobre la marcha para generar esos códigos de paridad antes de guardarlos._

**_Coste económico_**

- **_RAID 1:_** _Tiene como principal desventaja su alto coste, ya que pagas el doble por cada gigabyte que realmente puedes usar._
- **_RAID 5:_** _Se considera la opción ideal para servidores porque ofrece un gran_ **_equilibrio entre seguridad y velocidad_**_, maximizando la inversión en discos duros._
