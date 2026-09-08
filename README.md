# PHYS/NETS 7052: Computational Methods for Network Science — Fall 2026

Welcome! This repository hosts the Jupyter notebooks and supporting materials for each class meeting.

- **Course website / Jupyter Book:** https://computational-methods-network-science.github.io/nets7052_fa26/
- **GitHub repository:** https://github.com/computational-methods-network-science/nets7052_fa26/
- **Syllabus:** https://brennanklein.com/phys7052-fall26
- **Meetings:** Mon/Wed, 11:45am–1:25pm, 101 Belvidere, 3rd floor, 140A/B
- **Office hours:** Wednesdays 1:30–2:30pm, Network Science Institute (177 Huntington Ave, 10th floor) or Zoom

> **Note on course numbering.** This course was previously offered as **PHYS 7332** (Network Science Data II). It was renumbered to **PHYS/NETS 7052** for AY26–27. Materials from Fall 2025 live in the archived [`phys7332_fa25`](https://github.com/computational-methods-network-science/phys7332_fa25) repository.

## Course Overview

This course introduces computational methods for analyzing and modeling complex networks across scientific domains. It emphasizes programming-based workflows for working with network data: collection, cleaning, representation, and visualization. Topics include foundational network analysis, random graph models, community detection, machine learning for network data, dynamics on networks (diffusion, contagion, random walks), sampling and sparsification, temporal and spatial networks, and network comparison and reconstruction.

The course is built on the foundation of years of development by Matteo Chinazzi and Qian Zhang for earlier iterations of Network Science Data.

## Getting Started

Everything runs on Northeastern's **Explorer** HPC cluster. Class 00 walks through the whole setup; the short version:

1. **Log in to Open OnDemand:** https://ood.explorer.northeastern.edu/
2. **Load conda and activate the class environment:**
   ```bash
   module load anaconda3/2024.06
   source activate /courses/NETS7052.202710/shared/nets7052-env
   ```
3. **Fork this repository** on GitHub (button in the top right).
4. **Clone your fork** into your student directory on the cluster:
   ```bash
   cd /courses/NETS7052.202710/students/$USER
   git clone <YOUR FORK URL>
   ```
5. **Track this repo as `upstream`** so you can pull updates all semester:
   ```bash
   cd nets7052_fa26
   git remote add upstream https://github.com/computational-methods-network-science/nets7052_fa26.git
   git fetch upstream
   ```
6. **Pull new material** before each class:
   ```bash
   git fetch upstream && git merge upstream/main
   ```

### Environments

The main environment is defined in [`environment.yml`](environment.yml) (`nsdm-core`: scientific Python, NetworkX, plotting). A few later classes need heavier, conflicting dependencies and get their own environment under [`envs/`](envs/):

| Environment | Used for |
|---|---|
| `nsdm-core` | most classes |
| `nsdm-ml` | Classes 12–13 (machine learning; PyTorch, gensim) |
| `nsdm-osmnx` | Class 22 (spatial data) |
| `nsdm-igraph` | igraph / Leiden community detection |
| `nsdm-graphtool` | graph-tool / Infomap |

On the cluster the shared `nsdm-core` environment is already built for you at the path in step 2 — you do not need to create it. The `envs/*/setup.md` guides are there if you want to run any of this on your own machine.

Full instructions, including SSH keys and fixing common Git problems, are in [Class 00](notebooks/class_00/class_00_intro_and_setup.ipynb).

## Repository Layout

```
nets7052_fa26/
├── notebooks/
│   └── class_NN/                   one folder per class meeting, posted before that class
├── environment.yml                 the main conda environment (nsdm-core)
├── envs/                           specialized environments (ml, osmnx, igraph, graphtool)
├── data/README.md                  where the large course datasets live
├── _config.yml, _toc.yml           Jupyter Book configuration
└── README.md
```

**Notebooks are posted before each class meeting**, not all at once. Pull from `upstream` before class (see step 6 above) and the new material will appear. Class numbers here match the class numbers on the syllabus.

Class numbers in this repo match the class numbers on the syllabus. Sessions without a notebook (the guest speaker, project presentations) are listed in the schedule below but have no folder.

## Data

Large datasets are **not** stored in this repository. They live on the cluster at `/courses/NETS7052.202710/data/`, which is readable by everyone in the class. See [`data/README.md`](data/README.md) for details and for how to point a notebook at them.

## Schedule

| Class | Date | Topic |
|---|---|---|
| — | Mon, Sep 7 | *Labor Day — no class* |
| 0 | Wed, Sep 9 | Introduction to the Course, GitHub, Computing Setup |
| 1 | Mon, Sep 14 | Python Refresher (Data Structures, NumPy) |
| 2 | Wed, Sep 16 | Introduction to NetworkX 1 — Loading Data, Basic Statistics |
| 3 | Mon, Sep 21 | Introduction to NetworkX 2 — Graph Algorithms |
| 4 | Wed, Sep 23 | Distributions of Network Properties & Centralities |
| 5 | Mon, Sep 28 | Scraping Web Data — BeautifulSoup, HTML, Pandas |
| 6 | Wed, Sep 30 | Data Science & SQL |
| 7 | Mon, Oct 5 | Clustering & Community Detection 1 — Traditional |
| 8 | Wed, Oct 7 | Clustering & Community Detection 2 — Contemporary |
| — | Mon, Oct 12 | *Indigenous Peoples Day — no class* |
| 9 | Wed, Oct 14 | Guest Speaker |
| 10 | Mon, Oct 19 | Project Update Presentations |
| 11 | Wed, Oct 21 | Visualization — Python |
| 12 | Mon, Oct 26 | Introduction to Machine Learning 1 — General |
| 13 | Wed, Oct 28 | Introduction to Machine Learning 2 — Networks |
| 14 | Mon, Nov 2 | Dynamics on Networks 1 — Diffusion and Random Walks |
| 15 | Wed, Nov 4 | Dynamics on Networks 2 — Compartmental Models |
| 16 | Mon, Nov 9 | Dynamics on Networks 3 — Agent-Based Models |
| — | Wed, Nov 11 | *Veterans Day — no class* |
| 17 | Mon, Nov 16 | Network Sampling |
| 18 | Wed, Nov 18 | Network Filtering / Thresholding |
| 19 | Mon, Nov 23 | Dynamics of Networks — Temporal Networks |
| — | Wed, Nov 25 | *Fall break — no class* |
| 20 | Mon, Nov 30 | Network Comparison & Graph Distances |
| 21 | Wed, Dec 2 | Network Reconstruction from Dynamics |
| 22 | Mon, Dec 7 | Spatial Data, OSMNX, GeoPandas |
| 23 | Wed, Dec 9 | Final Presentation — Office Hours |
| 24 | Mon, Dec 14 | Final Presentations 1 |
| 25 | Wed, Dec 16 | Final Presentations 2 |

**Assignments** are announced and due on Fridays: A1 announced Sep 18, due Oct 2 · A2 announced Oct 9, due Oct 23 · A3 announced Oct 30, due Nov 13.

## Grading

| Component | Weight |
|---|---|
| Class attendance & participation | 10% |
| Problem sets | 45% |
| Mid-semester project presentation | 15% |
| Final project — presentation & report | 30% |

## Final Project

The final project is a chance to synthesize what you have learned into pedagogical material of your own. Modeled after the chapters in this book, you will write a new "chapter" for the class textbook: a thoroughly documented Python notebook explaining an advanced topic not deeply covered in the course. You are expected to research the background of the technique, the original paper(s) introducing it, and how it is used in the current network analysis literature. A template notebook will be posted here later in the semester, ahead of the Class 10 project update presentations.

## Instructor

**Brennan Klein** is an Assistant Professor in the Department of Communication Studies and the Department of Physics at Northeastern University, and core faculty at the Network Science Institute. He is the program director of the interdisciplinary MS in Complex Network Analysis. He directs the Complexity & Society Lab, which works on (1) information, emergence, and communication in complex systems, and (2) data justice — drawing on complex systems science to document, and fight against, emergent or systemic disparities in society, especially as they relate to the U.S. criminal-legal system. He also directs NetSI Sport, which studies team coordination, performance, and networks in elite sports. In 2023 he received the René Thom Young Researcher Award. He is the Data for Justice Fellow at the Institute on Policing, Incarceration & Public Safety at Harvard University's Hutchins Center for African & African American Research. He received a PhD in Network Science from Northeastern in 2020 and a BA in Cognitive Science & Psychology from Swarthmore College in 2014. Website: [brennanklein.com](https://brennanklein.com).

## Materials

There are no required materials, but we periodically draw from:

- Bagrow & Ahn (2024). ***Working with Network Data: A Data Science Perspective***. Cambridge University Press. [link](https://www.cambridge.org/network-data)

Also recommended:

- Barabási (2016). ***Network Science***. Cambridge University Press. [link](http://networksciencebook.com/)
- Newman (2018). ***Networks: An Introduction***, 2nd ed. Oxford University Press. [link](https://global.oup.com/academic/product/networks-9780198805090)
- VanderPlas (2019). ***Python Data Science Handbook***. O'Reilly. [link](https://github.com/jakevdp/PythonDataScienceHandbook)
