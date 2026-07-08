# Workshop: Databases with Python and GitHub 

> **Estimated Duration:** 3 to 4 hours | **Level:** Beginner-Intermediate
> **Prerequisites:** Having completed Module 1 (Linux Terminal) and Module 2 (Git Essentials).

In this workshop you will learn to install and configure two of the most widely-used database management systems in the professional world, connect them to Python, and version your work securely on GitHub.

---

## 🎯 Workshop Objectives

By the end of this workshop you will be able to:
- Install and configure **PostgreSQL** (relational database) and **MongoDB** (NoSQL database).
- Connect to both databases from a **Python** script.
- Store credentials securely using `.env` files.
- Version your project with **Git** without exposing sensitive information.
- Collaborate and submit your work on **GitHub** the way it is done in industry.

---

## Part 1: Installing PostgreSQL 🐘

PostgreSQL is an open-source relational database management system (SQL), extremely robust and widely used in industry and data science.

### 1.1 Installation

Open the terminal and run the following commands one by one:

```bash
# 1. Update the list of available packages
sudo apt update

# 2. Install PostgreSQL and its client utilities
sudo apt install -y postgresql postgresql-contrib
```

Verify the service is active:

```bash
sudo systemctl status postgresql
```

You should see a line saying `Active: active (running)`. Press `q` to exit.

### 1.2 Accessing PostgreSQL

PostgreSQL automatically creates a system user called `postgres`. To access the interactive interpreter:

```bash
sudo -u postgres psql
```

You are now inside the PostgreSQL console. The prompt changes to `postgres=#`.

### 1.3 Create Your User and Database

Run these commands **inside the PostgreSQL console** (`postgres=#`):

```sql
-- Create a new user (replace 'your_user' and 'your_password' with yours)
CREATE USER your_user WITH PASSWORD 'your_password';

-- Create a database for the workshop
CREATE DATABASE workshop_db;

-- Grant all privileges on the database to your user
GRANT ALL PRIVILEGES ON DATABASE workshop_db TO your_user;

-- Exit the console
\q
```

> [!NOTE]
> Save your username and password somewhere safe. You will use them later in the `.env` file.

### 1.4 Useful PostgreSQL Commands

| Command | Description |
|---|---|
| `\l` | List all databases |
| `\c db_name` | Connect to a database |
| `\dt` | List all tables in the current database |
| `\du` | List all users |
| `\q` | Exit the console |

---

## Part 2: Installing MongoDB 🍃

MongoDB is a **document-oriented NoSQL** database. It stores information in JSON-like documents (called BSON internally), making it very flexible for unstructured or schema-changing data.

### 2.1 Installation

MongoDB is not in the official Ubuntu/Mint repositories, so we must add the official repository:

```bash
# 1. Install required dependencies
sudo apt install -y gnupg curl

# 2. Import the official MongoDB GPG key
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor

# 3. Add the official MongoDB repository (for Ubuntu 22.04 / Mint 21)
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | \
   sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# 4. Update the package list and install MongoDB
sudo apt update
sudo apt install -y mongodb-org
```

### 2.2 Start the Service

```bash
# Start MongoDB
sudo systemctl start mongod

# Enable automatic startup when the computer turns on
sudo systemctl enable mongod

# Verify it is active
sudo systemctl status mongod
```

### 2.3 Accessing MongoDB

Access the MongoDB interactive interpreter:

```bash
mongosh
```

The prompt changes to `test>`. Try a basic command:

```javascript
// Show all databases
show dbs

// Exit
exit
```

---

## Part 3: Setting Up the Python Environment 🐍

Never install Python packages directly on the system. Always use a **virtual environment** to isolate each project's dependencies.

### 3.1 Create the Project Structure

```bash
# Navigate to your projects folder or create a new one
mkdir ~/workshop-db && cd ~/workshop-db

# Create the virtual environment
python3 -m venv .venv

# Activate the virtual environment
source .venv/bin/activate
```

Your terminal prompt will now show `(.venv)` at the beginning, indicating the environment is active.

### 3.2 Install Dependencies

```bash
pip install psycopg2-binary pymongo python-dotenv
```

| Library | Purpose |
|---|---|
| `psycopg2-binary` | Connect Python to PostgreSQL |
| `pymongo` | Connect Python to MongoDB |
| `python-dotenv` | Read environment variables from a `.env` file |

Save the dependencies to a `requirements.txt` file:

