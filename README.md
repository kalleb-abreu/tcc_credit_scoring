# Getting Started with `renv`

`renv` is a dependency management toolkit for R (similar to `venv` and `pip freeze` in Python). It ensures that your project uses its own private library of packages, rather than the global system library.

### 1. Initialize the Project

Open your terminal and start R. Then, run the initialization command to set up the project structure.

```r
R
renv::init()
```

> **What this does:** creates a `renv/` folder, a `.Rprofile`, and a `renv.lock` file. It isolates this project from your other R projects.

### 2. Activate the Environment

Restart your terminal or R session to ensure the environment is loaded correctly. If R does not automatically detect the project, you can force activation:

```r
# Restart your terminal/shell first, then launch R
source("renv/activate.R")
```

> **What this does:** runs the startup script that tells R to look _only_ in this project's folder for packages.

### 3. Install Packages

Install packages as you normally would. They will now be installed into the project's private library.

```r
install.packages("dplyr")
```

### 4. Save the State

Once your code is working, save the exact versions of the packages you are using into the lockfile.

```r
renv::snapshot()
```

> **Note:** By default, `renv` only saves packages that are actually mentioned in your scripts (e.g., `library(dplyr)`). If you want to force save everything installed, use `renv::snapshot(type="all")`.

### 5. Restore

When a teammate clones this repository (or you move to a new machine), they run this single command to install everything exactly as you had it:

```r
renv::restore()
```

> **What this does:** downloads and installs the exact package versions listed in `renv.lock`.

---

### Summary of Files

- 📄 **`renv.lock`**: The list of packages and versions (Keep in Git).
- 📄 **`.Rprofile`**: The auto-loader script (Keep in Git).
- 📂 **`renv/library`**: The actual installed package files (Ignore in Git).
