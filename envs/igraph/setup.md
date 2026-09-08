# NSDM igraph environment (cmns-igraph)

This guide installs a dedicated environment for notebooks that use **python-igraph** (plus Leiden community detection, and Plotly-based plotting).

---

## 0) Install a Conda distribution

Recommended: **Miniforge** (conda-forge first).

Verify:

```bash
conda --version
```

Optional (recommended): faster installs with `mamba`:

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
conda activate cmns-igraph
```

---

## 3) Register as a Jupyter kernel

```bash
conda activate cmns-igraph
python -m ipykernel install --user --name cmns-igraph --display-name "Python (cmns-igraph / igraph)"
```

---

## 4) Verify the install

```bash
conda activate cmns-igraph
python -c "import igraph as ig; import leidenalg; import plotly; print('igraph OK')"
```

Jupyter smoke test:

```python
import igraph as ig
import leidenalg
import plotly
import numpy as np

print("igraph:", ig.__version__)
print("leidenalg:", leidenalg.__version__)
print("plotly:", plotly.__version__)
print("numpy:", np.__version__)
```

---

## 5) Launch JupyterLab

```bash
conda activate cmns-igraph
jupyter lab
```

Kernel: **Python (cmns-igraph / igraph)**

---

## 6) Which notebooks use this environment?

- `class_08_communities1_v2.ipynb`
- `class_30_igraph_v3.ipynb`

---

## 7) Updating / removing the environment

Update:

```bash
conda activate cmns-igraph
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-igraph
```

---

## 8) Troubleshooting

1) **ImportError: `igraph` fails to import.**  
   Check you’re in the right environment and you’re not mixing channels:

   ```bash
   conda activate cmns-igraph
   conda list | grep igraph
   python -c "import igraph; print(igraph.__version__)"
   ```

2) **Plotly figures not showing in Jupyter.**  
   Restart the kernel, and ensure you launched Jupyter from the same environment.

3) **Kernel confusion (“it runs in terminal but not in Jupyter”).**  
   Re-register the kernel:

   ```bash
   conda activate cmns-igraph
   python -m ipykernel install --user --name cmns-igraph --display-name "Python (cmns-igraph / igraph)"
   ```

4) **macOS: Intel/Rosetta mismatch.**  
   Verify `uname -m` and recreate the env in the correct shell.

5) **Solver conflicts.**  
   Use strict conda-forge + mamba:

   ```bash
   conda config --set channel_priority strict
   conda install -n base -c conda-forge mamba
   ```