```bash
pip freeze > requirements.txt
```

### 3.3 Create the `.env` File with Credentials

The `.env` file stores your passwords and sensitive data **outside the code**. It must never be uploaded to GitHub.

```bash
nano .env
```

Write the following (replace with your real data):

```
# PostgreSQL credentials
PG_HOST=localhost
PG_PORT=5432
PG_DATABASE=workshop_db
PG_USER=your_user
PG_PASSWORD=your_password

# MongoDB credentials
MONGO_URI=mongodb://localhost:27017
MONGO_DATABASE=workshop_mongo_db
```

Save with `Ctrl + O`, `Enter`, and close with `Ctrl + X`.

---

## Part 4: Python Connection Scripts 💻

### 4.1 Connection and Operations with PostgreSQL

Create the file `postgres_demo.py`:

```bash
nano postgres_demo.py
```

```python
import psycopg2
from dotenv import load_dotenv
import os

# Load variables from the .env file
load_dotenv()

# Establish the connection using environment variables
conn = psycopg2.connect(
    host=os.getenv("PG_HOST"),
    port=os.getenv("PG_PORT"),
    dbname=os.getenv("PG_DATABASE"),
    user=os.getenv("PG_USER"),
    password=os.getenv("PG_PASSWORD")
)

cursor = conn.cursor()
print("✅ PostgreSQL connection established.")

# --- CREATE TABLE ---
cursor.execute("""
    CREATE TABLE IF NOT EXISTS students (
        id SERIAL PRIMARY KEY,
        name VARCHAR(100) NOT NULL,
        major VARCHAR(100),
        grade FLOAT
    );
""")
conn.commit()
print("📋 Table 'students' verified/created.")

# --- INSERT DATA ---
students = [
    ("Ana García", "Biology", 4.5),
    ("Carlos Ruiz", "Engineering", 3.8),
    ("Sofía Martínez", "Chemistry", 4.9),
]
cursor.executemany(
    "INSERT INTO students (name, major, grade) VALUES (%s, %s, %s);",
    students
)
conn.commit()
print(f"➕ {cursor.rowcount} students inserted.")

# --- QUERY DATA ---
cursor.execute("SELECT * FROM students ORDER BY grade DESC;")
rows = cursor.fetchall()

print("\n📊 Students by grade (highest to lowest):")
print(f"{'ID':<5} {'Name':<20} {'Major':<20} {'Grade':<5}")
print("-" * 55)
for row in rows:
    print(f"{row[0]:<5} {row[1]:<20} {row[2]:<20} {row[3]:<5}")

# --- CLOSE CONNECTION ---
cursor.close()
conn.close()
print("\n🔒 Connection closed.")
```

Run the script:

```bash
python3 postgres_demo.py
```

### 4.2 Connection and Operations with MongoDB

Create the file `mongo_demo.py`:

```bash
nano mongo_demo.py
```

```python
from pymongo import MongoClient
from dotenv import load_dotenv
import os
from datetime import datetime

# Load variables from the .env file
load_dotenv()

# Establish the connection
client = MongoClient(os.getenv("MONGO_URI"))
db = client[os.getenv("MONGO_DATABASE")]
print("✅ MongoDB connection established.")

# Select (or create) the collection
collection = db["experiments"]

# --- INSERT DOCUMENTS ---
experiments = [
    {
        "title": "Aspirin Synthesis",
        "researcher": "Ana García",
        "date": datetime(2025, 3, 15),
        "results": {"yield_pct": 87.5, "purity_pct": 99.1},
        "status": "completed"
    },
    {
        "title": "DNA Extraction from Banana",
        "researcher": "Carlos Ruiz",
        "date": datetime(2025, 4, 2),
        "results": {"yield_pct": 72.3},
        "status": "under analysis"
    },
]

result = collection.insert_many(experiments)
print(f"➕ Documents inserted with IDs: {result.inserted_ids}")

# --- QUERY DOCUMENTS ---
print("\n📋 All experiments:")
for doc in collection.find():
    print(f"  - {doc['title']} | Researcher: {doc['researcher']} | Status: {doc['status']}")

# --- FILTER DOCUMENTS ---
print("\n🔍 Completed experiments:")
completed = collection.find({"status": "completed"})
for doc in completed:
    print(f"  - {doc['title']} | Yield: {doc['results'].get('yield_pct')}%")

# --- CLOSE CONNECTION ---
client.close()
print("\n🔒 Connection closed.")
```

