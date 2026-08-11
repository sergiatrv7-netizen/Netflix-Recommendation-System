## About this folder

This folder contains the raw datasets used for the Netflix Recommendation System project.

### `viewing_history_sample.csv`

The original `viewing_history.csv` file (~89 MB, 1.76M rows, 55,000 users) exceeds
GitHub's recommended file size limits, so it was not included in this repository.

Instead, `viewing_history_sample.csv` (~9.6 MB, ~172K rows) contains a **10% random
sample of users**, with their **full viewing history preserved** (not a random sample
of individual rows). This approach keeps each sampled user's complete watch pattern
intact, which is important for training and evaluating recommendation models that
rely on per-user history.

To regenerate the full dataset locally, run `generar_historial_visualizaciones.py`.
