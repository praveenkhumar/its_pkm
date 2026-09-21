# Windows Guide: Managing Python Environments with `venv` and `uv`

This guide explains how to set up, isolate, and manage Python virtual environments on Windows using both the standard built-in **`venv`** module and the blazing-fast modern package and environment manager **`uv`** (by Astral).

---

## Table of Contents
1. [Overview: venv vs. uv](#overview-venv-vs-uv)
2. [Part 1: Built-in Virtual Environments (`venv`)](#part-1-built-in-virtual-environments-venv)
   - [Creating a venv](#1-create-a-venv)
   - [Activating in PowerShell or Command Prompt](#2-activate-the-environment)
   - [Fixing PowerShell Script Execution Policy](#3-handling-powershell-execution-policy-errors)
   - [Installing Packages & Deactivating](#4-installing-packages-and-deactivating)
3. [Part 2: Modern Python & Environment Manager (`uv`)](#part-2-modern-python--environment-manager-uv)
   - [Installing `uv` on Windows](#1-install-uv-on-windows)
   - [Verifying the Installation](#2-verify-uv-installation)
   - [Installing Python via `uv`](#3-optional-installing-python-versions-via-uv)
   - [Creating & Managing Environments with `uv venv`](#4-creating-environments-with-uv-venv)
   - [Modern Project Workflow (`uv init`, `uv add`, `uv run`)](#5-modern-project-workflow-recommended)
4. [Quick Command Cheatsheet](#quick-command-cheatsheet)

---

## Overview: venv vs. uv

| Feature | Standard `venv` | Modern `uv` |
| :--- | :--- | :--- |
| **Origin** | Built into standard Python library | Standalone Rust-based binary by Astral |
| **External Tools Needed** | None (comes with Python) | Needs a one-time install |
| **Speed** | Moderate | 10x–100x faster than `pip` and standard `venv` |
| **Python Version Management** | Uses whichever Python is on your PATH | Can download and manage multiple Python versions |
| **Best For** | Zero-dependency scripts, quick isolated testing | Modern application development, fast CI/CD, production |

---

## Part 1: Built-in Virtual Environments (`venv`)

The `venv` module is built into Python 3 on Windows, meaning you don't need to install any external tools.

### 1. Create a `venv`

1. Open **Command Prompt** (`cmd`) or **PowerShell**.
2. Navigate to your project directory:
   ```cmd
   cd C:\Users\<YourUsername>\Desktop\my_project
   ```
3. Run the creation command:
   ```cmd
   python -m venv .venv
   ```
   *(This creates an isolated environment inside a hidden folder named `.venv`).*

---

### 2. Activate the Environment

You must run the activation script corresponding to your active terminal shell:

- **In PowerShell:**
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```

- **In Command Prompt (CMD):**
  ```cmd
  .venv\Scripts\activate.bat
  ```

- **In Git Bash:**
  ```bash
  source .venv/Scripts/activate
  ```

Once activated, your terminal prompt will show a prefix like `(.venv)`.

---

### 3. Handling PowerShell Execution Policy Errors

If you run `.\.venv\Scripts\Activate.ps1` in PowerShell and receive an error stating:
> *"File ... cannot be loaded because running scripts is disabled on this system."*

Windows restricts script execution by default. Resolve it using one of these options:

#### Option A: Allow scripts for the current terminal session only (Recommended)
```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```
*Then re-run `.\.venv\Scripts\Activate.ps1`.*

#### Option B: Allow local scripts permanently for your user account
Open PowerShell and run:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

### 4. Installing Packages and Deactivating

With the environment activated:

1. **Install packages** safely without polluting system Python:
   ```cmd
   pip install requests pandas
   ```
2. **Save dependencies to a file**:
   ```cmd
   pip freeze > requirements.txt
   ```
3. **Deactivate the environment**:
   ```cmd
   deactivate
   ```

---

## Part 2: Modern Python & Environment Manager (`uv`)

[`uv`](https://docs.astral.sh/uv/) is a fast Python package installer and resolver written in Rust. It functions as a drop-in replacement for `pip`, `pip-tools`, `virtualenv`, and `pyenv`.

---

### 1. Install `uv` on Windows

Choose **one** of the following methods to install `uv`:

#### Method A: Official Standalone Installer via PowerShell (Recommended)
Open **PowerShell** and run:
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

#### Method B: Windows Package Manager (`winget`)
Open **Command Prompt** or **PowerShell** and run:
```cmd
winget install --id=astral-sh.uv -e
```

#### Method C: Via `pip` (If Python is already installed)
```cmd
pip install uv
```

---

### 2. Verify `uv` Installation

Restart your terminal window and verify that `uv` is available on your PATH:
```cmd
uv --version
```
**Expected Output:**
```text
uv 0.x.x (...)
```

If it reports that the command is not recognized after running Method A, verify that `C:\Users\<YourUsername>\.local\bin` or `C:\Users\<YourUsername>\AppData\Roaming\uv\bin` is added to your User `PATH` environment variable.

---

### 3. (Optional) Installing Python Versions via `uv`

`uv` can automatically download and configure standalone Python builds on Windows without using the standard installer:

```cmd
# List available Python releases
uv python list

# Install a specific version
uv python install 3.12

# Install the latest stable version
uv python install
```

---

### 4. Creating Environments with `uv venv`

You can use `uv` simply as an accelerated drop-in replacement for `python -m venv`:

1. Navigate to your project folder:
   ```cmd
   cd C:\Users\<YourUsername>\Desktop\my_project
   ```
2. Create an environment (created in milliseconds):
   ```cmd
   uv venv
   ```
   *(To use a specific Python version: `uv venv --python 3.12`)*
3. Activate it just like a regular virtual environment:
   - **PowerShell:** `.\.venv\Scripts\Activate.ps1`
   - **CMD:** `.venv\Scripts\activate.bat`
4. Install packages at high speed:
   ```cmd
   uv pip install requests fastapi uvicorn
   ```

---

### 5. Modern Project Workflow (Recommended)

`uv` includes a complete project management workflow that eliminates the need to manually activate virtual environments:

1. **Initialize a new project:**
   ```cmd
   uv init my-app
   cd my-app
   ```
   *This creates a project skeleton with `pyproject.toml` and `.python-version`.*

2. **Add dependencies:**
   ```cmd
   uv add requests httpx
   ```
   *`uv` automatically creates a virtual environment, resolves locks, and updates `pyproject.toml`.*

3. **Run your code inside the isolated environment:**
   ```cmd
   uv run main.py
   ```
   *`uv run` automatically ensures the virtual environment exists and is up to date before running the script.*

---

## Quick Command Cheatsheet

| Task | Built-in `venv` + `pip` | `uv` Project Workflow |
| :--- | :--- | :--- |
| **Create environment** | `python -m venv .venv` | `uv venv` |
| **Activate (PowerShell)** | `.\.venv\Scripts\Activate.ps1` | `.\.venv\Scripts\Activate.ps1` *(optional)* |
| **Activate (CMD)** | `.venv\Scripts\activate.bat` | `.venv\Scripts\activate.bat` *(optional)* |
| **Install package** | `pip install <pkg>` | `uv add <pkg>` or `uv pip install <pkg>` |
| **Run script** | `python script.py` | `uv run script.py` |
| **Export dependencies** | `pip freeze > requirements.txt` | `uv pip compile pyproject.toml` or `uv export` |
| **Exit environment** | `deactivate` | `deactivate` |