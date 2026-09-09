# Course data

The big datasets live on the cluster, not in this repo:

```
/courses/NETS7052.202710/data/
```

Everyone in the class can read that directory, so nothing you need for a class notebook has to be downloaded. Read them straight from there — don't copy them into your own folder. The largest is 94 MB, and eight copies of it on a shared filesystem helps nobody.

## Using it from a notebook

Reference the shared path directly rather than a local `data/` folder:

```python
from pathlib import Path

DATA = Path("/courses/NETS7052.202710/data")
df = pd.read_csv(DATA / "some_dataset.csv")
```

If you are working off the cluster, set the same variable to wherever you keep your own copy and the rest of the notebook will work unchanged:

```python
DATA = Path("~/my_local_data").expanduser()
```

## What's in there

| File | Size | Used by |
|---|---|---|
| `db28seg.dd.wac.2021.2022.asc` | 94 MB | Class 18 — Network Filtering / Thresholding |
| `mystery.pickle` | 18 MB | Class 11 — Visualization |
| `tl_2020_25_tract/` (shapefile) | 6.8 MB | Class 22 — Spatial Data |
| `cit-HepPh.txt` | 6.4 MB | Class 17 — Network Sampling |
| `ma_clim.csv` | 5.5 MB | Class 22 — Spatial Data |

Small example files (under ~5 MB) that a notebook needs in order to run standalone are committed alongside it, under `notebooks/class_NN_<topic>/data/`.
