# Ottawa Microclimate & Canopy Analytics Platform

**[View the Live Interactive Dashboard Here](https://www.arcgis.com/apps/dashboards/801e9deb8ad349afabfbf8baad8b318c)**

## Project Overview
This project is an automated spatial ETL pipeline and interactive web application designed to mathematically quantify the inverse correlation between urban canopy density and microclimate surface temperatures across 116 municipal neighborhoods in Ottawa, Ontario.

## Technical Architecture
* **Data Engineering (ETL):** FME was utilized to process and execute spatial joins on >300,000 municipal tree asset vectors against administrative boundaries.
* **Spatial Analytics:** Python and ArcPy were deployed to process Level-2 satellite imagery, executing Zonal Statistics to calculate mean surface temperatures and tree counts per neighborhood.
* **Application Deployment:** The final payload was optimized for cloud hosting and deployed via ArcGIS Dashboards, featuring dynamic spatial queries, hardware-accelerated UI, and application-tier data filtering (`Shape__Area > 1000 AND Tree_Count > 0`) to eliminate topological slivers and database duplication.

## Data Sources & Citations: 

1. City of Ottawa Open Data — Municipal Tree Inventory (Updated: Mar 27, 2026) | ONS Boundaries (Updated: Nov 27, 2024) 
**[open.ottawa.ca](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-3/explore?location=45.249599%2C-75.799952%2C0)** 

2. USGS EarthExplorer — Landsat 9 L2 TIRS, Scene LC09_L2SP_016028 (Acquired: Aug 11, 2025) **[earthexplorer.usgs.gov](https://earthexplorer.usgs.gov/)** 

3. ESA Copernicus — Sentinel-2 L2A MSI, Tiles T18TVR/T18TVQ (Acquired: Aug 15, 2025) **[dataspace.copernicus.eu](https://browser.dataspace.copernicus.eu/?zoom=5&lat=50.16282&lng=20.78613&demSource3D=%22MAPZEN%22&cloudCoverage=30&dateMode=SINGLE)**
