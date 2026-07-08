# Módulo 1: Linux y la Línea de Comandos 🐧

¡Bienvenido a la guía de Linux! En este módulo, cubriremos desde los conceptos más fundamentales del sistema operativo hasta el uso avanzado de la terminal (shell). Dominar esto te dará el control absoluto sobre tu computadora, servidores y flujos de desarrollo.

---

## 1.1 ¿Qué es Linux y el Kernel?

A menudo llamamos "Linux" a todo el sistema operativo, pero en términos estrictos, **Linux es solo el Kernel (el núcleo)**. 

Para entender la diferencia, usemos una analogía sencilla:
*   **El Hardware (Procesador, RAM, Disco):** Es el chasis y las ruedas de un automóvil.
*   **El Kernel (Linux):** Es el motor. Habla directamente con las piezas físicas, distribuye la energía (recursos) y hace que todo funcione.
*   **El Entorno de Escritorio y las Aplicaciones:** Son el volante, los asientos y el tablero con los que interactúa el conductor (tú).

Linux es de código abierto (open-source), extremadamente estable y seguro. Por esta razón, es el estándar indiscutible para servidores de internet, supercomputadoras, bases de datos y clusters de procesamiento de alto rendimiento.

### Las Distribuciones (Distros)
Como Linux es solo el "motor", diferentes comunidades y empresas construyen su propio "automóvil" a su alrededor, añadiendo instaladores, gestores de paquetes y entornos de escritorio. A este paquete completo se le llama **Distribución (Distro)**. 

En entornos de desarrollo e investigación, interactuarás principalmente con dos familias:
1.  **Familia Debian / Ubuntu / Linux Mint:** Son las distros más amigables y populares. Su entorno gráfico suele ser muy intuitivo y son excelentes para crear entornos de trabajo portátiles y persistentes.
2.  **Familia Red Hat / Fedora:** Sistemas modernos y robustos que integran las últimas tecnologías, muy utilizados en entornos corporativos y estaciones de trabajo avanzadas.

---

## 1.2 Opciones para usar Linux

No necesitas borrar tu sistema operativo actual (Windows o macOS) para aprender y usar Linux. Existen varias alternativas según tus necesidades:

1.  **Live USB (Pendrive en Vivo):** Ejecuta Linux directamente desde un pendrive sin alterar tu disco duro ni tus archivos. Es ideal para aprender y tener un sistema portátil que puedas usar en cualquier computadora.
2.  **WSL (Windows Subsystem for Linux):** Permite ejecutar una terminal de Linux directamente dentro de Windows de forma nativa, ideal para desarrolladores que necesitan herramientas de consola de Linux en Windows.
3.  **Máquinas Virtuales (VMs):** Usando programas como VirtualBox o VMware, puedes correr Linux como una ventana o aplicación dentro de tu sistema operativo actual.
4.  **Arranque Dual (Dual Boot):** Instala Linux en una partición del disco duro junto a Windows o macOS. Al encender la computadora, eliges cuál sistema iniciar.
5.  **Instalación Dedicada:** Reemplazar por completo tu sistema operativo anterior y usar Linux como el único sistema de la computadora.

---

## 1.3 Guía de Arranque desde USB (Booting)

Si vas a usar Linux desde un **Live USB**, debes indicarle a tu computadora que arranque desde el pendrive en lugar del disco duro interno.

### 1. Proceso de Arranque General en PC
1.  Apaga tu computadora por completo.
2.  Inserta el pendrive con Linux en un puerto USB.
3.  Enciende el equipo y, **de inmediato y repetidamente**, presiona la tecla del **Menú de Arranque (Boot Menu)** o de la BIOS de tu fabricante.
4.  Selecciona la unidad USB en la lista y presiona `Enter`.
5.  Elige la opción **"Start Linux Mint"** (o la distro correspondiente).

#### Teclas de Arranque Comunes según la Marca:
| Marca | Tecla del Menú de Arranque / BIOS |
| :--- | :--- |
| **HP** | `F9` o `Esc` |
| **Dell** | `F12` |
| **Lenovo** | `F12` o botón físico `Novo` (en laptops) |
| **Asus** | `Esc` o `F8` |
| **Acer** | `F12` o `F2` *(Nota: a veces debes activar la opción "F12 Boot Menu" en la BIOS primero)* |
| **Toshiba** | `F12` |
| **Apple (Intel)** | Mantener presionada la tecla `Option/Alt` (`⌥`) al encender |

---

### 2. Guía Específica para MacBook Air (Retina, 13", 2019 - Chip T2)
Los equipos Apple fabricados entre 2018 y 2020 que incorporan el **chip de seguridad Apple T2** bloquean por defecto el arranque desde discos externos para proteger el sistema. Para usar un Live USB en estos equipos, se debe hacer una configuración inicial única.

