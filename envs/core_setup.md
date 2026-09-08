# NSDM Core environment (nsdm-core)

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
conda activate nsdm-core
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
conda activate nsdm-core
python -m ipykernel install --user --name nsdm-core --display-name "Python (nsdm-core)"
```

Check that it worked:

```bash
jupyter kernelspec list
```

---

## 4) Verification (quick smoke tests)

### 4.1 Command-line import test

```bash
conda activate nsdm-core
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
conda activate nsdm-core
jupyter lab
```

In JupyterLab: **Kernel → Change Kernel → Python (nsdm-core)**.

---

## 6) Which notebooks use this environment?

- `class_01_python_refresher_v2.ipynb`
- `class_02_networkx1_v2.ipynb`
- `class_03_networkx2_v2.ipynb`
- `class_04_distributions_v5.ipynb`
- `class_11_homophily_v4.ipynb`
- `class_12_visualization_python_v3.ipynb`
- `class_16_dynamics1_v4.ipynb`
- `class_17_dynamics2_v3.ipynb`
- `class_18_dynamics3_v3.ipynb`
- `class_19_graphdistances_v2.ipynb`
- `class_20_temporal_networks_v3.ipynb`
- `class_21_sparsification_v3.ipynb`
- `class_22_sampling_v5.ipynb`
- `class_23_linkprediction_v3.ipynb`
- `class_25_spectral_v2.ipynb`
- `class_27_network_reconstruction_v4.ipynb`
- `class_31_causal_inference_networks_v3.ipynb`
- `class_32_stats_v3.ipynb`
- `class_33_geometry_v3.ipynb`
- `class_34_information_theory_networks_v3.ipynb`
- `class_35_complex_contagion_v4.ipynb`
- `class_39_temporal_community_detection_v3.ipynb`
- `class_40_motifs_v4.ipynb`
- `class_41_signed_networks_v4.ipynb`
- `class_42_coarse_graining_v3.ipynb`
- `class_44_network_growth_models_v3.ipynb`
- `class_45_ranking_in_networks_v3.ipynb`
- `class_46_network_rewiring_dynamics_v3.ipynb`
- `class_48_games_on_networks_v3.ipynb`
- `class_49_hierarchical_v3.ipynb`
- `class_50_visibility_graphs_v2.ipynb`
- `class_51_paths_v3.ipynb`
- `class_52_robustness_resilience_v2.ipynb`
- `class_53_dynamics4_v3.ipynb`
- `class_54_graph_curvature_v2.ipynb`
- `class_55_ergm_v2.ipynb`
- `class_56_neuronal_dynamics_v1.ipynb`
- `class_63_sql_to_networks_v3.ipynb`
- `class_69_bigdata_v4.ipynb`

---

## 7) Updating / removing the environment

Update (apply changes if `environment.yml` changes):

```bash
conda activate nsdm-core
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n nsdm-core
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
   conda activate nsdm-core
   python -m ipykernel install --user --name nsdm-core --display-name "Python (nsdm-core)"
   ```

7) **Still stuck? Collect diagnostics before asking for help.**

   ```bash
   conda info
   conda list
   python -c "import sys; print(sys.version); print(sys.executable)"
   ```
