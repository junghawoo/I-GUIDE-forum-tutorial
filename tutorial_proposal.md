# Tutorial Proposal

**Title:** From Dam Risk Metrics to Interactive Maps: A Hands-on Jupyter Tutorial for Open Geospatial REST APIs
**Track:** Workshops and Tutorials
**Length:** Quarter-day (2 hours)
**Level:** Intermediate (Graduate Student / Researcher)

## 1. Abstract

This tutorial takes participants on a journey from web-based data discovery to programmatic spatial validation — entirely through a REST API, with no database setup required. We begin with the "finished product"—the High Hazard Dam Dashboard—to establish a research context for dam-failure vulnerability. Participants will then "peek behind the curtain" at the Swagger API documentation to discover the endpoints that power the service. Moving into Jupyter Notebooks, we transition to a programmatic workflow: mastering the "functional plumbing" of REST APIs to query risk metrics, constructing complex ordinal filters, and rendering interactive GeoJSON maps.

The session culminates in a "Trust but Verify" challenge. The API serves some geometry layers from a **precomputed cache** (simplified to 1m tolerance, clipped to dam zones at import time) for speed. Participants will pull both the precomputed summary counts and the raw underlying geometries for the same dam, then reproduce the API's numbers themselves with a GeoPandas spatial join (`gpd.sjoin`). Where the two disagree, they'll trace the gap back to precision, clipping, and caching decisions made upstream. This "round-trip" teaches a vital lesson in data provenance — how to verify precomputed web results against raw spatial logic — using only the Python geospatial stack already available in their notebook environment. Attendees will leave with a complete, reusable toolbox of notebooks for bridging the gap between high-level web services and defensible spatial data science.

## 2. Learning Objectives

- **API Literacy:** Navigate Swagger/OpenAPI documentation to identify schemas and endpoints.
- **Programmatic Interrogation:** Build robust Python `requests` calls using multi-criteria logic (AND/OR filters) to move beyond simple data downloads.
- **Dynamic Storytelling:** Transform JSON responses into styled, interactive Leaflet/folium maps directly within a notebook environment.
- **Audit & Validation:** Gain confidence in "black box" APIs by reproducing a precomputed metric from raw geometry using a GeoPandas spatial join, and reasoning about why the two might differ.

## 3. Detailed Schedule (120 Minutes)

### I. The Anatomy of a Geospatial Service (10 min)
The Dashboard & Swagger UI: a tour of the dam risk dashboard, followed by a lookup exercise in the API docs to understand the "Map vs. Data" relationship — what the dashboard shows vs. the endpoint that produced it.

### II. Notebook 1: The Request Lifecycle (20 min)
**Skills:** Python `requests` patterns, handling pagination/limits, and converting JSON responses into a GeoDataFrame.

### III. Notebook 2: Multi-Criteria Risk Filtering (25 min)
**Skills:** Constructing JSON payloads for `POST /risk/metrics/filters` with ordinal operators (`gte`, `lte`, `eq`, `in`) and `AND`/`OR` logic.
**Challenge:**
- Identify high-risk dams based on intersecting Social Vulnerability Index (SVI) thresholds.
- Identify high-risk dams based on the number of hospital beds affected.
- Identify high-risk dams based on the length of interstates affected.

### — Break (10 min) —

### IV. Notebook 3: Interactive Mapping with Leaflet/folium (30 min)
**Skills:** Styling GeoJSON footprints and infrastructure layers (from `/risk/zone.geojson` and `/risk/features/multi.geojson`) as an interactive, layered map to build a visual risk narrative.

### V. Notebook 4: The GeoPandas "Round-Trip" Validation (20 min)
**Skills:** Pulling both a precomputed summary (`/risk/summary`) and the raw underlying geometry for the same dam, then reproducing the count with `gpd.sjoin(features, zone, predicate="intersects")`.
**Discussion:** Why precomputed and self-joined counts might differ — cache simplification tolerance (1m), clipping at import time vs. live geometry, and data currency.

### Wrap-up (5 min)
Recap of the four-notebook toolbox and pointers for extending it to other dam-risk questions.

## 4. Technology & Support

The tutorial runs entirely on the participants' existing execution environment: the workshop platform clones a per-student GitHub repository and executes it from JupyterLab, so no local environment setup, installation, or database provisioning is required at session start. All work is done against a live, hosted REST API (no local server or database to run) using standard Python packages (`requests`, `geopandas`, `shapely`, `folium`). Because the "Trust but Verify" validation step uses GeoPandas spatial joins on API-served geometry rather than a personal database, there is no per-student database sandbox to provision or troubleshoot — participants can focus entirely on spatial logic and API literacy from minute one.