> [!NOTE]
> Este procedimiento no borra tus archivos ni modifica tu macOS. Solo le da permiso a la Mac para arrancar desde tu USB de Linux si tú lo decides expresamente al encender.

#### Parte 1: Autorizar el Arranque Externo (Solo la primera vez)
1.  Apaga tu MacBook Air por completo.
2.  Enciende el equipo y mantén presionadas las teclas **`Cmd (⌘) + R`** hasta que aparezca el logo de Apple o un globo terráqueo. Entrarás al modo de recuperación (**macOS Recovery**).
3.  Si te lo pide, selecciona tu usuario de macOS e introduce tu contraseña de administrador.
4.  En la barra de menú superior, haz clic en **Utilidades** > **Utilidad de Seguridad de Arranque** (Startup Security Utility).
5.  Autentícate de nuevo si es necesario.
6.  En **Arranque seguro (Secure Boot)**, selecciona **Sin seguridad** (No Security). (Esto garantiza la máxima compatibilidad con distros de Linux).
7.  En **Arranque externo (External Boot)**, selecciona **Permitir el arranque desde medios externos o extraíbles**.
8.  Cierra la utilidad y reinicia tu Mac desde el menú Apple.

#### Parte 2: Arrancar Linux Mint desde el Pendrive
1.  Apaga tu MacBook Air por completo.
2.  Conecta tu pendrive USB (usa un adaptador USB-A a USB-C si es necesario).
3.  Enciende el equipo y mantén presionada la tecla **`Option/Alt (⌥)`** de inmediato.
4.  Suéltala cuando veas la pantalla gris del **Gestor de Arranque (Startup Manager)**.
5.  Selecciona el disco de color amarillo/naranja llamado **"EFI Boot"** y presiona `Enter`.
6.  Aparecerá el menú de inicio de Linux Mint. Presiona `Enter` para cargar el escritorio Cinnamon.

> [!TIP]
> **¿No funciona el WiFi en tu MacBook con chip T2?**
> Algunas tarjetas de red Broadcom integradas en las Mac requieren controladores privativos que no vienen preinstalados. Si no ves redes WiFi:
> *   Conéctate a internet temporalmente usando un adaptador USB a Ethernet.
> *   Abre el **Gestor de Actualizaciones** o el **Centro de Controladores** de Linux Mint, donde el sistema detectará e instalará el controlador adecuado de forma automática.

#### Parte 3: Salir de Linux Mint y volver a macOS
1.  En Linux Mint, ve al Menú inferior izquierdo, haz clic en el botón de apagado y selecciona **Apagar** (Shut Down).
2.  Espera a que el equipo se apague del todo y **retira el pendrive**.
3.  Enciende tu Mac normalmente. Arrancará de forma automática en macOS, tal y como lo dejaste.

---

## 1.4 Entorno Gráfico vs Consola: El Escritorio Cinnamon y Nemo

Al iniciar Linux Mint, verás el entorno de escritorio **Cinnamon**. Su diseño es familiar e intuitivo si vienes de Windows:
*   **El Menú:** Ubicado en la esquina inferior izquierda. Permite acceder a los programas organizados por categorías.
*   **El Panel Inferior:** La barra de tareas que contiene las aplicaciones abiertas, el reloj y los controles del sistema (red, volumen, actualizaciones).
*   **Administrador de Archivos (Nemo):** El programa gráfico para navegar por tus carpetas, crear documentos, copiar, mover y borrar archivos de forma visual.

### El Sistema de Archivos en Linux
A diferencia de Windows, en Linux **no existen letras de unidad** como `C:` o `D:`. Todo el sistema está organizado bajo un único árbol jerárquico que comienza en la **Raíz**, representada por una barra diagonal (`/`).

Las carpetas más importantes para un usuario son:
*   **`/home/tu_usuario`:** Tu carpeta personal (Home). Aquí se guardan tus archivos, descargas, escritorio y configuraciones personales. Equivale al `C:\Users\tu_usuario` de Windows.
*   **`/media` o `/mnt`:** Directorios de montaje. Aquí es donde Linux monta automáticamente tus pendrives USB, discos duros externos y otras particiones del sistema.
*   **`/etc`:** Contiene los archivos de configuración de todo el sistema operativo y programas instalados (se modifican con permisos de administrador).
*   **`/usr`:** Contiene los programas instalados y sus recursos compartidos.

---

## 1.5 La Terminal y la Shell: ¿Qué es Bash?

Aunque el entorno gráfico es muy cómodo, el verdadero poder de Linux reside en su interfaz de texto.

