# Módulo 1: Linux y la Línea de Comandos 🐧

¡Bienvenido a la línea de comandos! En este módulo, cubriremos los aspectos fundamentales del uso de Linux a través de la terminal (shell). Domina esto y podrás navegar y gestionar tu computadora como un profesional.

---

## 1.1 ¿Por qué Linux? y Entendiendo las Shells

Linux es un sistema operativo potente y de código abierto que hace funcionar la gran mayoría de los servidores de internet, bases de datos y herramientas de desarrollo.

*   **La Terminal (o Consola):** Un programa de texto que te permite escribir comandos.
*   **La Shell (ej. Bash o Zsh):** El intérprete de comandos que lee el texto que escribes y le da instrucciones al sistema operativo para realizar tareas.

Al escribir comandos en texto, obtienes acceso a automatizaciones y a un control directo sobre la computadora que las interfaces gráficas (GUIs) no pueden ofrecer.

---

## 1.2 Navegación Esencial

Para interactuar con el sistema, debes saber cómo moverte entre carpetas (llamadas **directorios**).

### 1. `pwd` (Print Working Directory)
Muestra la ruta del directorio en el que te encuentras actualmente en el sistema de archivos.
```bash
pwd
# Ejemplo de Salida: /home/usuario/proyectos
```

### 2. `ls` (List)
Muestra una lista de archivos y carpetas dentro del directorio actual.
*   `ls -l`: Lista detallada (permisos, tamaño, propietario, fecha).
*   `ls -a`: Lista todos los archivos, incluidos los ocultos (aquellos que empiezan con un punto, ej. `.git`).

### 3. `cd` (Change Directory)
Te mueve a otra carpeta.
```bash
cd Documentos      # Entrar a la carpeta Documentos
cd ..              # Subir un nivel (directorio padre)
cd ~               # Ir al directorio personal (Home)
```

---

## 1.3 Operaciones con Archivos

Ahora que sabes navegar, aprendamos a manipular archivos y carpetas.

### 1. `mkdir` (Make Directory)
Crea una carpeta nueva.
```bash
mkdir nueva-carpeta
```

### 2. `touch`
Crea un archivo vacío.
```bash
touch hola.txt
```

### 3. `cp` (Copy)
Copia archivos o directorios.
*   *Para archivos:* `cp origen.txt destino.txt`
*   *Para directorios (recursivo):* `cp -r carpeta_a carpeta_b`

### 4. `mv` (Move / Rename)
Mueve o renombra archivos/carpetas.
```bash
mv hola.txt documentos/hola.txt   # Mover archivo
mv nombre_viejo.txt nuevo.txt     # Renombrar archivo
```

### 5. `rm` (Remove)
Elimina archivos o carpetas.
> ⚠️ **Advertencia:** ¡La terminal no tiene Papelera de Reciclaje! Los archivos borrados se eliminan permanentemente.
*   *Para archivos:* `rm archivo.txt`
*   *Para carpetas (recursivo y forzado):* `rm -rf nombre_carpeta`

---

## 1.4 Trucos Avanzados: Comodines y Redirecciones

A medida que te sientas más cómodo, puedes empezar a combinar comandos y usar atajos.

### Comodines (`*`)
Coincide con cualquier conjunto de caracteres.
```bash
rm *.log           # Elimina todos los archivos que terminan en .log
ls proyecto*       # Lista archivos que comienzan con "proyecto"
```

### Redirecciones (`>` y `>>`)
Redirecciona la salida de un comando a un archivo en lugar de mostrarla en la terminal.
*   `>` sobrescribe el archivo.
*   `>>` añade al final del archivo.
```bash
echo "Hola Mundo" > saludo.txt
echo "Añadiendo una segunda línea" >> saludo.txt
```

---

[⬅️ Volver al Índice Principal](../README.md)
