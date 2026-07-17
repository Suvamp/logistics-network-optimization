# Setup

## Option A — Local (conda)

```bash
# 1. Clone the repo
git clone <your-repo-url>
cd last-mile-logistics-network-optimization

# 2. Create the environment
conda env create -f environment.yml
conda activate logistics_optimization

# 3. Launch Jupyter
jupyter lab notebooks/last_mile_logistics_optimization.ipynb
```

Run all cells top to bottom. Phase 1 downloads Chicago's road network from OpenStreetMap (30–60s), and Phase 6 snaps ~9 vehicle routes onto the road graph (30–90s) — both need an internet connection on first run.

## Option B — Google Colab

Open the notebook in Colab and run the first code cell (`IN_COLAB` check) — it installs all dependencies via pip automatically. No local environment needed.

## Troubleshooting

| Error | Fix |
|-------|-----|
| OSMnx download fails | Check internet; try a smaller place string (e.g. `'Lincoln Park, Chicago'`); wait a few minutes and retry |
| PuLP returns `None` | Check for NaN in the distance matrix; try increasing `p` |
| OR-Tools finds no solution | Increase `time_limit_s`; raise vehicle capacity or `NUM_VEHICLES` |
| NetworkX path not found | Re-run Phase 1 with `retain_all=False` to keep only the largest connected component |
| Folium map blank | Hard-refresh (Ctrl+Shift+R) or try a different browser |
| Memory error on distance matrix | Reduce the number of demand points; use `dtype=np.float32` |
