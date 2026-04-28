# VS Code Python Virtual Environment Setup 🐍

Complete guide for setting up Python virtual environments in Visual Studio Code for both Windows and Linux.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=flat&logo=visual-studio-code&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=flat&logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)

## 📋 Table of Contents
- [Prerequisites](#prerequisites)
- [Windows Setup](#windows-setup)
- [Linux Setup](#linux-setup)
- [VS Code Configuration](#vs-code-configuration)
- [Installing Packages](#installing-packages)
- [Troubleshooting](#troubleshooting)

## 🔧 Prerequisites

### Windows
- Python 3.8+ installed
- Visual Studio Code
- Windows Terminal or Command Prompt

### Linux
- Python 3.8+ and pip
- Visual Studio Code
- Terminal

---

## 🪟 Windows Setup

### Step 1: Install Python

1. Download from [python.org](https://www.python.org/downloads/)
2. Run installer
3. ✅ Check "Add Python to PATH"
4. Click "Install Now"

### Step 2: Verify Installation

```cmd
python --version
pip --version
```

### Step 3: Install VS Code

1. Download from [code.visualstudio.com](https://code.visualstudio.com/)
2. Install with default settings

### Step 4: Install Python Extension

1. Open VS Code
2. Press `Ctrl+Shift+X`
3. Search "Python"
4. Install "Python" by Microsoft

### Step 5: Create Project Folder

```cmd
cd Desktop
mkdir my-python-project
cd my-python-project
```

### Step 6: Create Virtual Environment

```cmd
python -m venv venv
```

This creates a `venv` folder in your project.

### Step 7: Activate Virtual Environment

```cmd
venv\Scripts\activate
```

You'll see `(venv)` in your terminal.

### Step 8: Open in VS Code

```cmd
code .
```

### Step 9: Select Python Interpreter

1. Press `Ctrl+Shift+P`
2. Type "Python: Select Interpreter"
3. Choose the one with `.\venv\Scripts\python.exe`

### Step 10: Deactivate (when done)

```cmd
deactivate
```

---

## 🐧 Linux Setup

### Step 1: Install Python and pip

**Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

**Fedora:**
```bash
sudo dnf install python3 python3-pip
```

**Arch:**
```bash
sudo pacman -S python python-pip
```

### Step 2: Verify Installation

```bash
python3 --version
pip3 --version
```

### Step 3: Install VS Code

**Ubuntu/Debian:**
```bash
sudo snap install code --classic
# OR
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code
```

**Fedora:**
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf install code
```

### Step 4: Install Python Extension

1. Open VS Code: `code`
2. Press `Ctrl+Shift+X`
3. Search "Python"
4. Install "Python" by Microsoft

### Step 5: Create Project Folder

```bash
cd ~/Documents
mkdir my-python-project
cd my-python-project
```

### Step 6: Create Virtual Environment

```bash
python3 -m venv venv
```

### Step 7: Activate Virtual Environment

```bash
source venv/bin/activate
```

You'll see `(venv)` in your terminal.

### Step 8: Open in VS Code

```bash
code .
```

### Step 9: Select Python Interpreter

1. Press `Ctrl+Shift+P`
2. Type "Python: Select Interpreter"
3. Choose `./venv/bin/python`

### Step 10: Deactivate (when done)

```bash
deactivate
```

---

## ⚙️ VS Code Configuration

### Recommended Extensions

```
Python
Pylance
Python Indent
autopep8
```

### Create settings.json

Press `Ctrl+Shift+P` → "Preferences: Open Settings (JSON)"

Add:
```json
{
    "python.defaultInterpreterPath": "${workspaceFolder}/venv/bin/python",
    "python.terminal.activateEnvironment": true,
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.formatting.provider": "autopep8",
    "editor.formatOnSave": true,
    "[python]": {
        "editor.defaultFormatter": "ms-python.autopep8"
    }
}
```

### Create .vscode/launch.json for Debugging

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal"
        }
    ]
}
```

---

## 📦 Installing Packages

### Create requirements.txt

```txt
numpy==1.24.3
pandas==2.0.3
matplotlib==3.7.2
requests==2.31.0
```

### Install from requirements.txt

**Windows:**
```cmd
venv\Scripts\activate
pip install -r requirements.txt
```

**Linux:**
```bash
source venv/bin/activate
pip install -r requirements.txt
```

### Install Individual Package

```bash
pip install package-name
```

### List Installed Packages

```bash
pip list
```

### Export Current Environment

```bash
pip freeze > requirements.txt
```

---

## 🛠️ Troubleshooting

### Issue: "python: command not found" (Windows)

**Solution:** Reinstall Python with "Add to PATH" checked.

### Issue: "python3: command not found" (Linux)

**Solution:**
```bash
sudo apt install python3
```

### Issue: Virtual environment not activating

**Windows PowerShell:**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
venv\Scripts\Activate.ps1
```

**Linux:**
```bash
chmod +x venv/bin/activate
source venv/bin/activate
```

### Issue: VS Code not detecting interpreter

**Solution:**
1. `Ctrl+Shift+P`
2. "Python: Select Interpreter"
3. Click "Enter interpreter path"
4. Browse to `venv/Scripts/python.exe` (Windows) or `venv/bin/python` (Linux)

### Issue: pip command not found in venv

**Solution:**
```bash
python -m pip install --upgrade pip
```

---

## 📚 Best Practices

1. **One venv per project** - Keep environments isolated
2. **Use requirements.txt** - Document all dependencies
3. **Add venv to .gitignore** - Don't commit virtual environments
4. **Activate before coding** - Always activate venv before running code
5. **Update pip regularly** - `pip install --upgrade pip`

---

## 📁 Project Structure

```
my-python-project/
├── venv/                  # Virtual environment (don't commit)
├── .vscode/
│   ├── settings.json
│   └── launch.json
├── src/
│   └── main.py
├── tests/
│   └── test_main.py
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 🎯 Quick Reference

### Windows Commands
```cmd
# Create venv
python -m venv venv

# Activate
venv\Scripts\activate

# Deactivate
deactivate

# Install packages
pip install -r requirements.txt

# Open VS Code
code .
```

### Linux Commands
```bash
# Create venv
python3 -m venv venv

# Activate
source venv/bin/activate

# Deactivate
deactivate

# Install packages
pip install -r requirements.txt

# Open VS Code
code .
```

---

## 📄 License

MIT License

---
Made with ❤️ for Python developers
