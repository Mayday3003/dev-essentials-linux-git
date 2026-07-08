# Module 1: Linux & The Command Line 🐧

Welcome to the command line! In this module, we will cover everything from the core concepts of the operating system to the advanced usage of the terminal (shell). Mastering this will give you full control over your computer, servers, and development workflows.

---

## 1.1 Fundamentals: Understanding Linux and the Kernel

We often refer to the entire operating system as "Linux", but in strict terms, **Linux is only the Kernel (the core)**.

To understand the difference, let's use a simple analogy:
*   **The Hardware (Processor, RAM, Storage):** This is the chassis and wheels of a car.
*   **The Kernel (Linux):** This is the engine. It talks directly to the physical components, allocates power (resources), and makes everything run.
*   **The Desktop Environment and Applications:** These are the steering wheel, seats, and dashboard that the driver (you) interacts with.

Linux is open-source, extremely stable, and highly secure. For this reason, it is the undisputed standard for internet servers, supercomputers, databases, and high-performance processing clusters.

### Distributions (Distros)
Since Linux is just the "engine", different communities and companies build their own "car" around it by adding installers, package managers, and desktop environments. This complete package is called a **Distribution (Distro)**.

In development and research environments, you will primarily interact with two families:
1.  **Debian / Ubuntu / Linux Mint Family:** The most user-friendly and popular distros. Their graphical interfaces are highly intuitive, and they are excellent for creating portable, persistent USB environments.
2.  **Red Hat / Fedora Family:** Modern, robust systems that integrate the latest technologies. They are widely used in corporate environments and advanced research workstations.

---

## 1.2 Options for Using Linux

You do not need to delete your current operating system (Windows or macOS) to learn and use Linux. There are several alternatives depending on your needs:

1.  **Live USB (Live Pendrive):** Runs Linux directly from a USB drive without modifying your hard drive or files. It is ideal for learning and having a portable system you can use on any computer.
2.  **WSL (Windows Subsystem for Linux):** Allows you to run a Linux terminal natively inside Windows, which is ideal for developers who need Linux command-line tools on a Windows PC.
3.  **Virtual Machines (VMs):** Using programs like VirtualBox or VMware, you can run Linux as a window or application inside your current operating system.
4.  **Dual Boot:** Installs Linux on a separate partition of your hard drive alongside Windows or macOS. When you turn on your computer, you choose which system to boot.
5.  **Dedicated Installation:** Completely replacing your previous operating system and using Linux as the sole OS on the computer.

---

## 1.3 Booting from USB Guide (Booting)

If you are going to use Linux from a **Live USB**, you must instruct your computer to boot from the flash drive instead of the internal hard drive.

### 1. General PC Boot Process
1.  Turn off your computer completely.
2.  Insert your Linux USB drive into a USB port.
3.  Turn on the machine and, **immediately and repeatedly**, press the **Boot Menu** or BIOS key for your manufacturer.
4.  Select the USB drive from the list and press `Enter`.
5.  Choose the option **"Start Linux Mint"** (or the corresponding distro option).

#### Common Boot Keys by Brand:
| Brand | Boot Menu / BIOS Key |
| :--- | :--- |
| **HP** | `F9` or `Esc` |
| **Dell** | `F12` |
| **Lenovo** | `F12` or physical `Novo` button (on laptops) |
| **Asus** | `Esc` or `F8` |
| **Acer** | `F12` or `F2` *(Note: you may need to enable "F12 Boot Menu" in the BIOS first)* |
| **Toshiba** | `F12` |
| **Apple (Intel)** | Hold down the `Option/Alt` (`⌥`) key during boot |

---

### 2. Specific Guide for MacBook Air (Retina, 13", 2019 - Apple T2 Security Chip)
Apple computers built between 2018 and 2020 that feature the **Apple T2 security chip** block booting from external drives by default to secure the system. To use a Live USB on these machines, you must perform a one-time initial setup.

> [!NOTE]
> This process does not delete your files or modify your macOS. It only allows the Mac to boot from your Linux USB if you explicitly choose to do so when turning it on.

#### Part 1: Authorizing External Boot (One-time setup)
1.  Shut down your MacBook Air completely.
2.  Turn it on and hold down the **`Cmd (⌘) + R`** keys until the Apple logo or a spinning globe appears. This loads **macOS Recovery**.
3.  If prompted, select your macOS user and enter your administrator password.
4.  In the top menu bar, click **Utilities** > **Startup Security Utility**.
5.  Authenticate again if prompted.
6.  Under **Secure Boot**, select **No Security**. (This ensures maximum compatibility with Linux distros).
7.  Under **External Boot**, select **Allow booting from external or removable media**.
8.  Close the utility and restart your Mac from the Apple menu.