*   **La Terminal (o Consola):** Es la ventana gráfica o aplicación que te permite interactuar con el sistema a través de texto (se abre en Linux Mint con `Ctrl + Alt + T`).
*   **La Shell (Intérprete de comandos):** Es el programa interno que lee los comandos que escribes en la terminal, los traduce y le dice al Kernel que ejecute la tarea solicitada.
*   **Bash (Bourne Again SHell):** Es el intérprete de comandos más popular y el estándar por defecto en la gran mayoría de las distribuciones Linux. Cuando aprendes comandos de consola en Linux, estás aprendiendo el lenguaje de Bash.

> [!NOTE]
> Otra shell común es **Zsh**, que se usa por defecto en los sistemas macOS modernos, pero comparte más del 95% de la sintaxis y comandos de Bash.

---

## 1.6 Permisos y Seguridad: El Poder de `sudo` y Root

Linux está diseñado desde sus cimientos para ser un sistema multiusuario y seguro. 

*   **Usuario Estándar:** Es tu usuario diario. Tiene permisos para modificar sus propios archivos en `/home/tu_usuario`, pero no puede alterar la configuración del sistema ni dañar archivos críticos.
*   **Superusuario (Root):** Es el administrador supremo del sistema. Tiene poder ilimitado para instalar programas, modificar la configuración y borrar cualquier archivo.
*   **`sudo` (SuperUser DO):** Es el comando que le dice a la terminal: *"Préstame los privilegios del superusuario (Root) por un momento para ejecutar esta acción específica"*.

> [!IMPORTANT]
> **La Contraseña en la Terminal:**
> Cuando ejecutes un comando usando `sudo`, la terminal te pedirá tu contraseña de usuario. Al escribirla, **no verás ningún carácter en la pantalla (ni asteriscos, ni puntos)**. Esto es un comportamiento de seguridad normal para evitar que alguien vea la longitud de tu contraseña. Escríbela con normalidad y presiona `Enter`.

---

## 1.7 Navegación Esencial

Para trabajar en la consola de comandos, debes saber moverte por el árbol de carpetas (directorio de trabajo).

### 1. `pwd` (Print Working Directory)
Muestra la ruta completa del directorio donde te encuentras ubicado en este instante.
```bash
pwd
# Ejemplo de salida: /home/usuario/CursoLinuxMint
```

### 2. `ls` (List)
Lista el contenido del directorio actual (archivos y carpetas).
*   `ls -l`: Muestra una lista detallada (permisos, tamaño, propietario y fecha de modificación).
*   `ls -a`: Muestra todos los archivos, incluyendo los ocultos (aquellos cuyos nombres comienzan con un punto, como `.git`).
*   `ls -lh`: Muestra el tamaño de los archivos en formato legible para humanos (KB, MB, GB).

### 3. `cd` (Change Directory)
Cambia de directorio para moverte entre carpetas.
```bash
cd Documentos      # Entra a la carpeta "Documentos"
cd ..              # Sube un nivel (va al directorio padre)
cd ~               # Te lleva directamente a tu carpeta personal (Home)
cd /               # Te lleva a la raíz del sistema
```

---

## 1.8 Operaciones con Archivos

Aprende a crear, copiar, mover y eliminar archivos y directorios desde la consola de comandos.

### 1. `mkdir` (Make Directory)
Crea una carpeta nueva.
```bash
mkdir Practicas
```

### 2. `touch`
Crea un archivo de texto vacío (o actualiza la fecha de modificación si ya existe).
```bash
touch practica1.txt
```

### 3. `cp` (Copy)
Copia un archivo o una carpeta de un lugar a otro.
*   **Copiar archivo:** `cp archivo.txt destino.txt`
*   **Copiar carpeta:** Para copiar directorios completos con su contenido, debes usar el parámetro recursivo `-r`.
    ```bash
    cp -r carpeta_origen/ carpeta_destino/
    ```

### 4. `mv` (Move / Rename)
Mueve archivos o carpetas, o les cambia el nombre si el destino está en el mismo directorio.
```bash
mv practica1.txt Documentos/practica1.txt   # Mueve el archivo
mv practica1.txt practica_final.txt         # Renombra el archivo
```

### 5. `rm` (Remove)
Elimina archivos o directorios permanentemente.

> [!WARNING]
> ¡La terminal no tiene Papelera de Reciclaje! Los archivos borrados con `rm` se eliminan para siempre de forma inmediata. Úsalo con extrema precaución.

*   **Eliminar un archivo:** `rm notas.txt`
*   **Eliminar una carpeta vacía:** `rmdir carpeta_vacia/`
*   **Eliminar una carpeta con contenido:** Requiere el parámetro recursivo y forzado `-rf`.
    ```bash
    rm -rf carpeta_con_archivos/
    ```

---

## 1.9 Editor de Texto Nano

Cuando trabajas en servidores remotos o en la consola sin interfaz gráfica, necesitas un editor de texto integrado en la terminal. **`nano`** es el editor ideal para principiantes porque es sencillo de usar y siempre muestra sus atajos en la parte inferior de la pantalla.

