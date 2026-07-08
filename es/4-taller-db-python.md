# Taller Práctico: Bases de Datos con Python y GitHub 
> **Duración estimada:** 3 a 4 horas | **Nivel:** Principiante-Intermedio
> **Requisitos previos:** Haber completado el Módulo 1 (Linux Terminal) y el Módulo 2 (Git Essentials).

En este taller aprenderás a instalar y configurar dos de los gestores de bases de datos más utilizados en el mundo profesional, a conectarlos con Python y a versionar tu trabajo de forma segura en GitHub.

---

##  Objetivos del Taller

Al finalizar este taller serás capaz de:
- Instalar y configurar **PostgreSQL** (base de datos relacional) y **MongoDB** (base de datos NoSQL).
- Conectarte a ambas bases de datos desde un script de **Python**.
- Guardar credenciales de forma segura usando archivos `.env`.
- Versionar tu proyecto con **Git** sin exponer información sensible.
- Colaborar y entregar tu trabajo en **GitHub** como se hace en la industria.

---

## Parte 1: Instalación de PostgreSQL 

PostgreSQL es un sistema de gestión de bases de datos relacional (SQL) de código abierto, extremadamente robusto y usado ampliamente en la industria y en ciencia de datos.

### 1.1 Instalación

Abre la terminal y ejecuta los siguientes comandos uno por uno:

```bash
# 1. Actualizar la lista de paquetes disponibles
sudo apt update

# 2. Instalar PostgreSQL y sus utilidades cliente
sudo apt install -y postgresql postgresql-contrib
```

Verifica que el servicio está activo:

```bash
sudo systemctl status postgresql
```

Deberías ver una línea que dice `Active: active (running)`. Presiona `q` para salir.

### 1.2 Acceder a PostgreSQL

PostgreSQL crea automáticamente un usuario de sistema llamado `postgres`. Para acceder al intérprete interactivo:

```bash
sudo -u postgres psql
```

Ahora estás dentro de la consola de PostgreSQL. El prompt cambia a `postgres=#`.

### 1.3 Crear tu Usuario y Base de Datos

Ejecuta estos comandos **dentro de la consola de PostgreSQL** (`postgres=#`):

```sql
-- Crear un nuevo usuario (reemplaza 'tu_usuario' y 'tu_contraseña' con los tuyos)
CREATE USER tu_usuario WITH PASSWORD 'tu_contraseña';

-- Crear una base de datos para el taller
CREATE DATABASE taller_db;

-- Dar todos los permisos sobre la base de datos a tu usuario
GRANT ALL PRIVILEGES ON DATABASE taller_db TO tu_usuario;

-- Salir de la consola
\q
```

> [!NOTE]
> Guarda tu usuario y contraseña en un lugar seguro. Los usarás más adelante en el archivo `.env`.

### 1.4 Comandos Útiles de PostgreSQL

| Comando | Descripción |
|---|---|
| `\l` | Listar todas las bases de datos |
| `\c nombre_db` | Conectarse a una base de datos |
| `\dt` | Listar todas las tablas de la base de datos actual |
| `\du` | Listar todos los usuarios |
| `\q` | Salir de la consola |

---

## Parte 2: Instalación de MongoDB 

MongoDB es una base de datos **NoSQL orientada a documentos**. Almacena la información en documentos tipo JSON (llamados BSON internamente), lo que lo hace muy flexible para datos no estructurados o con esquemas cambiantes.

### 2.1 Instalación

MongoDB no está en los repositorios oficiales de Ubuntu/Mint, por lo que debemos añadir el repositorio oficial:

```bash
# 1. Instalar dependencias necesarias
sudo apt install -y gnupg curl

# 2. Importar la clave GPG oficial de MongoDB
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor

# 3. Añadir el repositorio oficial de MongoDB (para Ubuntu 22.04 / Mint 21)
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | \
   sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# 4. Actualizar la lista de paquetes e instalar MongoDB
sudo apt update
sudo apt install -y mongodb-org
```