#### Part 2: Booting Linux Mint from the USB Drive
1.  Shut down your MacBook Air completely.
2.  Connect your USB drive (use a USB-A to USB-C adapter if needed).
3.  Turn on the computer and immediately hold down the **`Option/Alt (⌥)`** key.
4.  Release it when you see the grey **Startup Manager** screen showing available disks.
5.  Select the yellow/orange disk icon labeled **"EFI Boot"** and press `Enter`.
6.  The Linux Mint boot menu will appear. Press `Enter` to load the Cinnamon desktop.

> [!TIP]
> **No WiFi on your T2 chip MacBook?**
> Some built-in Broadcom network cards in Macs require proprietary drivers that are not pre-installed. If you cannot see any WiFi networks:
> *   Connect to the internet temporarily using a USB-to-Ethernet adapter.
> *   Open the **Update Manager** or **Driver Manager** in Linux Mint, where the system will automatically detect and install the appropriate driver.

#### Part 3: Exiting Linux Mint and Returning to macOS
1.  In Linux Mint, go to the bottom-left Menu, click the power button, and select **Shut Down**.
2.  Wait for the machine to turn off completely and **remove the USB drive**.
3.  Turn on your Mac normally. It will boot automatically into macOS, exactly as you left it.

---

## 1.4 Graphical Environment vs Console: Cinnamon Desktop and Nemo

When you start Linux Mint, you will see the **Cinnamon** desktop environment. Its layout is familiar if you are coming from Windows:
*   **The Menu:** Located in the bottom-left corner. Provides access to installed programs, organized by category.
*   **The Bottom Panel:** The taskbar containing open windows, the clock, and system tray icons (network, volume, updates).
*   **File Manager (Nemo):** The graphical program to browse folders, create files, copy, move, and delete items visually.

### The Linux File System
Unlike Windows, Linux **does not have drive letters** like `C:` or `D:`. Everything is organized under a single hierarchical tree that starts at the **Root**, represented by a forward slash (`/`).

The most important directories for a user are:
*   **`/home/your_username`:** Your personal directory (Home). This is where your documents, downloads, desktop, and personal configurations are stored. It is equivalent to `C:\Users\your_username` in Windows.
*   **`/media` or `/mnt`:** Mount directories. This is where Linux automatically mounts your USB drives, external hard drives, and other system partitions.
*   **`/etc`:** Contains configuration files for the entire operating system and installed programs (modified using admin privileges).
*   **`/usr`:** Contains installed programs and their shared assets.

---

## 1.5 The Terminal and The Shell: What is Bash?

While the graphical interface is convenient, the true power of Linux lies in its text interface.

*   **The Terminal (or Console):** The graphical window or application that lets you interact with the system via text (open it in Linux Mint with `Ctrl + Alt + T`).
*   **The Shell (Command Interpreter):** The internal program that reads the commands you type in the terminal, translates them, and instructs the Kernel to execute the task.
*   **Bash (Bourne Again SHell):** The most popular command interpreter and the default standard in most Linux distributions. When you learn command-line skills in Linux, you are learning the syntax of Bash.

> [!NOTE]
> Another common shell is **Zsh**, which is used by default on modern macOS systems, but it shares more than 95% of its syntax and commands with Bash.

---

## 1.6 Permissions and Security: The Power of `sudo` and Root

Linux is built from the ground up to be a secure, multi-user system.

*   **Standard User:** Your daily account. You have permission to modify your own files in `/home/your_username`, but you cannot modify system configurations or damage critical system files.
*   **Superuser (Root):** The supreme administrator of the system. Root has unlimited power to install software, change settings, and delete any file.
*   **`sudo` (SuperUser DO):** The command that tells the terminal: *"Lend me Superuser (Root) privileges for a moment to run this specific action"*.

> [!IMPORTANT]
> **Password Entry in the Terminal:**
> When executing a command using `sudo`, the terminal will ask for your user password. As you type, **no characters will appear on the screen (no asterisks, no dots)**. This is a normal security feature to prevent onlookers from seeing the password length. Just type it normally and press `Enter`.

---

## 1.7 Essential Navigation

To work in the command line, you need to know how to move through the directory tree (your working directory).

### 1. `pwd` (Print Working Directory)
Shows the complete path of the folder you are currently in.
```bash
pwd
# Example output: /home/user/LinuxMintCourse
```

### 2. `ls` (List)
Lists the contents of the current directory (files and folders).
*   `ls -l`: Displays a detailed list (permissions, size, owner, and modification date).
*   `ls -a`: Shows all files, including hidden files (those starting with a dot, such as `.git`).
*   `ls -lh`: Displays file sizes in a human-readable format (KB, MB, GB).

### 3. `cd` (Change Directory)
Changes your directory to navigate between folders.
```bash
cd Documents      # Enter the "Documents" folder
cd ..              # Go up one level (parent directory)
cd ~               # Go straight to your Home directory
cd /               # Go to the root of the file system
```

---

## 1.8 File Operations

Learn how to create, copy, move, and delete files and directories from the command line.

### 1. `mkdir` (Make Directory)
Creates a new folder.
```bash
mkdir Practices
```