Run the script:

```bash
python3 mongo_demo.py
```

---

## Part 5: Git and GitHub Integration 🌿

### 5.1 Create the `.gitignore` File

This file tells Git which files **not to track or upload**. It is the most important security step.

```bash
nano .gitignore
```

```
# Python virtual environment (not versioned, recreated with pip install)
.venv/
__pycache__/
*.pyc

# Credentials file (NEVER upload this to GitHub!)
.env

# System files
.DS_Store
```

Save and close (`Ctrl + O`, `Enter`, `Ctrl + X`).

> [!CAUTION]
> If you accidentally upload the `.env` file to GitHub with real passwords, you must change those passwords **immediately**. Git saves the history and anyone can see it.

### 5.2 Initialize the Git Repository

```bash
# Initialize the repository
git init

# See the current status (you will see untracked files)
git status
```

### 5.3 Make Your First Commit

```bash
# Add all relevant files to the staging area
git add .

# Verify that .env does NOT appear in the list (git status)
git status

# Create the first commit
git commit -m "feat: add database connection scripts and project setup"
```

### 5.4 Connect to GitHub and Push the Project

1. Go to [github.com](https://github.com) and create a new repository called `workshop-db-python` (empty, without a README).
2. Copy the repository URL (example: `https://github.com/your_username/workshop-db-python.git`).
3. Run in the terminal:

```bash
# Link the local repository with the remote on GitHub
git remote add origin https://github.com/your_username/workshop-db-python.git

# Push the changes to the main branch
git push -u origin main
```

---

## 🏋️ Practice Exercises

### Exercise 1: Linux — Explore the Environment
1. Use `ls -la ~/workshop-db/` to list all project files, including hidden ones. Can you see `.env` and `.venv`? Why are they important?
2. Use `cat requirements.txt` to see the project dependencies.
3. Using `nano`, add a comment in your `.env` with today's date (a line starting with `#`).

### Exercise 2: PostgreSQL — Extend the Table
1. Access the database with `sudo -u postgres psql -d workshop_db`.
2. Add a new column to the `students` table:
```sql
ALTER TABLE students ADD COLUMN semester INTEGER DEFAULT 1;
```
3. Update a student's data:
```sql
UPDATE students SET semester = 4 WHERE name = 'Ana García';
```
4. Query students with a grade above 4.0:
```sql
SELECT name, grade FROM students WHERE grade > 4.0;
```

### Exercise 3: MongoDB — Add a New Experiment
1. Open `mongo_demo.py` with `nano`.
2. Add a third experiment to the `experiments` list with your own data (a fictional experiment from your field of study).
3. Change the filter query to find documents with status `"under analysis"`.
4. Run the script with `python3 mongo_demo.py` and verify the result.

### Exercise 4: Git — Full Workflow with Branches
1. Create a new branch for your work:
```bash
git checkout -b feature/my-experiment
```
2. Modify `mongo_demo.py` (add your experiment from Exercise 3).
3. Save the change to Git:
```bash
git add mongo_demo.py
git commit -m "feat: add my custom experiment to mongo demo"
```
4. Merge your branch into `main`:
```bash
git checkout main
git merge feature/my-experiment
```
5. Push the changes to GitHub:
```bash
git push origin main
```

### Exercise 5: Final Challenge — A Complete Report
Create a new script called `report.py` that:
1. Connects to **PostgreSQL** and queries students with a grade >= 4.0.
2. Connects to **MongoDB** and queries experiments with status `"completed"`.
3. Prints both results in a readable format in the terminal.
4. Versions the new file with `git add report.py` and `git commit -m "feat: add report script"` and runs `git push`.

---

## 📋 Key Commands Summary

| Context | Command | Description |
|---|---|---|
| **PostgreSQL** | `sudo systemctl start postgresql` | Start the service |
| **PostgreSQL** | `sudo -u postgres psql` | Enter the console |
| **MongoDB** | `sudo systemctl start mongod` | Start the service |
| **MongoDB** | `mongosh` | Enter the console |
| **Python** | `python3 -m venv .venv` | Create virtual environment |
| **Python** | `source .venv/bin/activate` | Activate virtual environment |
| **Python** | `pip install -r requirements.txt` | Install dependencies |
| **Git** | `git checkout -b branch-name` | Create and switch to branch |
| **Git** | `git push origin main` | Push changes to GitHub |

---

[⬅️ Back to Main Index](../README.md)
