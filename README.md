# NETS/PHYS 7052: Computational Methods for Network Science — Fall 2026

Mondays & Wednesdays: 11:45am – 1:25pm
September 9 – December 16, 2026
101 Belvidere, 3rd fl, 140A/B

**Course Website:** https://computational-methods-network-science.github.io/nets7052_fa26/

**Github Repository:** https://github.com/computational-methods-network-science/nets7052_fa26

**Syllabus:** https://brennanklein.com/phys7052-fall26

**Office Hours:** Wednesdays, 1:30–2:30pm, Network Science Institute (177 Huntington Ave, 10th floor) or Zoom

## Summary

Introduces computational methods for analyzing and modeling complex networks across scientific domains. Emphasizes programming-based workflows for working with network data, including data collection, cleaning, representation, and visualization. Covers foundational concepts in network analysis; random graph models; community detection; machine learning for network data; network dynamics such as diffusion, contagion, and random walks; network sampling and sparsification; temporal and spatial networks; and network comparison and reconstruction. Provides structured opportunities to implement algorithms with feedback, interpret results, and communicate network-based insights in technical and interdisciplinary contexts.

This course was previously offered as PHYS 7332 (Network Science Data II), and was renumbered to NETS/PHYS 7052 for AY26–27. It is built on the foundation of years of work and development by Matteo Chinazzi and Qian Zhang, for earlier iterations of Network Science Data.

## Getting Started

Everything runs on Northeastern's Explorer HPC cluster. Class 00 walks through the whole setup; the short version:

