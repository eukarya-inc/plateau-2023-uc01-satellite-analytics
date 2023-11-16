## Flood Analysis with SAR and PLATEAU
This is a usecase for PLATEAU in FY2023.

This project has been tested on Google Colaboratory (2023.Nov).

### Installation
The easiest way to deploy this repository is downloading the notebook [Git2Colab_Installation_PLATEAU_FloodSAR.ipynb](https://colab.research.google.com/github/eukarya-inc/plateau-2023-uc01-satellite-analytics/blob/main/Git2Colab_Installation_PLATEAU_FloodSAR.ipynb) to your google drive and running it on Google Colaboratory. 

### Optional: Pre-trained Model Checkpoints

To predict flood area from satellite data, pre-trained model checkpoints are required.
There are two types of input data models: a single-polarization (vv) model and a dual-polarization (vv, vh) model.
By default, the dual-polarization model is used.

- Dual-polarization model: [model_epoch_aug_mask_100.pth](https://drive.google.com/file/d/1rD68QJQr-gmF9jeZY5qBjVJJqoWOFe7E/)
- Single-polarization model: [model_epoch_vv_119.pth](https://drive.google.com/file/d/1VEgB3VcLOYEwud9Zo-QsHUAMmNkrGDZq/)

If you already run [Git2Colab_Installation_PLATEAU_FloodSAR.ipynb](https://colab.research.google.com/github/eukarya-inc/plateau-2023-uc01-satellite-analytics/blob/main/Git2Colab_Installation_PLATEAU_FloodSAR.ipynb), This step can be skipped

### Descriptions of Source Codes under PLATEAU-FloodSAR directory 
This repository is designed to be deployed on Google Drive and used primarily through Google Colab. The notebooks should be executed in the order indicated by the sequential numbers at the beginning of their filenames. Each notebook first downloads necessary data and caches precomputed data on Google Drive for memory efficiency and reusability. Subsequent notebooks utilize these cached data for predictions. Therefore, it's essential to authorize Google Drive connection and create a working directory on Google Drive. The path to this directory must be set before executing the notebooks. Additionally, be mindful of the available space on Google Drive, especially when making predictions over extensive areas.

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


