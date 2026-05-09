# UNIDAD 3 - Instalación y configuración de SSOO

## 1\. Requisitos y Compatibilidad (Hardware y Software)

Para que un sistema o programa funcione correctamente, el equipo debe cumplir con ciertas características:  
<br>

- **Requisitos de Hardware:** Son las características físicas que necesita un equipo para que un programa o sistema funcione correctamente.

  Incluyen componentes físicos como:
  - **CPU** -> determina la velocidad y compatibilidad, Algunos programas requieren un número mínimo de núcleos o cierta arquitectura (x86, x64, ARM).
  - **memoria RAM** -> afecta el rendimiento al cargar programas.
  - **GPU** (tarjeta gráfica) -> Puede ser integrada o dedicada.
  - **Espacio de almacenamiento** en HDD o SSD.
  - **Periféricos** **y** **componentes adicionales**:
    - **Tarjeta de sonido**
    - **Tarjeta de red**
    - Cámara/micrófono
    - Sensores (en móviles)

**Compatibilidad eléctrica y física**: En equipos ensamblados, también importa la compatibilidad entre placa madre, RAM, CPU, fuente, etc.  
<br>

- **Requisitos de Software:** Son los componentes lógicos necesarios, como la **versión y arquitectura del sistema operativo (32 o 64 bits), librerías (ej. Java, .NET) y los controladores o _drivers_ actualizados.**

  Software complementario: Navegadores compatibles. Bases de datos (MySQL, PostgreSQL) Servidores web (Apache, Nginx)

- **Niveles de requisitos:** Se dividen en **mínimos** (funcionamiento básico con limitaciones), **recomendados** (experiencia fluida y estable) y **óptimos** (para usuarios que exigen el máximo rendimiento).  
  <br>

- **Compatibilidad:**
  - **Funcional**: El equipo físico (procesador, RAM y tarjeta gráfica) tiene la capacidad y las instrucciones necesarias para ejecutar el programa sin fallos.
  - **Del sistema operativo**: El software debe estar diseñado específicamente para el sistema en el que se va a instalar (como Windows, Android o iOS) y ser compatible con su versión.
  - **De controladores (drivers):** Los componentes físicos necesitan drivers compatibles con el sistema operativo actual para que puedan funcionar correctamente.
  - **De arquitectura**: El código del programa debe coincidir con la estructura del procesador del equipo (por ejemplo, aplicaciones de 64 bits para sistemas x64, o programas ARM exclusivos para hardware ARM).  
    <br>

## 2\. Preparación del Hardware: Memoria BIOS/UEFI y Configuración de Arranque

Antes de instalar el sistema operativo en un ordenador ensamblado (sin software precargado), interactúa la memoria BIOS (o su versión moderna, UEFI).

- **Configurar la memoria BIOS/UEFI::** La BIOS/UEFI identifica y memoriza los componentes instalados en la placa base (como CPU, RAM, discos duros y puertos) y evita hackeos del arranque. Además, también almacena números de serie y claves de licencia de software de forma que si tenemos que reinstalar el SO no es necesario introducirlo de nuevo.

- **BOOT DEVICE:** Para instalar un sistema operativo, se debe acceder a esta memoria durante el encendido (usualmente pulsando teclas como SUPR; Alt + F2; F8; F9 o F10) y configurar el orden de arranque (Boot Priority) cambiando el primer dispositivo de lectura al USB o DVD donde se encuentra el instalador del sistema operativo.

  Durante la instalación del sistema operativo, deberemos de seleccionar desde el menú Boot: dónde se instala el Sistema Operativo, Configurar Fecha y hora de nuestra placa base, Habilitación del uso de puertos USB, Habilitar la virtualización.

  Con esta configuración de la secuencia de arranque, ya podríamos salir del menú de la BIOS y guardar la configuración (SAVE & EXIT), pulsando F10 o la tecla elegida por el desarrollador de la BIOS/UEFI:

  Posteriormente, podemos dejar este orden de arranque del ordenador (boot menu) si no tarda mucho tiempo en arrancar la placa base. En caso contrario, cambiaríamos el orden y colocaríamos en primera lugar (1st boot device) el HDD.  
  <br>

## 3\. Instalación de Windows 11

- **Actualizar entre ediciones (Windows 11 Home -> Pro):**
  - Asegúrate de que Windows 11 esté actualizado.
  - Ve a Inicio > Configuración > Activación.
  - Si está disponible “Actualizar la edición de Windows”, selecciona Cambiar.
  - Introduce la nueva clave de producto y sigue las instrucciones.

- **Instalar Windows en un dispositivo sin sistema operativo:**
  - Crear medios de instalación (por ejemplo, unidad USB) para Windows 11.
  - Conecta el medio al dispositivo y arráncalo desde ahí.
  - Cuando se te pida, escribe la clave de producto. El programa de instalación seleccionará la edición correcta según la clave.

- **Actualizar a Windows 11 desde una versión anterior:**
  - Asegúrate de que la versión de Windows existente esté completamente actualizada
  - Crea el medio de instalación de Windows 11 (USB) y conéctalo al equipo. Ejecútalo (setup.exe) desde el medio de instalación. Cuando el asistente lo pida, introduce la clave de producto y sigue.  
    <br>

