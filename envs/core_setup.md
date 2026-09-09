# Core environment (cmns-core)

This guide installs the **core Python environment** for the Network Science notebooks: scientific Python, NetworkX, plotting, plus a handful of extra libraries that show up in the “core” notebooks (stats/temporal networks/big-data I/O/visualization).

## What is Conda (and why are we using it)?

Conda is a tool for creating isolated Python environments (separate “software bubbles”) so packages don’t conflict with each other.  
In this course we use Conda because many scientific libraries include compiled code, and Conda can install pre-built binaries reliably.

---

## 0) Install a Conda distribution

Recommended: **Miniforge** (Conda pre-configured to use `conda-forge`, which has the best scientific Python coverage).

After installing, open a new terminal and verify:

```bash
conda --version
```

Optional (recommended): install `mamba` (a faster solver):

```bash
conda install -n base -c conda-forge mamba
```

---

## 1) Configure conda-forge (recommended)

Run once:

```bash
conda config --add channels conda-forge
conda config --set channel_priority strict
```

---

## 2) Create the environment

From the folder that contains `environment.yml`:

```bash
mamba env create -f environment.yml
conda activate cmns-core
```

If you don’t have `mamba`, replace the first command with:

```bash
conda env create -f environment.yml
```

### macOS note (Intel vs Apple Silicon)

Check your CPU architecture:

```bash
uname -m
```

- `arm64` = Apple Silicon (M1/M2/M3…)
- `x86_64` = Intel (or Rosetta)

Be consistent: mixing `arm64` and `x86_64` environments is a common source of installation pain.

---

## 3) Register as a Jupyter kernel (non-negotiable)

```bash
conda activate cmns-core
python -m ipykernel install --user --name cmns-core --display-name "Python (cmns-core)"
```

Check that it worked:

```bash
jupyter kernelspec list
```

---

## 4) Verification (quick smoke tests)

### 4.1 Command-line import test

```bash
conda activate cmns-core
python -c "import networkx as nx, numpy as np, pandas as pd; import sklearn; import statsmodels; print('core imports OK')"
```

### 4.2 Jupyter smoke test (paste into a notebook cell)

```python
import sys
import numpy as np
import pandas as pd
import networkx as nx
import matplotlib
import sklearn
import statsmodels

print("python:", sys.version.split()[0])
print("numpy:", np.__version__)
print("pandas:", pd.__version__)
print("networkx:", nx.__version__)
print("matplotlib:", matplotlib.__version__)
print("sklearn:", sklearn.__version__)
print("statsmodels:", statsmodels.__version__)
```

---

## 5) Launch JupyterLab

```bash
conda activate cmns-core
jupyter lab
```

In JupyterLab: **Kernel → Change Kernel → Python (cmns-core)**.

---

## Which classes use this environment?

Most of them. The exceptions are Classes 7 and 8 (community detection), 12 and 13 (machine learning), and 22 (spatial), which need the heavier environments under `envs/`. The schedule in the [README](../README.md) says which is which.

## 7) Updating / removing the environment

Update (apply changes if `environment.yml` changes):

```bash
conda activate cmns-core
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-core
```

---

## 8) Troubleshooting (common fixes)

1) **“I installed packages but Jupyter can’t import them.”**  
   You’re probably running the wrong kernel. Check:

   ```bash
   which python
   python -c "import sys; print(sys.executable)"
   jupyter kernelspec list
   ```

2) **Solver takes forever / gets stuck.**  
   Use `mamba`, and keep channels clean:

   ```bash
   conda install -n base -c conda-forge mamba
   conda config --set channel_priority strict
   ```

3) **Mixing `defaults` and `conda-forge` caused conflicts.**  
   Confirm your config:

   ```bash
   conda config --show channels
   conda config --show channel_priority
   ```

4) **macOS: architecture mismatch (Intel vs Apple Silicon).**  
   Recreate the environment in a terminal that matches your CPU architecture.

5) **Pip installed into the wrong place.**  
   Always use pip through the environment’s Python:

   ```bash
   python -m pip -V
   python -m pip install <package>
   ```

6) **Kernel registration permission errors.**  
   Make sure you used `--user`, and try again after activating the env:

   ```bash
   conda activate cmns-core
   python -m ipykernel install --user --name cmns-core --display-name "Python (cmns-core)"
   ```

7) **Still stuck? Collect diagnostics before asking for help.**

   ```bash
   conda info
   conda list
   python -c "import sys; print(sys.version); print(sys.executable)"
   ```