### 2.2 Iniciar el Servicio

```bash
# Iniciar MongoDB
sudo systemctl start mongod

# Habilitar el inicio automático al encender el equipo
sudo systemctl enable mongod

# Verificar que está activo
sudo systemctl status mongod
```

### 2.3 Acceder a MongoDB

Accede al intérprete interactivo de MongoDB:

```bash
mongosh
```

El prompt cambia a `test>`. Prueba con un comando básico:

```javascript
// Ver todas las bases de datos
show dbs

// Salir
exit
```

---

## Parte 3: Configurar el Entorno de Python 

Nunca instales paquetes de Python directamente en el sistema. Usa siempre un **entorno virtual** para aislar las dependencias de cada proyecto.

### 3.1 Crear la Estructura del Proyecto

```bash
# Navega a tu carpeta de proyectos o crea una nueva
mkdir ~/taller-db && cd ~/taller-db

# Crear el entorno virtual
python3 -m venv .venv

# Activar el entorno virtual
source .venv/bin/activate
```

Tu prompt de terminal ahora mostrará `(.venv)` al inicio, indicando que el entorno está activo.

### 3.2 Instalar las Dependencias

```bash
pip install psycopg2-binary pymongo python-dotenv
```

| Librería | Para qué sirve |
|---|---|
| `psycopg2-binary` | Conectar Python con PostgreSQL |
| `pymongo` | Conectar Python con MongoDB |
| `python-dotenv` | Leer variables de entorno desde un archivo `.env` |

Guarda las dependencias en un archivo `requirements.txt`:

```bash
pip freeze > requirements.txt
```

### 3.3 Crear el Archivo `.env` con las Credenciales

El archivo `.env` guarda tus contraseñas y datos sensibles **fuera del código**. Nunca debe subirse a GitHub.

```bash
nano .env
```

Escribe lo siguiente (reemplaza con tus datos reales):

```
# Credenciales de PostgreSQL
PG_HOST=localhost
PG_PORT=5432
PG_DATABASE=taller_db
PG_USER=tu_usuario
PG_PASSWORD=tu_contraseña

# Credenciales de MongoDB
MONGO_URI=mongodb://localhost:27017
MONGO_DATABASE=taller_mongo_db
```

Guarda con `Ctrl + O`, `Enter`, y cierra con `Ctrl + X`.

---

## Parte 4: Scripts de Conexión con Python 

### 4.1 Conexión y Operaciones con PostgreSQL

Crea el archivo `postgres_demo.py`:

```bash
nano postgres_demo.py
```

```python
import psycopg2
from dotenv import load_dotenv
import os

# Cargar las variables del archivo .env
load_dotenv()

# Establecer la conexión usando las variables de entorno
conn = psycopg2.connect(
    host=os.getenv("PG_HOST"),
    port=os.getenv("PG_PORT"),
    dbname=os.getenv("PG_DATABASE"),
    user=os.getenv("PG_USER"),
    password=os.getenv("PG_PASSWORD")
)

cursor = conn.cursor()
print(" Conexión a PostgreSQL establecida.")

# --- CREAR TABLA ---
cursor.execute("""
    CREATE TABLE IF NOT EXISTS estudiantes (
        id SERIAL PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        carrera VARCHAR(100),
        nota FLOAT
    );
""")
conn.commit()
print("Tabla 'estudiantes' verificada/creada.")

# --- INSERTAR DATOS ---
estudiantes = [
    ("Ana García", "Biología", 4.5),
    ("Carlos Ruiz", "Ingeniería", 3.8),
    ("Sofía Martínez", "Química", 4.9),
]
cursor.executemany(
    "INSERT INTO estudiantes (nombre, carrera, nota) VALUES (%s, %s, %s);",
    estudiantes
)
conn.commit()
print(f" {cursor.rowcount} estudiantes insertados.")

# --- CONSULTAR DATOS ---
cursor.execute("SELECT * FROM estudiantes ORDER BY nota DESC;")
filas = cursor.fetchall()

print("\ Estudiantes por nota (de mayor a menor):")
print(f"{'ID':<5} {'Nombre':<20} {'Carrera':<20} {'Nota':<5}")
print("-" * 55)
for fila in filas:
    print(f"{fila[0]:<5} {fila[1]:<20} {fila[2]:<20} {fila[3]:<5}")

# --- CERRAR CONEXIÓN ---
cursor.close()
conn.close()
print("\ Conexión cerrada.")
```

