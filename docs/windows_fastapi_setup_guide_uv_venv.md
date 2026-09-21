# Windows Guide: Building and Running FastAPI with `venv` and `uv`

This guide walks you through setting up, developing, and running a **FastAPI** web application on Windows. It covers two approaches:
1. **The Modern `uv` Workflow** (Recommended: ultra-fast, zero-friction dependency management)
2. **The Classic `venv` + `pip` Workflow** (Built-in standard library approach)

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [A Minimal FastAPI Application (`main.py`)](#a-minimal-fastapi-application-mainpy)
3. [Method 1: Fast & Modern Setup with `uv` (Recommended)](#method-1-fast--modern-setup-with-uv-recommended)
   * [Workflow A: Project Management (`uv init`, `uv add`, `uv run`)](#workflow-a-uv-project-workflow-recommended)
   * [Workflow B: Drop-in Virtual Environment (`uv venv` + `uv pip`)](#workflow-b-uv-venv--uv-pip-workflow)
4. [Method 2: Standard Setup with Built-in `venv` and `pip`](#method-2-standard-setup-with-built-in-venv-and-pip)
5. [Verifying & Interacting with Your API](#verifying--interacting-with-your-api)
   * [Interactive Swagger Docs (`/docs`)](#1-interactive-api-documentation-swagger-ui)
   * [Alternative Documentation (`/redoc`)](#2-alternative-documentation-redoc)
6. [Expanding the API: Adding Routes & Data Models](#expanding-the-api-adding-routes--data-models)
7. [Common Windows Pitfalls & Troubleshooting](#common-windows-pitfalls--troubleshooting)

---

## Prerequisites

Before starting, ensure you have:
* A Windows 10 or 11 machine.
* Python 3.8+ installed (or `uv` installed, which can download Python for you).
* A terminal of choice: **PowerShell**, **Command Prompt (CMD)**, or **Windows Terminal**.

---

## A Minimal FastAPI Application (`main.py`)

Regardless of which environment manager you choose, here is the boilerplate application code used throughout this guide.

Create a file named `main.py`:

```python
from fastapi import FastAPI

app = FastAPI(title="FastAPI Windows Demo")

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI on Windows!"}

@app.get("/items/{item_id}")
def read_item(item_id: int, query: str | None = None):
    return {"item_id": item_id, "query": query}
```

---

## Method 1: Fast & Modern Setup with `uv` (Recommended)

[`uv`](https://docs.astral.sh/uv/) handles environment creation, dependency resolution, and running applications in milliseconds without manual environment activation.

### Installing `uv` (If not already installed)

Open **PowerShell** and run:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Restart your terminal window and verify:

```powershell
uv --version
```

---

### Workflow A: `uv` Project Workflow (Recommended)

This workflow lets `uv` handle lockfiles (`uv.lock`), project configuration (`pyproject.toml`), and environment syncing automatically.

#### 1. Initialize the Project

```powershell
# Create project folder and scaffold
uv init fastapi-demo
cd fastapi-demo
```

*(Optional: If you need a specific Python version, run `uv python pin 3.12`)*

#### 2. Add FastAPI and the Standard Dependencies

FastAPI provides a CLI and standard ASGI server bundle via `fastapi[standard]`:

```powershell
uv add "fastapi[standard]"
```

`uv` resolves the dependencies in seconds, locks them into `uv.lock`, and prepares an internal virtual environment under `.venv`.

#### 3. Create or Edit `main.py`

Replace the contents of `main.py` in your project folder with the boilerplate code provided above.

#### 4. Run the Application

Execute your server without needing to manually activate the virtual environment:

```powershell
uv run fastapi dev main.py
```

*Alternative (direct Uvicorn invocation):*

```powershell
uv run uvicorn main:app --reload --port 8000
```

---

### Workflow B: `uv venv` + `uv pip` Workflow

If you prefer standard manual environment activation but want `uv`'s speed:

#### 1. Create a Project Directory & Virtual Environment

```powershell
mkdir fastapi-classic-uv
cd fastapi-classic-uv

# Create virtual environment in .venv
uv venv
```

#### 2. Activate the Environment

* **PowerShell:**
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```
* **Command Prompt (CMD):**
  ```cmd
  .venv\Scripts\activate.bat
  ```

#### 3. Install FastAPI with `uv pip`

```powershell
uv pip install "fastapi[standard]"
```

#### 4. Run the Application

```powershell
fastapi dev main.py
```
*(or: `uvicorn main:app --reload`)*

---

## Method 2: Standard Setup with Built-in `venv` and `pip`

Use this method if you cannot install external binaries and want to rely solely on Python's built-in tools.

### 1. Create a Project Folder

```powershell
mkdir fastapi-standard
cd fastapi-standard
```

### 2. Create the Virtual Environment

```powershell
python -m venv .venv
```

### 3. Activate the Virtual Environment

* **PowerShell:**
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```
* **Command Prompt (CMD):**
  ```cmd
  .venv\Scripts\activate.bat
  ```
* **Git Bash:**
  ```bash
  source .venv/Scripts/activate
  ```

> **Note for PowerShell Users:** If you see an error saying `running scripts is disabled on this system`, run:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
> ```
> Then run `.\.venv\Scripts\Activate.ps1` again.

Once activated, your terminal prompt will show a `(.venv)` prefix.

### 4. Upgrade `pip` and Install FastAPI

```powershell
python -m pip install --upgrade pip
pip install "fastapi[standard]"
```

### 5. Add `main.py` and Run

Create your `main.py` file, then launch the development server:

```powershell
fastapi dev main.py
```

*(or: `uvicorn main:app --reload --host 127.0.0.1 --port 8000`)*

### 6. Deactivating the Environment

When finished working, deactivate the environment by simply typing:

```powershell
deactivate
```

---

## Verifying & Interacting with Your API

Once your server is running, you will see terminal output similar to:

```text
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [...]
INFO:     Started server process [...]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

### 1. Root Endpoint

Open your browser and navigate to:
[http://127.0.0.1:8000/](http://127.0.0.1:8000/)

You will receive the JSON response:
```json
{
  "message": "Hello from FastAPI on Windows!"
}
```

### 2. Interactive API Documentation (Swagger UI)

FastAPI automatically generates interactive OpenAPI documentation. Visit:
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

* You can inspect all available routes (`GET /`, `GET /items/{item_id}`).
* Click **"Try it out"**, fill in parameters, and click **"Execute"** to test your endpoints directly from your browser.

### 3. Alternative Documentation (ReDoc)

Visit:
[http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## Expanding the API: Adding Routes & Data Models

FastAPI uses Python type hints and **Pydantic** to validate incoming JSON payloads. Here is an expanded `main.py` demonstrating a `POST` route:

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel, Field

app = FastAPI(title="Task Management API")

class Task(BaseModel):
    title: str = Field(..., example="Complete documentation")
    description: str | None = Field(None, example="Write Windows setup guides")
    completed: bool = False

# In-memory storage for demonstration
database: dict[int, Task] = {}

@app.get("/")
def home():
    return {"status": "online", "total_tasks": len(database)}

@app.post("/tasks/{task_id}", status_code=201)
def create_task(task_id: int, task: Task):
    if task_id in database:
        raise HTTPException(status_code=400, detail="Task already exists.")
    database[task_id] = task
    return {"message": "Task created successfully", "task": task}

@app.get("/tasks/{task_id}")
def get_task(task_id: int):
    if task_id not in database:
        raise HTTPException(status_code=404, detail="Task not found.")
    return database[task_id]
```

Because auto-reload is active (`--reload` or `fastapi dev`), saving `main.py` will automatically restart the server. Refresh `/docs` to inspect your new endpoints.

---

## Common Windows Pitfalls & Troubleshooting

### 1. `running scripts is disabled on this system` (PowerShell)
* **Cause:** Default Windows PowerShell security configuration blocks execution of unsigned scripts like `Activate.ps1`.
* **Fix:** In your PowerShell terminal, run:
  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
  ```

### 2. `error: [Errno 10048] error while attempting to bind on address ('127.0.0.1', 8000)`
* **Cause:** Another process or a previous instance of Uvicorn is already using port 8000.
* **Fix:** Either run on a different port:
  ```powershell
  uv run fastapi dev main.py --port 8001
  ```
  Or find and terminate the process holding port 8000 in PowerShell:
  ```powershell
  Get-Process -Id (Get-NetTCPConnection -LocalPort 8000).OwningProcess | Stop-Process -Force
  ```

### 3. Windows Defender Firewall Prompt
* When you run `uvicorn` or `fastapi dev` for the first time, Windows Firewall may ask to allow Python to communicate across networks.
* **Fix:** Ensure access is checked for **Private networks** (such as your home or work network) and select **Allow access**.

### 4. `'fastapi' or 'uvicorn' is not recognized`
* **Cause:** The virtual environment is either not activated, or the package was installed globally without scripts being on the Windows `PATH`.
* **Fix:** 
  * If using `venv`: Make sure you run `.\.venv\Scripts\Activate.ps1` before executing commands.
  * If using `uv`: Use `uv run fastapi dev main.py` so `uv` automatically executes inside the project environment.