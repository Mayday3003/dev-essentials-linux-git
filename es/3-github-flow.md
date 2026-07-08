# Módulo 3: Desarrollo Colaborativo con GitHub 🤝

GitHub es una plataforma en la nube que aloja repositorios de Git. Funciona como un punto de encuentro centralizado donde los desarrolladores guardan su código y colaboran de forma organizada.

---

## 3.1 Trabajar con Repositorios Remotos

Un **repositorio remoto** es una versión de tu proyecto alojada en un servidor (como GitHub).

### 1. `git clone`
Descarga un repositorio existente desde GitHub a tu computadora local.
```bash
git clone https://github.com/usuario/repositorio.git
```

### 2. `git remote add`
Enlaza tu repositorio local a un repositorio remoto en GitHub (usualmente llamado `origin`).
```bash
git remote add origin https://github.com/usuario/repositorio.git
```

### 3. `git push`
Sube tus commits locales a GitHub.
```bash
git push origin main
```

### 4. `git pull`
Descarga los últimos cambios desde GitHub y los fusiona directamente en tu rama local actual.
```bash
git pull origin main
```

---

## 3.2 Ramas y Fusión

Las ramas (branches) te permiten desarrollar nuevas funciones o corregir errores en un entorno aislado sin alterar la base de código estable principal (`main`).

```
       (Rama de función)      [*] ---> [*]
                             /            \
Rama `main`: -------------[*]------------[*] (Fusionada)
```

### 1. `git branch`
Muestra una lista de todas las ramas locales de tu proyecto.
```bash
git branch
```

### 2. Crear una rama
Crea una nueva rama con un nombre descriptivo para tu función o arreglo.
```bash
git branch feature-login
```

### 3. Cambiar de rama (`git checkout` o `git switch`)
Te cambia a la rama que especifiques.
```bash
git checkout feature-login
# O también:
git switch feature-login
```
*   *Atajo (Crear y Cambiar):* `git checkout -b feature-login`

### 4. `git merge`
Combina los cambios de otra rama en tu rama activa actual.
Para fusionar `feature-login` dentro de `main`:
```bash
git checkout main
git merge feature-login
```

---

## 3.3 Resolución de Conflictos

Un conflicto de fusión (merge conflict) ocurre cuando Git no puede fusionar cambios automáticamente (por ejemplo, si dos personas editan la misma línea exacta de un archivo de manera diferente).

Cuando hay un conflicto, Git detiene el proceso y marca los puntos de conflicto en el archivo afectado:
```
<<<<<<< HEAD
Nuestros cambios aquí en la rama main
=======
Los cambios de la otra persona en la rama feature-login
>>>>>>> feature-login
```

### Cómo resolverlo:
1.  Abre el archivo en un editor de texto.
2.  Decide qué versión de los cambios quieres conservar y borra los marcadores de Git (`<<<<<<<`, `=======`, `>>>>>>>`).
3.  Guarda el archivo.
4.  Prepara el archivo resuelto en staging: `git add <archivo>`
5.  Finaliza la fusión haciendo un commit: `git commit -m "merge: Resolver conflictos"`

---

## 3.4 El Flujo de Trabajo en GitHub (GitHub Flow)

El flujo de trabajo estándar para colaborar y contribuir código en proyectos profesionales es el siguiente:

1.  **Fork:** Crea una copia del repositorio de otra persona en tu propia cuenta de GitHub.
2.  **Clonar:** Descarga tu repositorio copiado (fork) a tu máquina local.
3.  **Crear Rama:** Trabaja siempre en una rama nueva para tu propuesta.
4.  **Confirmar y Subir (Commit & Push):** Realiza tus cambios, haz commits y súbelos a tu fork en GitHub.
5.  **Pull Request (PR):** Abre una solicitud de extracción en GitHub para proponer integrar tus cambios en la rama `main` del repositorio original.
6.  **Revisión de Código:** Se discuten los cambios sugeridos, se hacen correcciones si es necesario y se aprueba la propuesta.
7.  **Fusión (Merge):** Los mantenedores del repositorio original fusionan tu Pull Request.

---

[⬅️ Volver al Índice Principal](../README.md)
