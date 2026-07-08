# Módulo 2: Control de Versiones con Git 🌿

Git es la herramienta estándar de la industria para el seguimiento y control de cambios en el código. Permite a varios desarrolladores trabajar en el mismo proyecto sin sobrescribir el trabajo de los demás y mantiene un historial completo de cada cambio realizado.

---

## 2.1 ¿Qué es Git y Flujo de Trabajo Local

Piensa en Git como una máquina del tiempo local. En Git, los archivos pasan por tres áreas principales antes de guardarse de manera permanente:

1.  **Directorio de Trabajo (Working Directory):** La carpeta en tu computadora donde creas y editas tu código.
2.  **Área de Preparación (Staging Area):** Un espacio intermedio donde seleccionas qué archivos y cambios están listos para ser guardados.
3.  **Repositorio Local (Carpeta `.git`):** La base de datos donde Git almacena de forma permanente las capturas de estado (commits) de tu proyecto.

```
Directorio de Trabajo ---> Área de Preparación ---> Repositorio Local
     (Edición)                (git add)               (git commit)
```

---

## 2.2 Seguir Cambios

Para empezar a registrar los cambios de un proyecto, debes inicializar Git en él.

### 1. `git init`
Ejecuta esto una sola vez dentro de la carpeta raíz de tu proyecto para comenzar el seguimiento.
```bash
git init
```

### 2. `git status`
Muestra el estado actual del proyecto: qué archivos han cambiado, cuáles están listos en el Área de Preparación y cuáles aún no están bajo el control de Git.
```bash
git status
```

### 3. `git add`
Mueve los cambios desde el Directorio de Trabajo al Área de Preparación.
```bash
git add script.py      # Preparar un archivo específico
git add .              # Preparar todos los cambios del directorio actual
```

### 4. `git commit`
Guarda una captura de estado del Área de Preparación en el Repositorio Local. Cada commit requiere un mensaje descriptivo.
```bash
git commit -m "feat: Agregar sistema de inicio de sesión"
```

---

## 2.3 Historial e Inspección de Commits

Una vez que has hecho commits, puedes revisar la línea de tiempo de tu proyecto.

### 1. `git log`
Muestra la lista de commits realizados, su ID único (hash), el autor, la fecha y el mensaje descriptivo.
```bash
git log
# Presiona 'q' para salir de la vista del historial
```
*   `git log --oneline`: Una vista compacta que muestra una sola línea por cada commit.

### 2. `git show`
Muestra los cambios exactos (diferencias o "diff") introducidos en un commit específico.
```bash
git show <commit-hash>
```

---

## 2.4 Deshacer Errores

Git es muy tolerante. Si cometes un error, casi siempre puedes deshacerlo.

### 1. Descartar cambios sin preparar (`git restore`)
Si editaste un archivo pero quieres devolverlo a cómo se veía en el último commit:
```bash
git restore index.html
```

### 2. Quitar un archivo del Área de Preparación (`git restore --staged`)
Si ejecutaste por error `git add` y quieres sacar el archivo de la zona de preparación:
```bash
git restore --staged index.html
```

### 3. Ir a un commit del pasado (`git checkout`)
Cambia temporalmente tu directorio de trabajo para inspeccionar el estado del proyecto en un punto específico.
```bash
git checkout <commit-hash>
# Para regresar al presente (rama principal):
git checkout main
```

---

[⬅️ Volver al Índice Principal](../README.md)
