# NSDM OSMnx / Geospatial environment (cmns-osmnx)

This guide installs a Conda environment for geospatial notebooks using **OSMnx + GeoPandas**.

OSMnx is pure Python, but it depends on geospatial libraries with compiled components (GEOS/PROJ/etc.), so Conda is the “foolproof” way to install it.

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
conda activate cmns-osmnx
```

---

## 3) Register as a Jupyter kernel

```bash
conda activate cmns-osmnx
python -m ipykernel install --user --name cmns-osmnx --display-name "Python (cmns-osmnx / OSMnx)"
```

---

## 4) Verify the install

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

---

## 5) Launch JupyterLab

```bash
conda activate cmns-osmnx
jupyter lab
```

Kernel: **Python (cmns-osmnx / OSMnx)**

---

## 6) Which notebooks use this environment?

- `class_24_spatial_v4.ipynb`
- `class_28_flows_v2.ipynb`
- `class_38_multilayer_urban_v2.ipynb`

---

## 7) Updating / removing the environment

Update:

```bash
conda activate cmns-osmnx
conda env update -f environment.yml --prune
```

Remove:

```bash
conda env remove -n cmns-osmnx
```

---

## 8) Troubleshooting (GIS-specific pain points)

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
