# Module 1: Linux & The Command Line 🐧

Welcome to the command line! In this module, we will cover the core aspects of using Linux via the terminal (shell). Master these and you'll navigate and manage your computer like a pro.

---

## 1.1 Why Linux? & Understanding Shells

Linux is a powerful, open-source operating system that runs most of the internet's servers, databases, and development tooling. 

*   **The Terminal (or Console):** A text-based program that lets you type commands.
*   **The Shell (e.g., Bash or Zsh):** The command interpreter that reads the text you type and instructs the operating system to perform tasks.

By writing text commands, you gain access to automations and direct control over the computer that graphical user interfaces (GUIs) cannot offer.

---

## 1.2 Essential Navigation

To interact with the system, you must know how to move between folders (called **directories**).

### 1. `pwd` (Print Working Directory)
Shows where you currently are in the file system.
```bash
pwd
# Example Output: /home/user/projects
```

### 2. `ls` (List)
Lists files and folders inside the current directory.
*   `ls -l`: Detailed list (permissions, size, owner, date).
*   `ls -a`: List all files, including hidden files (those starting with a dot, e.g., `.git`).

### 3. `cd` (Change Directory)
Moves you into another folder.
```bash
cd Documents       # Move inside the Documents folder
cd ..              # Move up one level (parent directory)
cd ~               # Move to your Home directory
```

---

## 1.3 File Operations

Now that you know how to navigate, let's learn how to manipulate files and folders.

### 1. `mkdir` (Make Directory)
Creates a new folder.
```bash
mkdir new-folder
```

### 2. `touch`
Creates a new empty file.
```bash
touch hello.txt
```

### 3. `cp` (Copy)
Copies files or directories.
*   *For files:* `cp source.txt destination.txt`
*   *For directories (recursive):* `cp -r folder_a folder_b`

### 4. `mv` (Move / Rename)
Moves or renames files/folders.
```bash
mv hello.txt documents/hello.txt  # Move file
mv oldname.txt newname.txt        # Rename file
```

### 5. `rm` (Remove)
Deletes files or folders.
> ⚠️ **Warning:** The terminal does not have a Recycle Bin/Trash! Deleted files are gone forever.
*   *For files:* `rm file.txt`
*   *For directories (recursive and forced):* `rm -rf folder_name`

---

## 1.4 Advanced Tips: Wildcards & Redirections

As you get more comfortable, you can start combining commands and using shortcuts.

### Wildcards (`*`)
Matches any set of characters.
```bash
rm *.log           # Deletes all files ending with .log
ls project*        # Lists files starting with "project"
```

### Redirections (`>` and `>>`)
Redirects the output of a command to a file instead of showing it in the terminal.
*   `>` overwrites the file.
*   `>>` appends to the file.
```bash
echo "Hello World" > greetings.txt
echo "Adding a second line" >> greetings.txt
```

---

[⬅️ Back to Main Index](../README.md)