Ejecuta el script:

```bash
python3 postgres_demo.py
```

### 4.2 Conexión y Operaciones con MongoDB

Crea el archivo `mongo_demo.py`:

```bash
nano mongo_demo.py
```

```python
from pymongo import MongoClient
from dotenv import load_dotenv
import os
from datetime import datetime

# Cargar las variables del archivo .env
load_dotenv()

# Establecer la conexión
client = MongoClient(os.getenv("MONGO_URI"))
db = client[os.getenv("MONGO_DATABASE")]
print("Conexión a MongoDB establecida.")

# Seleccionar (o crear) la colección
coleccion = db["experimentos"]

# --- INSERTAR DOCUMENTOS ---
experimentos = [
    {
        "titulo": "Síntesis de Aspirina",
        "investigador": "Ana García",
        "fecha": datetime(2025, 3, 15),
        "resultados": {"rendimiento_pct": 87.5, "pureza_pct": 99.1},
        "estado": "completado"
    },
    {
        "titulo": "Extracción de ADN de Banano",
        "investigador": "Carlos Ruiz",
        "fecha": datetime(2025, 4, 2),
        "resultados": {"rendimiento_pct": 72.3},
        "estado": "en análisis"
    },
]

resultado = coleccion.insert_many(experimentos)
print(f"➕ Documentos insertados con IDs: {resultado.inserted_ids}")

# --- CONSULTAR DOCUMENTOS ---
print("\ Todos los experimentos:")
for doc in coleccion.find():
    print(f"  - {doc['titulo']} | Investigador: {doc['investigador']} | Estado: {doc['estado']}")

# --- FILTRAR DOCUMENTOS ---
print("\n Experimentos completados:")
completados = coleccion.find({"estado": "completado"})
for doc in completados:
    print(f"  - {doc['titulo']} | Rendimiento: {doc['resultados'].get('rendimiento_pct')}%")

# --- CERRAR CONEXIÓN ---
client.close()
print("\n Conexión cerrada.")
```

Ejecuta el script:

```bash
python3 mongo_demo.py
```

---
n🔍
## Parte 5: Integración con Git y GitHub 

### 5.1 Crear el Archivo `.gitignore`

Este archivo le dice a Git qué archivos **no debe rastrear ni subir**. Es el paso de seguridad más importante.

```bash
nano .gitignore
```

```
# Entorno virtual de Python (no se versiona, se recrea con pip install)
.venv/
__pycache__/
*.pyc

# Archivo de credenciales (¡NUNCA subir esto a GitHub!)
.env

# Archivos de sistema
.DS_Store
```

Guarda y cierra (`Ctrl + O`, `Enter`, `Ctrl + X`).

> [!CAUTION]
> Si subes el archivo `.env` a GitHub por accidente con contraseñas reales, debes cambiar esas contraseñas **inmediatamente**. Git guarda el historial y cualquiera puede verlo.

### 5.2 Inicializar el Repositorio Git

```bash
# Inicializar el repositorio
git init

# Ver el estado actual (verás los archivos sin rastrear)
git status
```

### 5.3 Hacer tu Primer Commit

```bash
# Añadir todos los archivos relevantes al área de preparación
git add .

# Verificar que .env NO aparece en el listado (git status)
git status

# Crear el primer commit
git commit -m "feat: add database connection scripts and project setup"
```

### 5.4 Conectar con GitHub y Subir el Proyecto

