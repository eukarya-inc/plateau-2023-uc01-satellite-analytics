## Flood Analysis with SAR and PLATEAU
This is a usecase for PLATEAU in FY2023.

This project has been tested on Google Colaboratory (2023.Nov).

### Source Code Descriptions

This repository is designed to be deployed on Google Drive and used primarily through Google Colab. The notebooks should be executed in the order indicated by the sequential numbers at the beginning of their filenames. Each notebook first downloads necessary data and caches precomputed data on Google Drive for memory efficiency and reusability. Subsequent notebooks utilize these cached data for predictions. Therefore, it's essential to authorize Google Drive connection and create a working directory on Google Drive. The path to this directory must be set before executing the notebooks. Additionally, be mindful of the available space on Google Drive, especially when making predictions over extensive areas.


The easiest way is to run the notebook [0_Installation_PLATEAU_FloodSAR.ipynb](https://colab.research.google.com/github/eukarya-inc/plateau-2023-uc01-satellite-analytics/blob/feature/install/PLATEAU-FloodSAR/0_Installation_PLATEAU_FloodSAR.ipynb) to deploy this repository in your google drive and download model checkpoint.

#### 0_Installation_PLATEAU_FloodSAR.ipynb
- Deploy this repository into your Google Drive and download model checkpoint.
- **Required Procedures**: Connection to Google Drive

#### 0_PrepareProject.ipynb
- Initializes the project by setting up the case name and defining the area of interest. Parses CityGML to generate building data within the specified area and pre-downloads Digital Elevation Model (DEM).
- **Required Procedures**: Connection to Google Drive.

#### 1_EstimateSAR-FloodPrbDiff.ipynb
- Acquires Sentinel-1 data for the area of interest and generates flood probability raster data (logit).
- **Required Procedures**: Authentication with Google Earth Engine (GEE), Connection to Google Drive.
- **Required Files**: Flood Estimation Model Checkpoint

#### 2_GeneratePointGroup.ipynb
- Creates point cloud data from flood probability raster data. Parameters are adjustable.
- **Required Procedures**: Connection to Google Drive.

#### 3_CalcFloodDEMRaster.ipynb
- Generates flood surface elevation raster data from point cloud data. Parameters are adjustable.
- **Required Procedures**: Connection to Google Drive.

#### 3_GIAJ-CalcFloodDEMRaster.ipynb
- Produces flood surface elevation raster data from flood area GeoJSON published by the Geospatial Information Authority of Japan.
- **Required Procedures**: Connection to Google Drive.

#### 4_AssessBuildings.ipynb
- Generates disaster data for buildings using building data and flood surface elevation raster data.
- **Required Procedures**: Connection to Google Drive.

#### 5_Uploade.ipynb
- Uploads data to Re:Earth CMS.
- **Required Procedures**: Connection to Google Drive, Authentication with Re:Earth CMS.

#### plateau_floodsar_lib.py
- Downloads and locally saves DEM tiles from the Geospatial Information Authority of Japan, integrates multiple types (e.g., DEM5A, DEM5B), calculates geoid height, and extracts and fills values for the specified area. (Includes 4 classes)
