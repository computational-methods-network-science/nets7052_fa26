# NSDM Machine Learning environment (cmns-ml)

This guide installs a CPU-first environment for ML notebooks using **PyTorch** (plus scikit-learn).

We intentionally install **CPU builds by default**. GPU support is optional and varies by hardware/driver.

---

## 0) Install a Conda distribution

Recommended: **Miniforge** (conda-forge first).

Verify:

```bash
conda --version
```

Optional (recommended): install `mamba`:

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
conda activate cmns-ml
```

---

## 3) Register as a Jupyter kernel

```bash
conda activate cmns-ml
python -m ipykernel install --user --name cmns-ml --display-name "Python (cmns-ml / PyTorch CPU)"
```

---

## 4) Verify the install

```bash
conda activate cmns-ml
python -c "import torch; import sklearn; print(torch.__version__); print('cuda available:', torch.cuda.is_available())"
```

Jupyter smoke test:

```python
import torch
import sklearn
import numpy as np

print("torch:", torch.__version__)
print("cuda available:", torch.cuda.is_available())
print("sklearn:", sklearn.__version__)
print("numpy:", np.__version__)
```

On CPU installs, `cuda available` should usually be `False`.

---

## 5) Optional: PyTorch Geometric (torch_geometric)

Two notebooks import `torch_geometric`, but they are written to **skip PyG-only sections** if it isn’t installed.

If you want to run the PyG sections, install it **after** PyTorch is working:

```bash
conda activate cmns-ml
python -m pip install torch-geometric
```

If that fails (common), follow the official PyTorch Geometric install instructions for your exact PyTorch + OS combo (it may require installing `torch-scatter`, `torch-sparse`, etc.).

---

## 6) Launch JupyterLab

```bash
conda activate cmns-ml
jupyter lab
```

Kernel: **Python (cmns-ml / PyTorch CPU)**

---

## 7) Which notebooks use this environment?

- `class_26_embedding_v3.ipynb`
- `class_64_machine_learning_1_v3.ipynb`
- `class_65_graph_machine_learning_2_v4.ipynb`

---

## 8) Optional: GPU notes (do not do this unless you know you want it)

GPU-enabled installs depend on your GPU (NVIDIA vs Apple vs AMD), drivers, and the specific PyTorch build.
If you need GPU support, use the official PyTorch “Start Locally” / “Previous Versions” instructions to generate the right install command for your system, then **re-register the Jupyter kernel** afterward.

---

## 9) Updating / removing the environment

Update:

```bash
conda activate cmns-ml
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-ml
```

---

## 10) Troubleshooting

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

4) **Torch-geometric install errors.**  
   This is common. Treat PyG as optional unless your assignment explicitly requires it.

5) **Solver conflicts.**  
   Stick to strict conda-forge and use `mamba`.

6) **Still stuck? Collect diagnostics:**

   ```bash
   conda info
   conda list
   python -c "import sys; print(sys.executable)"
   ```
