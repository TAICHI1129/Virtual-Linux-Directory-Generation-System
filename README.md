# VDGS (Virtual Linux Directory Generation System)

VDGS is a highly secure, lightweight CLI virtual sandbox system implemented in Python. It simulates an isolated Linux operating environment inside a dedicated host directory while utilizing the host system's native Bash shell capabilities.

---

## Key Features

* **Multi-Platform Support (UnixToWindows)**: Automatically detects the host OS (Linux, macOS, or Windows) and bridges paths and environments seamlessly (e.g., using Git Bash on Windows).
* **Strict Directory Sandbox**: Confines all terminal actions and file system interactions within a designated `virtual_root` folder. Any attempt to traverse out of bounds is instantly neutralized.
* **Linux-Only Executable Validation**: Blocks non-Linux executable binaries (.exe, .app, .bat, etc.). It directly inspects binary magic numbers to ensure only authentic Linux ELF or UNIX Shebang scripts can be executed.
* **Administrative Authentication Gate**: Hardware emulation and network functions are completely isolated by default. Access is unlocked only via external administrative password validation.
* **Isolated Multi-Window Architecture**: Spawns user Bash instances in independent, standalone console windows while the parent controller acts as a secure centralized audit monitor.

---

## Prerequisites & Setup

### For Mac & Linux Users
Ensure that `/bin/bash` is installed and accessible via your default shell. No additional environment setup is required.

### For Windows Users
You must have **Git Bash** (or a compatible Bash environment) installed, and `bash.exe` must be added to your system's **Environment Variables (Path)**.
* Test this by opening a command prompt (cmd) and typing "bash". If the shell launches, VDGS will run perfectly.

---

## Installation & Usage

1. Save the VDGS core script as `vdgs.py`.
2. Run the main system using Python:

    python vdgs.py

3. Upon initialization, a folder named `virtual_root/` will be generated in the script's local path. This folder serves as the exclusive sandbox storage.

---

## Core Management Commands

Execute these commands inside the main `VDGS-Controller#` console to orchestrate the sandbox environment.

### 1. Interactive Terminal Deployment
Spawns an isolated native Bash terminal instance in a separate popping window.

    open

### 2. Virtual USB Port Mapping
Securely mounts a host physical folder or endpoint path to the sandbox network path (`/mnt/usb`).
* **Default Admin Password**: `vdgs_secure_pass`

    # Connect / Map a virtual device
    vdgs-usb --connect [DeviceName] [HostPathOrPort]

    # Disconnect / Safely unmount
    vdgs-usb --disconnect

### 3. Network Isolation Management
Lifts or applies strict sandboxed proxy network restrictions on spawned child shell processes.

    # Unlock Internet Access (Requires Admin Password)
    vdgs-net --connect

    # Re-apply Strict Network Isolation
    vdgs-net --disconnect

### 4. Secure Termination
Termulates all connected instances and safely shuts down the VDGS controller framework.

    exit

---

## Security Architecture Overview

+-------------------------------------------------------------+

|                     Host PC System                          |
|                                                             |
|   +-----------------------------------------------------+   |
|   |         VDGS Controller (Parent Process)            |   |
|   +-------------------+---------------------------------+   |
|                       |                                     |
|           [Spawns Isolated Child Window]                    |
|                       v                                     |
|   +-----------------------------------------------------+   |
|   |         Isolated Bash Window (guest@sandbox)        |   |
|   |                                                     |   |
|   |  - Static analysis blocks out-of-bounds traversal   |   |
|   |  - Dynamic verification limits binaries to ELF/#!    |   |
|   |  - Network default spoofed via internal proxies      |   |
|   |  - File state mirrored strictly to ./virtual_root/  |   |
|   +-----------------------------------------------------+   |
+-------------------------------------------------------------+

---

## License
This system is provided as a secure development sandbox simulator. Feel free to modify, scale up, or integrate the security pipeline mechanisms into larger virtual architecture projects.