### 2. `touch`
Creates a new empty text file (or updates the modification timestamp if it already exists).
```bash
touch practice1.txt
```

### 3. `cp` (Copy)
Copies a file or a folder from one location to another.
*   **Copy file:** `cp file.txt destination.txt`
*   **Copy folder:** To copy complete directories with their contents, you must use the recursive `-r` flag.
    ```bash
    cp -r source_folder/ destination_folder/
    ```

### 5. `mv` (Move / Rename)
Moves files or folders, or changes their name if the destination is in the same directory.
```bash
mv practice1.txt Documents/practice1.txt   # Moves the file
mv practice1.txt final_practice.txt         # Renames the file
```

### 5. `rm` (Remove)
Deletes files or directories permanently.

> [!WARNING]
> The terminal has no Recycle Bin or Trash! Files deleted with `rm` are gone forever immediately. Use it with extreme caution.

*   **Delete a file:** `rm notes.txt`
*   **Delete an empty folder:** `rmdir empty_folder/`
*   **Delete a folder with content:** Requires the recursive and force `-rf` flags.
    ```bash
    rm -rf folder_with_files/
    ```

---

## 1.9 Nano Text Editor

When working on remote servers or in a terminal without a GUI, you need a text editor built into the command line. **`nano`** is the ideal editor for beginners because it is simple and always lists its shortcuts at the bottom of the screen.

To open or create a file with nano:
```bash
nano experiment_notes.txt
```

### Key Shortcuts in Nano (The `^` symbol represents the `Ctrl` key):
*   **Save changes (`Ctrl + O`):** Press `Ctrl + O`, confirm the file name with `Enter`, and the changes will be written.
*   **Exit the editor (`Ctrl + X`):** Closes nano. If you have unsaved changes, it will ask if you want to save them (`Y` for yes, `N` for no).
*   **Search text (`Ctrl + W`):** Opens the search bar to find text within the file.

---

## 1.10 Package Management (Installing Software)

In Linux, you rarely download `.exe` installers from websites. Instead, the system uses **Package Managers** that connect to secure online repositories to download and install programs from a central hub.

### 1. Graphical Package Management (Software Manager)
In Linux Mint, you can open the menu and search for the **Software Manager**. It is an app store where you can search by name (like VLC, GIMP, VS Code) and install them with a single click after entering your password.

### 2. Command Line Package Management
Depending on the distribution you use, the commands differ slightly:

#### For Debian / Ubuntu / Linux Mint systems (using `apt`)
*   **Update the list of available packages from the internet:**
    ```bash
    sudo apt update
    ```
*   **Install a new package:**
    ```bash
    sudo apt install package_name
    ```
*   **Uninstall/remove a package:**
    ```bash
    sudo apt remove package_name
    ```
*   **Upgrade all programs on the system to their latest versions:**
    ```bash
    sudo apt upgrade
    ```

#### For Red Hat / Fedora systems (using `dnf`)
*   **Install a new package:**
    ```bash
    sudo dnf install package_name
    ```
*   **Remove a package:**
    ```bash
    sudo dnf remove package_name
    ```

---

## 1.11 Maintenance and Backups: Updates and Timeshift

A stable system requires simple but effective preventive maintenance.

### 1. Update Manager
Linux Mint features a small shield icon in the taskbar. Check it regularly to apply security updates and bug fixes (levels 1 to 3 are the most common and recommended).

### 2. Backups with Timeshift
Timeshift is a built-in application in Linux Mint that allows you to take **snapshots** of your operating system's state. If a system update or configuration breaks your system, you can open Timeshift and restore it to the previous state, making it work again instantly.

*   **Basic setup:** Open Timeshift from the menu, select **RSYNC** as the snapshot type, and choose a destination drive (preferably an external drive).
*   **Create Snapshot:** Click **Create** to save the current state of the system before making critical modifications.

---

## 1.12 Safe Shutdown and Advanced Tips

As you get more comfortable in the console, you can use tips and tricks to automate and speed up tasks.

### Wildcards (`*`)
The asterisk (`*`) symbol acts as a wildcard representing any text.
```bash
rm *.log           # Deletes ALL files ending in .log
ls data*          # Lists all files starting with "data"
```

### Redirections (`>` and `>>`)
Allow you to send the text output of a command directly to a file instead of displaying it on the terminal screen.
*   `>`: Overwrites the file with the new text (creates it if it doesn't exist).
*   `>>`: Appends the text to the end of the existing file without erasing what was there.
```bash
echo "Start of experiment" > logs.txt
echo "Step 1 completed successfully" >> logs.txt
```

### Safe Shutdown from a Live USB
If you are running a **Live USB** and want to shut down the computer ensuring the USB filesystem doesn't get corrupted and all cached data is written to the flash memory, run this in the terminal:
```bash
sudo sync && sudo poweroff -f
```
*   `sync`: Forces the system to write any cached data in memory to the USB drive.
*   `poweroff -f`: Shuts down the computer immediately.

---

[⬅️ Back to Main Index](../README.md)
