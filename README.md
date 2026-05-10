# Oxford Cycling GIS Analysis

In this project, I apply geospatial analysis techniques to investigate cycling infrastructure and socioeconomic patterns across Oxford, England, UK.

## Research Questions

1. What can the maximum speed of bike paths tell us about cyclists' safety in Oxford?
2. Are Lower Layer Super Output Areas (LSOAs) with similar Gross Domestic Product (GDP) per capita levels located close to one another more often than would be expected by random chance?
3. Do higher-income neighbourhoods have higher number of bike paths/ greater length of bike paths combined?

## Data Sources

- **LSOA boundaries** (December 2021, England and Wales) — geopackage file
- **Mid-2022 LSOA population estimates** — Office for National Statistics (ONS)
- **Regional GDP per capita** for local authorities — ONS
- **Bike lane network** — extracted from OpenStreetMap via `osmnx`

## Methods

- **Data cleaning**: Merged LSOA boundaries with population and GDP data, filtered to Oxford, and cleaned the OSM bike lane network (including handling roads with multiple `maxspeed` values, e.g. Woodstock Road).
- **Exploratory Spatial Data Analysis (ESDA)**: Distribution plots and choropleth maps of bike lane speeds and GDP per capita per LSOA, plus a Kernel Density Estimation (KDE) plot.
- **Spatial autocorrelation**: Built a Queen contiguity spatial weights matrix, computed spatial lag of GDP per capita, standardised values, and produced a Moran Plot. Confirmed with an R² coefficient.
- **Bike lane vs. income analysis**: Split bike lane geometries at LSOA boundaries, spatially joined them to LSOAs, calculated total bike lane length per LSOA, normalised by area, and ran a Pearson correlation against GDP per capita (also normalised by area).

## Key Findings

**Question 1 — Cyclist safety**
The majority of bike lanes in Oxford have a maximum speed limit of 20–30 mph, suggesting cycling in the city is generally safe. However, ~76 streets carry a 50 mph limit and ~40 carry 70 mph (i.e., Eastern and Northern Bypasses, Marston Ferry Road, and Woodstock Road), which represent areas of higher risk for cyclists.

**Question 2 — Spatial autocorrelation of income**
There is **no spatial autocorrelation** between GDP per capita across Oxford's LSOAs. This means that a high-income LSOA is not necessarily surrounded by other high-income LSOAs. In fact, with the Moran Plot and R² we can confirm that the distribution is random. Central Oxford (i.e., MSOA Oxford 008) is a notable outlier, driven by the clustering of University of Oxford colleges.

**Question 3 — Income vs. bike lane provision**
After normalising both GDP per capita and bike lane length by LSOA area, we found a **positive correlation** between income and cycling infrastructure. This suggests that higher-income neighbourhoods in Oxford have substantially more access to bike lanes than lower-income ones.


## Repository Contents

- `oxford_cycling_gis.ipynb` — the main analysis notebook
- `screenshot/` — saved plots (e.g. `speed_map_by_color.png`, `woodstock_road.png`) for interactive maps that don't render statically


## Viewing the Full Notebook

The `oxford_cycling_gis.ipynb` notebook is **truncated when previewed on GitHub**, probably due to large embedded outputs from the interactive maps (built with `osmnx` and `folium`). So GitHub's preview cuts off partway through the notebook, and a substantial portion of the analysis is not visible in the browser.

To view the complete analysis, clone the repository and run the notebook locally:

```cmd
:: Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git

:: Navigate into the project folder
cd <your-repo-name>

:: Open the notebook
jupyter notebook oxford_cycling_gis.ipynb
```

You'll need Python with the following libraries installed: `geopandas`, `osmnx`, `pysal` (`libpysal`, `mapclassify`), `contextily`, `shapely`, `seaborn`, `matplotlib`, `scikit-learn`, and `scipy`. Install them with:

```cmd
pip install geopandas osmnx pysal contextily shapely seaborn matplotlib scikit-learn scipy jupyter
```

## Contact
I hope that this proejct inspires other coders to explore similar topics and come up with insightful trends about their geographic area of interest! For any questions please don't hesitate to contact me via email at giorgiadt14@gmail.com or drop me a line on [LinkedIn](https://www.linkedin.com/in/giorgia-dim/)!