Para abrir o crear un archivo con nano:
```bash
nano notas_experimento.txt
```

### Atajos Clave en Nano (La tecla `^` representa `Ctrl`):
*   **Guardar cambios (`Ctrl + O`):** Presiona `Ctrl + O`, confirma el nombre del archivo con `Enter` y se guardarán los cambios.
*   **Salir del editor (`Ctrl + X`):** Sale de nano. Si tienes cambios sin guardar, te preguntará si deseas guardarlos (`S` o `Y` para sí, `N` para no).
*   **Buscar texto (`Ctrl + W`):** Abre la barra de búsqueda de texto dentro del archivo.

---

## 1.10 Gestión de Paquetes (Instalación de Software)

En Linux, no sueles descargar instaladores `.exe` de páginas de internet. En su lugar, el sistema utiliza **Gestores de Paquetes** que se conectan a repositorios seguros de internet para descargar e instalar programas de forma centralizada.

### 1. Gestión Visual (Gestor de Software)
En Linux Mint, puedes abrir el menú y buscar el **Gestor de Software** (Software Manager). Es una tienda de aplicaciones donde puedes buscar por nombre (como VLC, GIMP, VS Code) e instalarlos haciendo un solo clic e introduciendo tu contraseña.

### 2. Gestión por Consola
Dependiendo de la distribución que utilices, los comandos varían levemente:

#### Para entornos basados en Debian / Ubuntu / Linux Mint (usando `apt`)
*   **Actualizar la lista de programas disponibles en internet:**
    ```bash
    sudo apt update
    ```
*   **Instalar un nuevo paquete:**
    ```bash
    sudo apt install nombre_del_paquete
    ```
*   **Desinstalar/remover un paquete:**
    ```bash
    sudo apt remove nombre_del_paquete
    ```
*   **Actualizar todos los programas del sistema a su última versión:**
    ```bash
    sudo apt upgrade
    ```

#### Para entornos basados en Red Hat / Fedora (usando `dnf`)
*   **Instalar un nuevo paquete:**
    ```bash
    sudo dnf install nombre_del_paquete
    ```
*   **Remover un paquete:**
    ```bash
    sudo dnf remove nombre_del_paquete
    ```

---

## 1.11 Mantenimiento y Respaldos: Actualizaciones y Timeshift

Un sistema estable requiere de mantenimiento preventivo sencillo pero efectivo.

### 1. Gestor de Actualizaciones (Update Manager)
Linux Mint tiene un pequeño icono de escudo en la barra de tareas. Revísalo regularmente para aplicar las actualizaciones de seguridad y correcciones de errores (niveles 1 a 3 son las más comunes y recomendadas).

### 2. Copias de Respaldo con Timeshift
Timeshift es una aplicación integrada en Linux Mint que permite tomar **instantáneas (snapshots)** del estado del sistema operativo. Si una actualización o configuración daña tu sistema, puedes abrir Timeshift y revertirlo al instante anterior para que vuelva a funcionar de inmediato.

*   **Configuración básica:** Abre Timeshift desde el menú, selecciona **RSYNC** como el tipo de copia y selecciona un disco o partición destino (preferiblemente una unidad externa).
*   **Crear Snapshot:** Haz clic en **Crear** para guardar el estado actual del sistema antes de hacer modificaciones críticas.

---

## 1.12 Apagado Seguro y Trucos Avanzados

A medida que te sientas más cómodo en la consola, puedes usar trucos para automatizar y agilizar tareas.

### Comodines (`*`)
El símbolo asterisco (`*`) actúa como un comodín que representa cualquier texto.
```bash
rm *.log           # Elimina TODOS los archivos que terminan en .log
ls datos*          # Muestra todos los archivos que empiezan con la palabra "datos"
```

### Redirecciones (`>` y `>>`)
Permiten enviar la salida de texto de un comando directamente a un archivo en lugar de mostrarla en la pantalla de la terminal.
*   `>`: Sobrescribe el archivo con el nuevo texto (si el archivo no existe, lo crea).
*   `>>`: Añade el texto al final del archivo existente, sin borrar lo anterior.
```bash
echo "Inicio del experimento" > logs.txt
echo "Paso 1 completado con éxito" >> logs.txt
```

### Apagar Correctamente desde Pendrive
Si estás utilizando un **Live USB** y quieres apagar la computadora asegurándote de que no se corrompa el sistema de archivos del pendrive y se escriban todos los datos pendientes en la memoria, ejecuta en la terminal:
```bash
sudo sync && sudo poweroff -f
```
*   `sync`: Fuerza al sistema a escribir en el pendrive toda la información que esté en la memoria caché.
*   `poweroff -f`: Apaga la computadora inmediatamente.

---

[⬅️ Volver al Índice Principal](../README.md)