1. **Log in to Open OnDemand:** https://ood.explorer.northeastern.edu/
2. **Load conda and activate the class environment:**
   ```bash
   module load anaconda3/2024.06
   source activate /courses/NETS7052.202710/shared/cmns-core
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

Full instructions, including SSH keys and fixing common Git problems, are in [Class 00](notebooks/class_00/class_00_intro_and_setup.ipynb).

### Environments

The main environment is defined in [`environment.yml`](environment.yml) (`cmns-core`: scientific Python, NetworkX, plotting). A few later classes need heavier, conflicting dependencies and get their own environment under [`envs/`](envs/):

| Environment | Used for |
|---|---|
| `cmns-core` | most classes |
| `cmns-ml` | Classes 12–13 (machine learning; PyTorch, gensim) |
| `cmns-osmnx` | Class 22 (spatial data) |
| `cmns-igraph` | igraph / Leiden community detection |
| `cmns-graphtool` | graph-tool / Infomap |

On the cluster the shared `cmns-core` environment is already built for you at the path in step 2 — you do not need to create it. The `envs/*/setup.md` guides are there if you want to run any of this on your own machine.

### Repository Layout

```
nets7052_fa26/
├── notebooks/
│   └── class_NN/                   one folder per class meeting, posted before that class
├── environment.yml                 the main conda environment (cmns-core)
├── envs/                           specialized environments (ml, osmnx, igraph, graphtool)
├── data/README.md                  where the large course datasets live
├── _config.yml, _toc.yml           Jupyter Book configuration
└── README.md
```

Notebooks are posted before each class meeting, not all at once. Pull from `upstream` before class (step 6 above) and the new material will appear. Class numbers here match the class numbers on the syllabus.

### Data

The large datasets for this course live on the cluster at `/courses/NETS7052.202710/data/`, readable by everyone in the class. See [`data/README.md`](data/README.md) for what's there and how to load it.

## Course Learning Outcomes

1. Develop and maintain software to analyze networks derived from a range of data sources, including real-world and simulated datasets.
2. Implement network algorithms to measure clustering, path lengths, spectra, community structure, and dynamics, demonstrating both theoretical understanding and computational proficiency.
3. Construct reproducible data analyses that integrate high-performance computing resources (e.g., the Explorer cluster at Northeastern University) for handling large-scale network data.
4. Design and code generative network models to simulate network growth, structure, and dynamics, and apply these models for inference from empirical data.
5. Collect network data online through web scraping, incorporating data collection ethics and norms.
6. Create and present pedagogical materials (e.g., a Jupyter Book chapter) on an advanced network analysis topic not covered in lectures, communicating technical ideas clearly to both specialist and non-specialist audiences.

## Course Materials

Our main resource for the course is the ever-growing Jupyter Book, where we will host the Python notebooks used in this class: https://computational-methods-network-science.github.io/nets7052_fa26/. Beyond that, there are no required materials for this course, but we will periodically draw from:

- Bagrow & Ahn (2024). ***Working with Network Data: A Data Science Perspective***. Cambridge University Press; 1st Edition; 978-1009212595. https://www.cambridge.org/network-data

Additionally, we recommend engagement with other useful network science and/or Python materials:

- Barabási (2016). ***Network Science***. Cambridge University Press; 1st Edition; 978-1107076266. http://networksciencebook.com
- Newman (2018). ***Networks: An Introduction***. Oxford University Press; 2nd Edition; 978-0198805090. https://global.oup.com/academic/product/networks-9780198805090
- VanderPlas (2019). ***Python Data Science Handbook***. O'Reilly Media, Inc; 978-1491912058. https://github.com/jakevdp/PythonDataScienceHandbook

## Coursework, Class Structure, Grading

**Logistics.** This is a twice-weekly hands-on class that emphasizes building experience with coding. This does not necessarily mean every second of every class will be live-coding, but it will inevitably come up in how the class is taught. We are often on the lookout for improving the pedagogical approach to this material, and we would welcome feedback on class structure. This course assumes prior experience with Python and basic linear algebra/probability; a short Python refresher is provided in Week 1.

**Cluster workflows.** This course is delivered primarily on Northeastern's high-performance computing cluster. We will (a) provide a course baseline environment (conda) for interactive work (via Open OnDemand/SSH), (b) demonstrate how to clone and customize per-student environments reproducibly, and (c) run heavy jobs on compute nodes as needed. If an environment breaks, students can revert to the baseline. Guidance will be provided in Week 1.

**Grading.** This course is graded as follows:

- Class Attendance & Participation: 10%
- Problem Sets: 45%
- Mid-Semester Project Presentation: 15%
- Final Project — Presentation & Report: 30%

## Final Project

The final project for this course is a chance for students to synthesize their knowledge of network analysis into pedagogical materials around a topic of their choosing. Modeled after chapters in the Jupyter book for this course, students will be required to make a new "chapter" for our class's textbook; this requires creating a thoroughly documented Python notebook that explains an advanced topic that was not deeply explored in the course. Students are required to conduct their own research into the background of the technique, the original paper(s) introducing the topic, and how/if it is currently used in today's network analysis literature. These chapters should contain informative data visualizations that build on one another, section-by-section. The purpose of this assignment is to demonstrate the coding skills gained in this course, doing so by learning a new network analysis technique and sharing it with members of the class. Halfway through the semester, there will be project update presentations where students receive class and instructor feedback on their project topics.

### Ideas for Final Project Chapters (non-exhaustive)

- Motifs in Networks
- Robustness / Resilience of Network Structure
- Network Game Theory
- Network Geometry
- Continuous Models of Network Dynamics
- Percolation in Networks
- Signed Networks
- Coarse Graining Networks
- Mesoscale Structure in Networks (e.g. core-periphery)
- Graph Isomorphism and Approximate Isomorphism
- Higher-Order Networks
- Introduction to Graph Neural Networks
- Hopfield Networks and Boltzmann Machines
- Graph Curvature or Topology
- Reservoir Computing
- Adaptive Networks
- Multiplex/Multilayer Networks
- Network Rewiring Dynamics
- Fitting Distributions to Network Data
- Hierarchical Networks
- Ranking in Networks
- Deeper Dive: Random Walks on Networks
- Deeper Dive: Directed Networks
- Deeper Dive: Network Null Models
- Deeper Dive: Network Paths and their Statistics
- Deeper Dive: Network Growth Models
- Deeper Dive: Hypothesis Testing in Social Networks
- Deeper Dive: Bipartite Networks
- Many more possible ideas!

## Schedule

This schedule is subject to change.

| Class | Date | Topic | Instructor |
|---|---|---|---|
| – | Mon, Sep 7, 26 | Labor Day (No Class) | |
| 0 | Wed, Sep 9, 26 | Introduction to the Course, GitHub, Computing Setup | Brennan Klein |
| – | Fri, Sep 11, 26 | | |
| 1 | Mon, Sep 14, 26 | Python Refresher (Data Structures, NumPy) | Brennan Klein |
| 2 | Wed, Sep 16, 26 | Introduction to NetworkX 1 — Loading Data, Basic Statistics | Brennan Klein |
| – | Fri, Sep 18, 26 | *Assignment 1 announced* | |
| 3 | Mon, Sep 21, 26 | Introduction to NetworkX 2 — Graph Algorithms | Brennan Klein |
| 4 | Wed, Sep 23, 26 | Distributions of Network Properties & Centralities | Brennan Klein |
| – | Fri, Sep 25, 26 | | |
| 5 | Mon, Sep 28, 26 | Scraping Web Data 1 — BeautifulSoup, HTML, Pandas | Brennan Klein |
| 6 | Wed, Sep 30, 26 | Data Science & SQL | Brennan Klein |
| – | Fri, Oct 2, 26 | **Assignment 1 due** | |
| 7 | Mon, Oct 5, 26 | Clustering & Community Detection 1 — Traditional | Brennan Klein |
| 8 | Wed, Oct 7, 26 | Clustering & Community Detection 2 — Contemporary | Brennan Klein |
| – | Fri, Oct 9, 26 | *Assignment 2 announced* | |
| – | Mon, Oct 12, 26 | Indigenous Peoples Day (No Class) | |
| 9 | Wed, Oct 14, 26 | Guest Speaker | TBD |
| – | Fri, Oct 16, 26 | | |
| 10 | Mon, Oct 19, 26 | Project Update Presentations | Brennan Klein |
| 11 | Wed, Oct 21, 26 | Visualization — Python | Brennan Klein |
| – | Fri, Oct 23, 26 | **Assignment 2 due** | |
| 12 | Mon, Oct 26, 26 | Introduction to Machine Learning 1 — General | Brennan Klein |
| 13 | Wed, Oct 28, 26 | Introduction to Machine Learning 2 — Networks | Brennan Klein |
| – | Fri, Oct 30, 26 | *Assignment 3 announced* | |
| 14 | Mon, Nov 2, 26 | Dynamics on Networks 1 — Diffusion and Random Walks | Brennan Klein |
| 15 | Wed, Nov 4, 26 | Dynamics on Networks 2 — Compartmental Models | Brennan Klein |
| – | Fri, Nov 6, 26 | | |
| 16 | Mon, Nov 9, 26 | Dynamics on Networks 3 — Agent-Based Models | Brennan Klein |
| – | Wed, Nov 11, 26 | Veterans Day (No Class) | |
| – | Fri, Nov 13, 26 | **Assignment 3 due** | |
| 17 | Mon, Nov 16, 26 | Network Sampling | Brennan Klein |
| 18 | Wed, Nov 18, 26 | Network Filtering / Thresholding | Brennan Klein |
| – | Fri, Nov 20, 26 | | |
| 19 | Mon, Nov 23, 26 | Dynamics of Networks — Temporal Networks | Brennan Klein |
| – | Wed, Nov 25, 26 | Thanksgiving Break (No Class) | |
| – | Fri, Nov 27, 26 | | |
| 20 | Mon, Nov 30, 26 | Network Comparison & Graph Distances | Brennan Klein |
| 21 | Wed, Dec 2, 26 | Network Reconstruction from Dynamics | Brennan Klein |
| – | Fri, Dec 4, 26 | | |
| 22 | Mon, Dec 7, 26 | Spatial Data, OSMNX, GeoPandas | Brennan Klein |
| 23 | Wed, Dec 9, 26 | Final Presentation — Office Hours | Brennan Klein |
| – | Fri, Dec 11, 26 | | |
| 24 | Mon, Dec 14, 26 | Final Presentations 1 | Brennan Klein |
| 25 | Wed, Dec 16, 26 | Final Presentations 2 | Brennan Klein |
| – | Fri, Dec 18, 26 | | |

## Instructor

**Brennan Klein** is an Assistant Professor in the Department of Communication Studies and the Department of Physics at Northeastern University, and core faculty at the Network Science Institute. He is the program director of the interdisciplinary MS in Complex Network Analysis. Prof. Klein is also the director of the Complexity & Society Lab, which is focused on two broad research areas: 1) Information, emergence, and communication in complex systems: developing tools and theory for characterizing dynamics, structure, and scale in networks, and 2) Data justice: drawing on complex systems science to document—and fight against—emergent or systemic disparities in society, especially as they relate to the U.S. criminal-legal system. He is also the director of NetSI Sport, an interdisciplinary research group studying team coordination, performance, and networks in elite sports. In 2023, Prof. Klein was awarded the René Thom Young Researcher Award, given to a researcher to recognize substantial early career contributions and leadership in research in Complex Systems-related fields. Prof. Klein is the Data for Justice Fellow at the Institute on Policing, Incarceration & Public Safety at Harvard University's Hutchins Center for African & African American Research. He received a PhD in Network Science in 2020 from Northeastern University and earned his BA in Cognitive Science & Psychology from Swarthmore College in 2014. Website: [brennanklein.com](https://brennanklein.com).
