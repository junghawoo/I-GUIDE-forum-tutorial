# I-GUIDE Forum Tutorial — Dam Risk REST API

Materials for "From Dam Risk Metrics to Interactive Maps" (see `tutorial_proposal.md`).

## Contents

- `01_request_lifecycle.ipynb` — Python `requests` → GeoDataFrame, plus a one-liner `.explore()` map
- `02_multi_criteria_filtering.ipynb` — AND/OR ordinal filtering via `POST /risk/metrics/filters`
- `03_interactive_mapping.ipynb` — custom multi-layer folium maps
- `04_trust_but_verify.ipynb` — reproducing a precomputed API count from raw geometry with `gpd.sjoin`
- `requirements.txt` — Python dependencies

## API

All notebooks call a live, already-running instance of the Dam Risk REST API:

```
http://149.165.154.170:30080
```

This is an internal address — it's only reachable from a network with access to it
(e.g. campus network/VPN). If a request hangs or times out, that's the first thing
to check. Swagger docs: `http://149.165.154.170:30080/docs`.

No local server or database is required — every notebook talks to this API over
plain HTTP.

## Local environment (for testing before deploying to I-GUIDE)

```bash
conda create -n iguide-dam-tutorial -c conda-forge python=3.11 \
  geopandas folium mapclassify shapely pandas requests matplotlib jupyterlab ipykernel -y

conda activate iguide-dam-tutorial
python -m ipykernel install --user --name iguide-dam-tutorial --display-name "I-GUIDE Dam Tutorial"
jupyter lab
```

Then open any notebook and select the **I-GUIDE Dam Tutorial** kernel.

> Note: `geopandas` pulls in GDAL/PROJ, which resolve much more reliably through
> `conda-forge` than through plain `pip install -r requirements.txt`. The
> `requirements.txt` in this directory is provided for platforms (like I-GUIDE) that
> provision environments via pip; if you're setting this up yourself locally, the
> conda command above is the more reliable path.

All four notebooks have been executed end-to-end against the live API to confirm
they run cleanly with this environment.