1. Ve a [github.com](https://github.com) y crea un repositorio nuevo llamado `taller-db-python` (vacío, sin README).
2. Copia la URL del repositorio (ejemplo: `https://github.com/tu_usuario/taller-db-python.git`).
3. Ejecuta en la terminal:

```bash
# Vincular el repositorio local con el remoto en GitHub
git remote add origin https://github.com/tu_usuario/taller-db-python.git

# Subir los cambios a la rama principal
git push -u origin main
```

---

## Ejercicios Prácticos

### Ejercicio 1: Linux — Explorar el Entorno
1. Usa `ls -la ~/taller-db/` para listar todos los archivos del proyecto, incluyendo los ocultos. ¿Ves el archivo `.env` y `.venv`? ¿Por qué son importantes para el proyecto?
2. Usa el comando `cat requirements.txt` para ver las dependencias del proyecto.
3. Usando `nano`, añade un comentario en tu `.env` con la fecha de hoy (una línea que empiece con `#`).

### Ejercicio 2: PostgreSQL — Ampliar la Tabla
1. Accede a la base de datos con `sudo -u postgres psql -d taller_db`.
2. Añade una nueva columna a la tabla `estudiantes`:
```sql
ALTER TABLE estudiantes ADD COLUMN semestre INTEGER DEFAULT 1;
```
3. Actualiza los datos de un estudiante:
```sql
UPDATE estudiantes SET semestre = 4 WHERE nombre = 'Ana García';
```
4. Consulta los estudiantes con nota mayor a 4.0:
```sql
SELECT nombre, nota FROM estudiantes WHERE nota > 4.0;
```

### Ejercicio 3: MongoDB — Agregar un Nuevo Experimento
1. Abre `mongo_demo.py` con `nano`.
2. Añade un tercer experimento en el arreglo `experimentos` con tus propios datos (un experimento ficticio de tu carrera).
3. Cambia la consulta de filtrado para buscar documentos con estado `"en análisis"`.
4. Ejecuta el script con `python3 mongo_demo.py` y verifica el resultado.

### Ejercicio 4: Git — Flujo Completo con Ramas
1. Crea una nueva rama para tu trabajo:
```bash
git checkout -b feature/mi-experimento
```
2. Modifica `mongo_demo.py` (agrega tu experimento del Ejercicio 3).
3. Guarda el cambio en Git:
```bash
git add mongo_demo.py
git commit -m "feat: add my custom experiment to mongo demo"
```
4. Fusiona tu rama a `main`:
```bash
git checkout main
git merge feature/mi-experimento
```
5. Sube los cambios a GitHub:
```bash
git push origin main
```

### Ejercicio 5: Reto Final — Un Reporte Completo
Crea un script nuevo llamado `reporte.py` que:
1. Se conecte a **PostgreSQL** y consulte los estudiantes con nota >= 4.0.
2. Se conecte a **MongoDB** y consulte los experimentos con estado `"completado"`.
3. Imprima ambos resultados con un formato legible en la terminal.
4. Versiona el nuevo archivo con `git add reporte.py` y `git commit -m "feat: add report script"` y haz `git push`.

---

##  Resumen de Comandos Clave

| Contexto | Comando | Descripción |
|---|---|---|
| **PostgreSQL** | `sudo systemctl start postgresql` | Iniciar el servicio |
| **PostgreSQL** | `sudo -u postgres psql` | Entrar a la consola |
| **MongoDB** | `sudo systemctl start mongod` | Iniciar el servicio |
| **MongoDB** | `mongosh` | Entrar a la consola |
| **Python** | `python3 -m venv .venv` | Crear entorno virtual |
| **Python** | `source .venv/bin/activate` | Activar entorno virtual |
| **Python** | `pip install -r requirements.txt` | Instalar dependencias |
| **Git** | `git checkout -b nombre-rama` | Crear y cambiar de rama |
| **Git** | `git push origin main` | Subir cambios a GitHub |

---

[⬅️ Volver al Índice Principal](../README.md)
