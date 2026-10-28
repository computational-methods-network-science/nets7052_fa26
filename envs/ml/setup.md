# Machine Learning environment (cmns-ml)

This environment is for Classes 15 and 16, Machine Learning 1 and 2. On top of the usual scientific Python packages it has **PyTorch**, **PyTorch Geometric** and **gensim**, plus OSMnx, GeoPandas and contextily for the street-network example in Class 16.

PyTorch is installed as a **CPU build** on purpose. The class examples are small enough to train on a CPU, and a CPU build installs the same way on every machine.

---

## On the course cluster (Explorer)

You don't need to install anything. The environment is already built at `/courses/NETS7052.202710/shared/cmns-ml`. You connect it to JupyterLab once, the same way you connected `cmns-graphtool` in Class 8:

1. In [Open OnDemand](https://ood.explorer.northeastern.edu/), open the **Courses** menu, click **JupyterLab (Python)**, and launch it with your usual settings. Leave **Custom Anaconda Environment** blank.
2. Open a terminal (**File → New → Terminal**) and run this single line, exactly as written:
   ```bash
   /courses/NETS7052.202710/shared/cmns-ml/bin/python -m ipykernel install --user --name cmns-ml --display-name "Python (cmns-ml)"
   ```
3. Reload the browser tab. Open your copy of the notebook and choose **Kernel → Change Kernel…** → **Python (cmns-ml)**.
4. Check it in a notebook cell:
   ```python
   import sys, torch, torch_geometric
   print(sys.executable)
   print("torch", torch.__version__, "| PyG", torch_geometric.__version__)
   ```
   The first line should start with `/courses/NETS7052.202710/shared/cmns-ml/`.

**If it doesn't work:**

- *Python (cmns-ml) isn't in the kernel list.* Reload the browser tab. JupyterLab only reads the list of kernels when the page loads.
- *An import fails with a message about NumPy 1.x and 2.x, or `sys.executable` starts with `/shared/EL9/`.* The notebook is running on the cluster's own Python, not this environment. Run `cat ~/.local/share/jupyter/kernels/cmns-ml/kernel.json` in the terminal: the first path in `argv` should be the one from step 2. If it isn't, run step 2 again, then restart the kernel (**Kernel → Restart Kernel**). Switching kernels isn't enough, because the old process keeps running under the same name.
- *`torch.cuda.is_available()` prints `False`.* That's expected. This is a CPU build, even if your session is on the `courses-gpu` partition.

### Building the shared environment (instructor)

Once per semester. Run this in a terminal inside an OOD JupyterLab session, so that it runs on a compute node rather than the login node, from the top of your clone of this repository:

```bash
source /shared/EL9/explorer/anaconda3/2024.06/etc/profile.d/conda.sh
conda env create -p /courses/NETS7052.202710/shared/cmns-ml -f envs/ml/environment.yml
chmod -R o+rX /courses/NETS7052.202710/shared/cmns-ml
```

Use the `conda.sh` line, not `source activate`. On Explorer, `source activate` changes the prompt without changing which Python runs. When the build finishes, register the kernel for yourself with step 2 above.

---

## On your own computer

### 0) Install a Conda distribution

Recommended: **Miniforge** (conda-forge first).

Verify:

```bash
conda --version
```

Optional (recommended): install `mamba`:

```bash
conda install -n base -c conda-forge mamba
```

### 1) Configure conda-forge (recommended)

Run once:

```bash
conda config --add channels conda-forge
conda config --set channel_priority strict
```

### 2) Create the environment

From the folder that contains `environment.yml`:

```bash
mamba env create -f environment.yml
conda activate cmns-ml
```

### 3) Register as a Jupyter kernel

```bash
conda activate cmns-ml
python -m ipykernel install --user --name cmns-ml --display-name "Python (cmns-ml)"
```

### 4) Verify the install

```bash
conda activate cmns-ml
python -c "import torch, torch_geometric, sklearn, gensim; print(torch.__version__); print('cuda available:', torch.cuda.is_available())"
```

Jupyter smoke test:

```python
import torch
import torch_geometric
import sklearn
import numpy as np

print("torch:", torch.__version__)
print("torch_geometric:", torch_geometric.__version__)
print("cuda available:", torch.cuda.is_available())
print("sklearn:", sklearn.__version__)
print("numpy:", np.__version__)
```

On CPU installs, `cuda available` should be `False`.

### 5) Launch JupyterLab

```bash
conda activate cmns-ml
jupyter lab
```

Kernel: **Python (cmns-ml)**

### 6) Optional: GPU notes (do not do this unless you know you want it)

GPU-enabled installs depend on your GPU (NVIDIA vs Apple vs AMD), drivers, and the specific PyTorch build.
If you need GPU support, use the official PyTorch “Start Locally” / “Previous Versions” instructions to generate the right install command for your system, then **re-register the Jupyter kernel** afterward. PyTorch Geometric and `pyg-lib` have to match the PyTorch build, so reinstall them too.

### 7) Updating / removing the environment

Update:

```bash
conda activate cmns-ml
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-ml
```

### 8) Troubleshooting

1) **Kernel mismatch.**  
   If imports work in terminal but fail in Jupyter, you selected the wrong kernel.

2) **You accidentally installed GPU torch into a CPU env (or vice-versa).**  
   Check what you have:

   ```bash
   conda activate cmns-ml
   python -c "import torch; print(torch.__version__); print(torch.cuda.is_available())"
   conda list | grep -i torch
   ```

3) **Pip installed into the wrong environment.**  
   Always use:

   ```bash
   python -m pip install <package>
   ```

4) **`Node2Vec` says it requires `pyg-lib`, or `NeighborLoader` says it requires `pyg-lib` or `torch-sparse`.**  
   `pyg-lib` is missing or doesn't match your PyTorch. Install them together from conda-forge so they match: `mamba install -c conda-forge pytorch-cpu pytorch_geometric pyg-lib`.

5) **Solver conflicts.**  
   Stick to strict conda-forge and use `mamba`.

6) **Still stuck? Collect diagnostics:**

   ```bash
   conda info
   conda list
   python -c "import sys; print(sys.executable)"
   ```
