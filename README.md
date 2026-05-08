# Ottawa Microclimate & Canopy Analytics Platform

**[View the Live Interactive Dashboard Here](https://www.arcgis.com/apps/dashboards/801e9deb8ad349afabfbf8baad8b318c)**

## 1. Executive Summary
The Ottawa Microclimate & Canopy Analytics Platform is an enterprise-grade spatial intelligence tool designed to mathematically quantify the inverse correlation between municipal urban canopy density and microclimate surface temperatures. Built using an automated spatial ETL pipeline (FME, Python/ArcPy), the project fused over 300,000 municipal tree assets with Level-2 thermal and multispectral satellite telemetry. The final deployment provides an interactive, hardware-accelerated dashboard that allows urban planners to identify critical Urban Heat Islands (UHI) and strategically allocate forestry budgets.

## 2. Technical Architecture & Methodology
The solution required bridging dynamic municipal vector databases with static orbital raster telemetry.

### Phase 1: Data Engineering & ETL Pipeline (FME)  <img width="954" height="488" alt="FME_Spatial_Pipeline" src="https://github.com/user-attachments/assets/3f0ba640-641d-4cc2-84a6-be2dd1d2d9ed" />                       [FME Screenshot]
* Processed over 300,000 raw tree inventory points from the City of Ottawa. 
* Executed complex spatial joins to aggregate tree counts within 116 unique Ottawa Neighbourhood Study (ONS) administrative boundaries.

### Phase 2: Spatial Analytics & Raster Math (Python / ArcPy) [ArcPy script](ArcPy Script) 
<img width="1915" height="1018" alt="ArcGIS Pro (2)" src="https://github.com/user-attachments/assets/46035093-7ec0-4f8e-9d4e-14cae2e53495" />

* **Multispectral Processing:** Extracted Band 4 (Red) and Band 8 (NIR) from Sentinel-2 telemetry to compute the Normalized Difference Vegetation Index (NDVI), creating a seamless raster mosaic.
* **Thermal Processing:** Extracted Band 10 from Landsat 9 TIRS, applying USGS scaling algorithms and Kelvin-to-Celsius conversions to map Land Surface Temperature (LST).
* **Zonal Statistics:** Calculated the exact Mean LST and Mean NDVI for all pixels falling within each of the 116 municipal boundaries, joining the outputs back to the primary spatial database.

### Phase 3: ArcGIS Dashboard <img width="955" height="443" alt="Mean Surface Temperature" src="https://github.com/user-attachments/assets/56d2929f-77c0-45d1-86b5-db2927e86754" />
<img width="955" height="445" alt="Municipal Tree Density" src="https://github.com/user-attachments/assets/3bc8c1d0-f421-44b6-88a7-4baeebd3c516" />

* Deployed a dark-theme UI with a dynamic Layer Toggle engine to visually contrast "Thermal Heat" vs "Canopy Density".
* Engineered an application-tier topological filter (`Tree_Count > 0`) to silently resolve complex boundary duplications from the spatial join phase, locking the visible data to the exact 116 true neighborhood records.

## 3. The Business Problem Solved
This platform directly addresses the challenge of resource allocation in urban forestry. It provides undeniable spatial evidence that the hottest municipal zones directly correlate with canopy gaps, allowing municipal governments to transition from reactive maintenance to targeted, data-driven climate mitigation.



## Data Sources & Citations: 

1. City of Ottawa Open Data — Municipal Tree Inventory (Updated: Mar 27, 2026) | ONS Boundaries (Updated: Nov 27, 2024) 
**[open.ottawa.ca](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-3/explore?location=45.249599%2C-75.799952%2C0)** 

2. USGS EarthExplorer — Landsat 9 L2 TIRS, Scene LC09_L2SP_016028 (Acquired: Aug 11, 2025) **[earthexplorer.usgs.gov](https://earthexplorer.usgs.gov/)** 

3. ESA Copernicus — Sentinel-2 L2A MSI, Tiles T18TVR/T18TVQ (Acquired: Aug 15, 2025) **[dataspace.copernicus.eu](https://browser.dataspace.copernicus.eu/?zoom=5&lat=50.16282&lng=20.78613&demSource3D=%22MAPZEN%22&cloudCoverage=30&dateMode=SINGLE)**
