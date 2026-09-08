# NSDM graph-tool environment (cmns-graphtool)

This guide installs a dedicated Conda environment for the notebooks that use **graph-tool**.

Why a separate environment? `graph-tool` is a compiled C++ library with many dependencies, and it’s easiest when it’s isolated from other heavy stacks.

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
conda activate cmns-graphtool
```

---

## 3) Windows note (important)

`graph-tool` does **not** provide native Windows builds. The most reliable path is **WSL2 + Ubuntu** (or Docker). The graph-tool installation docs explicitly recommend WSL on Windows.

### WSL2 quick start (PowerShell as Administrator)

```powershell
wsl --install
```

Reboot if prompted, then open Ubuntu and repeat the Linux/macOS steps above *inside WSL*.

---

## 4) Register as a Jupyter kernel

```bash
conda activate cmns-graphtool
python -m ipykernel install --user --name cmns-graphtool --display-name "Python (cmns-graphtool / graph-tool)"
```

---

## 5) Verify the install

```bash
conda activate cmns-graphtool
python -c "import graph_tool.all as gt; import networkx as nx; print('graph-tool OK')"
```

Jupyter smoke test (paste into a notebook cell):

```python
import graph_tool.all as gt
import networkx as nx
import numpy as np

print("graph-tool:", gt.__version__)
print("networkx:", nx.__version__)
print("numpy:", np.__version__)
```

---

## 6) Launch JupyterLab

```bash
conda activate cmns-graphtool
jupyter lab
```

Kernel: **Python (cmns-graphtool / graph-tool)**

---

## 7) Which notebooks use this environment?

- `class_09_communities2_v3.ipynb`
- `class_10_communities3.ipynb`

---

## 8) Updating / removing the environment

Update:

```bash
conda activate cmns-graphtool
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-graphtool
```

---

## 9) Troubleshooting

1) **ImportError: `graph_tool` fails to import.**  
   Confirm you’re in the environment:

   ```bash
   conda activate cmns-graphtool
   which python
   python -c "import graph_tool.all as gt; print(gt.__version__)"
   ```

2) **Windows: you tried to install graph-tool in native Anaconda Prompt.**  
   Use WSL2 (recommended) or Docker instead.

3) **Solver conflicts / stalls.**  
   Enforce strict conda-forge and try `mamba`:

   ```bash
   conda config --set channel_priority strict
   conda install -n base -c conda-forge mamba
   ```

4) **Jupyter shows the wrong kernel.**  
   Re-register the kernel after activation:

   ```bash
   conda activate cmns-graphtool
   python -m ipykernel install --user --name cmns-graphtool --display-name "Python (cmns-graphtool / graph-tool)"
   ```

5) **Last resort: Docker**  
   There is an official Docker image you can use when local installs fail:

   ```bash
   docker pull tiagopeixoto/graph-tool
   ```
