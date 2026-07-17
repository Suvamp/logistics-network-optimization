# Last-Mile Logistics Network Optimization
### Vehicle Routing & Optimal Facility Placement · Chicago, IL

[![Python](https://img.shields.io/badge/Python-3.11-blue)](https://www.python.org)
[![OR-Tools](https://img.shields.io/badge/OR--Tools-9.8-green)](https://developers.google.com/optimization)
[![OSMnx](https://img.shields.io/badge/OSMnx-1.9-orange)](https://osmnx.readthedocs.io)
[![PuLP](https://img.shields.io/badge/PuLP-2.7-yellow)](https://coin-or.github.io/pulp)

A spatial optimization project that solves the **Capacitated Vehicle Routing Problem (CVRP)** and **p-median facility location** on Chicago's real road network.

**Skills demonstrated:** OSMnx · GeoPandas · NetworkX · Linear Programming (PuLP) · OR-Tools · R-tree spatial indexing · Folium

---

## Overview

Given 150 synthetic customer demand points and 20 candidate warehouse sites scattered across Chicago's actual drive network, the project:

1. Selects the best 3 warehouses to open (p-median facility location, solved as an ILP with PuLP)
2. Routes a multi-depot delivery fleet to serve every customer (Capacitated VRP, solved with Google OR-Tools)
3. Quantifies how much straight-line distance estimates underestimate real road travel in a dense urban grid

## Methodology

| Phase | Name | Description |
|-------|------|-------------|
| 1 | Setup & Data Acquisition | Download Chicago's road network from OpenStreetMap; generate synthetic demand points |
| 2 | Distance Matrix & Spatial Indexing | Vectorized Haversine distances + an R-tree index for fast proximity queries |
| 3 | Facility Location (p-Median) | ILP solver (PuLP) selects the optimal warehouse sites |
| 4 | Multi-Depot VRP | Google OR-Tools routes vehicle fleets from all selected warehouses |
| 5 | Distance Metric Comparison | Haversine vs. real network distance; detour factor analysis |
| 6 | Interactive Dashboard | Folium map with routes snapped to actual streets |
| 7 | Results Summary | Final metrics export |

## Results

Pulled from [`outputs/project_metrics.json`](outputs/project_metrics.json):

**Road network**
| Metric | Value |
|---|---|
| Nodes (intersections) | 29,700 |
| Edges (road segments) | 77,638 |
| Total road length | 10,373 km |

**Problem size**
| Metric | Value |
|---|---|
| Customers | 150 |
| Candidate warehouse sites | 20 |
| Total demand | 735 packages |

**Facility location (p=3)** — selected sites: `WH_03`, `WH_05`, `WH_19`

**Vehicle routing**
| Metric | Value |
|---|---|
| Naive baseline distance | 271.3 km |
| OR-Tools optimized fleet distance | 265.6 km |
| Distance reduction | 2.1% |
| Vehicles deployed | 9 (across 3 depots) |
| Customers served | 100% |

**Distance metric comparison**
| Metric | Value |
|---|---|
| Mean Haversine distance | 5.47 km |
| Mean network distance | 6.89 km |
| Mean detour factor | 1.278 (network routes are ~28% longer than straight-line) |

Per-vehicle breakdown: [`outputs/vehicle_summary.csv`](outputs/vehicle_summary.csv).

## Screenshots

<!-- Add screenshots below before publishing -->

**Chicago road network**
`outputs/chicago_network.png`

**p-Median coverage curve**
`outputs/facility_coverage_curve.png`

**Haversine vs. network distance comparison**
`outputs/distance_comparison.png`

**Interactive routing dashboard**
`outputs/logistics_dashboard.html` — open locally, or enable GitHub Pages on this repo for a live shareable link.

## Setup

```bash
conda env create -f environment.yml
conda activate logistics_optimization
jupyter lab notebooks/last_mile_logistics_optimization.ipynb
```

See [`SETUP.md`](SETUP.md) for full instructions (including a Google Colab option) and troubleshooting.

## Repository structure

```
.
├── README.md
├── SETUP.md
├── environment.yml
├── notebooks/
│   └── last_mile_logistics_optimization.ipynb
├── outputs/
│   ├── logistics_dashboard.html
│   ├── chicago_network.png
│   ├── facility_coverage_curve.png
│   ├── distance_comparison.png
│   ├── project_metrics.json
│   └── vehicle_summary.csv
├── data/                # data is fetched programmatically via OSMnx; empty by design
└── archive/              # earlier single-depot version of the notebook, kept for reference
```
