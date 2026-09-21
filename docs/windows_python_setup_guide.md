# Beginner's Guide: Installing and Running Python on Windows

This guide walks you step-by-step through downloading, installing, verifying, and executing your first Python program on a Windows machine.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Step 1: Download Python](#step-1-download-python)
3. [Step 2: Install Python](#step-2-install-python)
4. [Step 3: Verify the Installation](#step-3-verify-the-installation)
5. [Step 4: Write Your First Python Script](#step-4-write-your-first-python-script)
6. [Step 5: Run Your Script](#step-5-run-your-script)
7. [Alternative: Interactive Mode (REPL)](#alternative-interactive-mode-repl)
8. [Common Troubleshooting](#common-troubleshooting)

---

## Prerequisites
- A PC running **Windows 10** or **Windows 11** (64-bit recommended).
- An active internet connection.
- Administrator access on your machine.

---

## Step 1: Download Python

1. Open your web browser and visit the official Python download page:
   [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. The website should automatically detect your operating system and show a prominent button saying:
   **"Download Python 3.x.x"** (where `3.x.x` represents the latest stable release).
3. Click the button to download the Windows installer executable (`.exe`).

---

## Step 2: Install Python

1. Locate the downloaded `.exe` file (typically in your `Downloads` folder) and double-click it.
2. **CRITICAL STEP:** At the bottom of the installer window, ensure you check the box:
   > ☑ **Add python.exe to PATH**
   
   *(If you skip this, Windows will not recognize `python` commands in the terminal without manual configuration).*

3. Click **Install Now**.
4. If prompted by Windows User Account Control (UAC) asking for permission, select **Yes**.
5. Once installation finishes, you will see a screen titled *"Setup was successful"*.
6. *(Optional)* If you see a link that says **"Disable path length limit"**, click it to prevent issues with deep directory trees.
7. Click **Close**.

---

## Step 3: Verify the Installation

Confirm that Python and its package manager (`pip`) are correctly recognized by your system.

1. Press `Win + R` on your keyboard, type `cmd`, and press **Enter** (or search for **Command Prompt** / **PowerShell** in the Start menu).
2. Type the following command and press **Enter**:
   ```cmd
   python --version
   ```
   **Expected Output:**
   ```text
   Python 3.x.x
   ```
3. Next, check `pip`:
   ```cmd
   pip --version
   ```
   **Expected Output:**
   ```text
   pip 2x.x from ... (python 3.x)
   ```

If you see the version numbers, your installation is complete and properly configured.

---

## Step 4: Write Your First Python Script

Let's create a classic "Hello, World!" script.

1. Create a dedicated folder for your code (for example, on your Desktop: `C:\Users\<YourUsername>\Desktop\PythonProjects`).
2. Open a text editor such as **Notepad** (or a code editor like **Visual Studio Code**).
3. Type the following code into the editor:
   ```python
   # hello.py
   print("Hello, World!")
   
   name = input("What is your name? ")
   print(f"Welcome to Python programming, {name}!")
   ```
4. Save the file:
   - File name: `hello.py`
   - Save as type: **All Files (*.*)** (in Notepad, this ensures it doesn't save as `hello.py.txt`).
   - Location: inside your new project folder.

---

## Step 5: Run Your Script

1. Open **Command Prompt** or **PowerShell**.
2. Navigate to the folder containing your script using the `cd` (change directory) command:
   ```cmd
   cd Desktop\PythonProjects
   ```
3. Run the script by invoking Python followed by the file name:
   ```cmd
   python hello.py
   ```
4. You should see the program run in your terminal:
   ```text
   Hello, World!
   What is your name? Alex
   Welcome to Python programming, Alex!
   ```

---

## Alternative: Interactive Mode (REPL)

Python also features an interactive prompt where you can test code line by line.

1. Open **Command Prompt** and type:
   ```cmd
   python
   ```
2. The prompt will switch to triple arrows (`>>>`):
   ```python
   >>> 2 + 2
   4
   >>> print("Testing Python REPL")
   Testing Python REPL
   ```
3. To exit interactive mode, type `exit()` and press **Enter**, or press `Ctrl + Z` then **Enter**.

---

## Common Troubleshooting

### Issue 1: `'python' is not recognized as an internal or external command`
- **Cause:** The "Add python.exe to PATH" checkbox was missed during installation.
- **Fix:**
  1. Re-run the downloaded installer.
  2. Choose **Modify**.
  3. Ensure all features are checked, click **Next**, and make sure **Add Python to environment variables** is selected.
  4. Alternatively, search Windows for **"Edit the system environment variables"**, click **Environment Variables**, select `Path` under User variables, click **Edit**, and add the folder paths where Python was installed (e.g., `C:\Users\<User>\AppData\Local\Programs\Python\Python3x`).

### Issue 2: Windows opens the Microsoft Store when typing `python`
- **Cause:** Windows App Execution Aliases are redirecting you to install Python via the Windows Store.
- **Fix:**
  1. Open Windows **Settings** (`Win + I`).
  2. Go to **Apps** > **Advanced app settings** > **App execution aliases**.
  3. Toggle off **App Installer (python.exe)** and **App Installer (python3.exe)**.