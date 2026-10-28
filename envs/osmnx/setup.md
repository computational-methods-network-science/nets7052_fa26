# OSMnx / Geospatial environment (cmns-osmnx)

This environment is for Class 22, Spatial Data. It has **OSMnx** and **GeoPandas**, plus Shapely, pyproj and geopy.

OSMnx is pure Python, but it depends on geospatial libraries with compiled parts (GEOS, PROJ), so Conda is the reliable way to install it.

---

## On the course cluster (Explorer)

You don't need to install anything. The environment is already built at `/courses/NETS7052.202710/shared/cmns-osmnx`. You connect it to JupyterLab once, the same way you connected `cmns-ml` in Class 15:

1. In [Open OnDemand](https://ood.explorer.northeastern.edu/), open the **Courses** menu, click **JupyterLab (Python)**, and launch it with your usual settings. Leave **Custom Anaconda Environment** blank.
2. Open a terminal (**File → New → Terminal**) and run this single line, exactly as written:
   ```bash
   /courses/NETS7052.202710/shared/cmns-osmnx/bin/python -m ipykernel install --user --name cmns-osmnx --display-name "Python (cmns-osmnx)"
   ```
3. Reload the browser tab. Open your copy of the notebook and choose **Kernel → Change Kernel…** → **Python (cmns-osmnx)**.
4. Check it in a notebook cell:
   ```python
   import sys, osmnx, geopandas
   print(sys.executable)
   print("osmnx", osmnx.__version__, "| geopandas", geopandas.__version__)
   ```
   The first line should start with `/courses/NETS7052.202710/shared/cmns-osmnx/`.

**If it doesn't work:**

- *Python (cmns-osmnx) isn't in the kernel list.* Reload the browser tab. JupyterLab only reads the list of kernels when the page loads.
- *An import fails with a message about NumPy 1.x and 2.x, or `sys.executable` starts with `/shared/EL9/`.* The notebook is running on the cluster's own Python, not this environment. Run `cat ~/.local/share/jupyter/kernels/cmns-osmnx/kernel.json` in the terminal: the first path in `argv` should be the one from step 2. If it isn't, run step 2 again, then restart the kernel (**Kernel → Restart Kernel**). Switching kernels isn't enough, because the old process keeps running under the same name.
- *A cell that downloads a street network hangs or fails with a server error.* OSMnx gets its data from the Overpass API while the notebook runs, and Overpass is sometimes busy. Wait a minute and run the cell again. OSMnx keeps what it has already downloaded in a `cache` folder next to the notebook, so a rerun doesn't start from scratch.

### Building the shared environment (instructor)

Once per semester. Run this in a terminal inside an OOD JupyterLab session, so that it runs on a compute node rather than the login node, from the top of your clone of this repository:

```bash
source /shared/EL9/explorer/anaconda3/2024.06/etc/profile.d/conda.sh
conda env create -p /courses/NETS7052.202710/shared/cmns-osmnx -f envs/osmnx/environment.yml
chmod -R o+rX /courses/NETS7052.202710/shared/cmns-osmnx
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
conda activate cmns-osmnx
```

### 3) Register as a Jupyter kernel

```bash
conda activate cmns-osmnx
python -m ipykernel install --user --name cmns-osmnx --display-name "Python (cmns-osmnx)"
```

### 4) Verify the install

```bash
conda activate cmns-osmnx
python -c "import osmnx as ox, geopandas as gpd, shapely; import pyproj; print('osmnx/geopandas OK')"
```

Jupyter smoke test:

```python
import osmnx as ox
import geopandas as gpd
import shapely
import pyproj
import networkx as nx

print("osmnx:", ox.__version__)
print("geopandas:", gpd.__version__)
print("shapely:", shapely.__version__)
print("pyproj:", pyproj.__version__)
print("networkx:", nx.__version__)
```

### 5) Launch JupyterLab

```bash
conda activate cmns-osmnx
jupyter lab
```

Kernel: **Python (cmns-osmnx)**

### 6) Updating / removing the environment

Update:

```bash
conda activate cmns-osmnx
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-osmnx
```

### 7) Troubleshooting (GIS-specific pain points)

1) **“GEOS/PROJ errors” or `ImportError` in shapely/pyproj/fiona.**  
   This usually happens when mixing channels. Use strict conda-forge and recreate the env.

2) **Jupyter is running the wrong kernel.**  
   Confirm kernel registration:

   ```bash
   jupyter kernelspec list
   ```

3) **macOS Apple Silicon: mixed architecture.**  
   Recreate the env in a terminal where `uname -m` matches your CPU.

4) **Network download failures (OSMnx downloads data).**  
   Try again on a different network, or test basic connectivity:

   ```bash
   python -c "import urllib.request; print(urllib.request.urlopen('https://www.openstreetmap.org').status)"
   ```

5) **Slow installs / solver timeouts.**  
   Use `mamba`:

   ```bash
   conda install -n base -c conda-forge mamba
   ```

6) **Still stuck? Collect diagnostics:**

   ```bash
   conda info
   conda list
   python -c "import sys; print(sys.executable)"
   ```
