# Course data

The large datasets for this course live on the cluster:

```
/courses/NETS7052.202710/data/
```

That directory is readable by everyone enrolled in the class and writable by the teaching staff. Nothing you need to run a class notebook has to be downloaded.

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

Small example files (under ~5 MB) that a notebook needs in order to run standalone are committed alongside it, under `notebooks/class_NN/data/`.

## Adding data (teaching staff)

Copy it to the shared directory rather than committing it:

```bash
cp big_dataset.csv /courses/NETS7052.202710/data/
```

Then add a row to the table above so students know what it is and which class uses it.