- **Medios de instalación:**
  - Ir a la página Windows 11 -> Descárgalo.
  - En “Crear medios de instalación de Windows 11”, seleccionar Descargar ahora.
  - Se descarga MediaCreationTool.exe O https://rufus.ie/es/ RUFUS.
  - Ejecutar la herramienta -> La herramienta guía todo el proceso.
  - Los medios de instalación permiten:
    - Instalar una nueva copia de Windows
    - Realizar una instalación limpia
    - Reinstalar Windows
  - Opciones de creación:
    - Unidad flash USB
    - Archivo ISO para máquinas virtuales o DVD
  - Requisitos del medio: - Conexión a internet estable - Unidad flash USB vacía con al menos 8 GB de capacidad (cuyo contenido previo será eliminado).  
    <br>

## 4\. Automatización de Instalación (PXE y Cloud-init)

Para entornos profesionales, existen métodos de instalación desatendida y a través de red:

- **PXE (Preboot Execution Environment):** Permite arrancar un equipo a través de la red sin necesidad de un USB o disco local . Funciona obteniendo una IP y descargando un archivo de arranque mediante un servidor DHCP y TFTP .

- **Cloud-init:** Es una herramienta para automatizar configuraciones en el primer arranque del sistema, permitiendo montar unidades, configurar servicios, crear usuarios, configurar claves SSH, ajustes de red, instalar paquetes, sin intervención humana.

  (Es muy común en máquinas en la nube (AWS, OpenStack, Azure), pero funciona perfectamente en servidores físicos).

- **Uso combinado:** El sistema arranca por PXE cargando un instalador automático, el cual descarga los datos de usuario de Cloud-init para finalizar la configuración en el primer reinicio .  
  <br>

## 5\. Particiones y Sistemas de Archivos

- **Particiones:** Son divisiones lógicas dentro de un disco físico que funcionan como discos independientes . Sirven para separar los archivos del sistema de los datos personales, instalar múltiples sistemas operativos u organizar copias de seguridad . En Windows 11, esto se gestiona mediante la herramienta "Administración de discos".

  **Administración de discos - Cómo crear una partición**
  - Reducir volumen -> Clic derecho sobre la partición existente (ej. C:) Elegir 'Reducir volumen' -> Indicar tamaño a liberar en MB -> Aparece espacio «No asignado».
  - Nuevo volumen -> Clic derecho en espacio «No asignado» -> Seleccionar 'Nuevo volumen simple' -> Asignar tamaño, letra de unidad y formateo (Recomendado: NTFS).
  - Eliminar particiones -> convierte el espacio en 'No asignado’.  
    <br>

- **Sistemas de Archivos:** Varían según el entorno principal:  
  <br>

- **Windows 11:** - **NTFS** de forma predeterminada para el sistema.

          Permite permisos avanzados, compresión, cifrado, journaling y archivos grandes.

      - **exFAT y FAT32** para memorias externas.

          Compatible con Windows, macOS y Linux (con drivers).

          No tiene journaling → mayor riesgo de corrupción si se corta la energía.

      - **ReFS** para entornos profesionales y de desarrollo.

          Orientado a servidores y desarrolladores.

          Resiliente frente a corrupción de datos.

  <br>

- **Linux (Ubuntu):** - **ext4** como estándar por su estabilidad.

      Journaling, grandes tamaños de archivo, muy fiable.

      - **Btrfs**

      Incluye snapshots, compresión y verificación de integridad.

      Ideal para usuarios avanzados.

      - **XFS** para servidores.

      Muy rápido con archivos grandes.

      Menos flexible al cambiar tamaño de particiones.

      - **FAT32 / exFAT / NTFS** (compatibilidad)

      Linux puede leer y escribir NTFS y exFAT mediante controladores.

  <br>

- **macOS:**
  - **APFS** de forma predeterminada desde macOS High Sierra

    Optimizado para SSD y NVMe.

    Soporte para snapshots, clonación, cifrado completo, espacio compartido.

  - **HFS+** en sistemas clásicos.

    Aún usado en algunos discos externos o sistemas antiguos.

  - **exFAT / FAT32**

        Se usa en discos externos para compatibilidad con Windows y Linux.

    <br>

- **Compartir archivos:** Para compatibilidad cruzada de discos externos entre Windows, macOS y Linux, se recomienda utilizar el formato **exFAT**.  
  <br>

| **Sistema operativo** | **NTFS**         | **exFAT** | **FAT32** | **ext4** | **APFS**                       |
| :-------------------- | :--------------- | :-------- | :-------- | :------- | :----------------------------- |
| **Windows 11**        | ✔ nativo         | ✔ nativo  | ✔         | ❌       | ❌                             |
| **Linux (Ubuntu)**    | ✔ con driver     | ✔         | ✔         | ✔ nativo | ❌ (solo lectura experimental) |
| **macOS**             | lectura limitada | ✔ nativo  | ✔         | ❌       | ✔ nativo                       |

<br>

**El soporte para Windows 10 finalizó en octubre de 2025; se recomienda pasar a Windows 11.**
