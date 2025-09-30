Starting a new Python project, especially using **uv** for dependency management and virtual environments, involves several best practices.

## 🐍 Core Steps and Best Practices with uv

Here's a breakdown of the best practices and typical workflow:

### 1\. Project Setup and Virtual Environment

The first and most critical step is isolating your project's dependencies using a **virtual environment**. `uv` excels at this, providing a fast alternative to `venv` or `conda`.

  * **Create the Project Directory:**
    ```bash
    mkdir my_new_project
    cd my_new_project
    ```
  * **Create and Activate the Virtual Environment:**
    Instead of creating the environment and *then* activating it, a modern approach is to let `uv` handle the creation and then rely on tools (like your shell integration or IDE) to use the environment when you're in that directory. However, to explicitly activate it:
    ```bash
    # 1. Create the virtual environment (named .venv is standard)
    uv venv
    # 2. Activate the virtual environment
    source .venv/bin/activate  # On Linux/macOS
    # .venv\Scripts\activate  # On Windows (Command Prompt)
    ```
      * **Best Practice:** Use the standard name **`.venv`** for your environment. This is recognized by most IDEs (like VS Code, PyCharm) and is universally added to **`.gitignore`**.

### 2\. Dependency Management

Use a standard, modern, and easily readable format for declaring your dependencies. The **`pyproject.toml`** file is the current Python standard for project metadata and configuration.

  * **Initialize `pyproject.toml`:**
    You can create this file manually or use a tool.

    ```toml
    # pyproject.toml
    [project]
    name = "my_new_project"
    version = "0.1.0"
    description = "A brief description of my project"
    authors = [
        {name = "Your Name", email = "you@example.com"},
    ]
    requires-python = ">=3.9" # Set your required Python version

    dependencies = [
        # Add your core dependencies here
        # e.g., "requests", "pydantic"
    ]

    [build-system]
    requires = ["setuptools>=61.0.0"]
    build-backend = "setuptools.build_meta"
    ```

      * **Best Practice:** Always specify the **`requires-python`** version to ensure environment compatibility.

  * **Install Dependencies with uv:**
    You can install dependencies directly from the command line, and `uv` will automatically add them to `pyproject.toml` (if you use the `--save` flag, which is good practice).

    ```bash
    # Install a dependency and update pyproject.toml (if using uv as a wrapper around pip-like commands)
    # If using just uv, you typically manage the toml file and let uv sync to it.

    # Standard installation (requires dependencies to be in pyproject.toml or a requirements file)
    uv sync

    # Or, to add a new package:
    # uv add requests  # (This feature is in active development/may be implemented by the time you read this)
    # For now, manually add to pyproject.toml and run:
    uv sync 
    ```

### 3\. Pinning Dependencies (Lock File)

For reproducible builds, you need a **lock file** that specifies the exact version and hash of *every* package (including transitive dependencies). `uv` manages this with the **`uv.lock`** file.

  * **Generate the Lock File:**
    ```bash
    uv lock
    ```
      * **Best Practice:** Commit the generated **`uv.lock`** file to version control (e.g., Git). This ensures that anyone who runs your project (or your CI/CD pipeline) installs the *exact same* set of dependencies.

### 4\. Version Control and Ignoring Files

Use Git for version control from day one.

  * **Initialize Git:**

    ```bash
    git init
    ```

  * **Create a `.gitignore`:**
    Essential items to ignore are the virtual environment and compiled Python files.

    ```gitignore
    # .gitignore

    # Virtual Environment
    .venv/
    # If you use venv/ instead of .venv/
    # venv/ 

    # Byte-compiled files
    __pycache__/
    *.pyc

    # Editor/OS temporary files
    .DS_Store

    # uv's lock file (if you choose to regenerate it often, though committing it is recommended for reproducibility)
    # If you choose NOT to commit it, uncomment the line below.
    # uv.lock
    ```

      * **Best Practice:** Always **exclude the virtual environment folder (`.venv/`)** from your version control.

### 5\. Project Structure

A clean, standard project structure makes maintenance and testing easier.

```
my_new_project/
├── .venv/                     # 👈 Virtual environment (ignored by Git)
├── .gitignore                 # 👈 Version control ignores
├── pyproject.toml             # 👈 Project metadata and dependency declaration
├── uv.lock                    # 👈 Pinned, reproducible dependencies (committed to Git)
├── README.md                  # 👈 Documentation for project setup and usage
├── src/                       # 👈 Recommended for your actual package code
│   └── my_new_project/        # 👈 The actual Python package directory
│       ├── __init__.py
│       └── core.py            # 👈 Your main code files
└── tests/                     # 👈 Unit and integration tests
    └── test_core.py
```

  * **Best Practice:** Adopt the **`src` layout** (`src/your_package_name/...`). This clearly separates your source code from other files (like tests, docs, config) and prevents import confusion (where you accidentally import the project directory instead of the installed package).

-----

## ✨ Summary Checklist

| Best Practice | Description | Command/File |
| :--- | :--- | :--- |
| **Isolation** | Use a virtual environment (named `.venv`). | `uv venv` |
| **Declaration** | Use `pyproject.toml` to list all direct dependencies. | `pyproject.toml` |
| **Reproducibility** | Generate and commit a lock file to pin dependencies. | `uv lock` |
| **Version Control** | Initialize Git and ignore the virtual environment. | `.gitignore` |
| **Structure** | Use the **`src` layout** for clear code organization. | `src/your_package_name/` |
| **Documentation** | Always start with a `README.md`. | `README.md` |