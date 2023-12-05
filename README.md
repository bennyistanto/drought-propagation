# Drought propagation

This repo contain notebook to analyze the propagation of **Meteorological Ddrought** (Standardized Precipitation Index - SPI) to **Hydrological Drought** (Standardized Streamflow Index - SSI) using **Lagged Correlation** at the pixel level with area of interest is Indonesia.

I use the **Standardized Precipitation Index** ([SPI](https://library.wmo.int/viewer/39629/download?file=wmo_1090_en.pdf&type=pdf&navigator=1)) - as proxy for meteorological drought, and the ([SPI](https://library.wmo.int/viewer/39629/download?file=wmo_1090_en.pdf&type=pdf&navigator=1)) - as proxy for hydrological drought. 

The SPI use monthly gridded Satellite precipitation estimates from Climate Hazards Group InfraRed Precipitation with Station data ([CHIRPS](https://doi.org/10.1038/sdata.2015.66)). 

The SSI use daily gridded River discharge in the last 24 hours from [GloFAS-ERA5 operational global river discharge reanalysis 1979–present](https://doi.org/10.5194/essd-12-2043-2020) as a proxy for the streamflow time series infomation.

There are 4 notebook along with support folder that required to run the analysis. Feel free to use your own preferences for this setting/folder arrangements.

1. `hyd` # Files required to proceed the hydrological drought goes here.
2. `met` # Files required to proceed the meteorological drought goes here.
3. `prop` # File required to proceed the propagation using lagged correlation goes here.
4. `subset` # In this folder I put `idn_subset_chirps.nc` file, a subset file to clip the input data to follow the area of interest. Basically this file are came from a shapefile polygon which has `land` attribute column with `value = 1`, then converting to raster based on `land` column, and set the cell size following our standard (I use 0.05 deg, because the SPI and SSI also has the same spatial resolution, 0.05 deg). After that, convert it to netCDF. All is done in ArcGIS Desktop.

The notebook

5. [`1_Steps_to_Generate_SPI_Using_CHIRPS_Data.ipynb`](./1_Steps_to_Generate_SPI_Using_CHIRPS_Data.ipynb)
6. [`2_Steps_to_Generate_SSI_Using_GloFAS-ERA5_Data.ipynb`](./2_Steps_to_Generate_SSI_Using_GloFAS-ERA5_Data.ipynb)
7. `3_Drought_Propagation_Met2Hyd_Using_CCA.ipynb`

	This is using Cross-Correlation for each pixel accross the entire time series, also employ noise filtering techniques like Singular Spectrum Analysis (SSA) which can help in isolate the underlying trends and patterns in our data before performing the CCA. This step is crucial for enhancing the signal-to-noise ratio in our datasets. 

This step-by-step guide was tested using Windows 11 with WSL2 - Ubuntu 22 enabled running on Thinkpad T480 2019, i7-8650U 1.9GHz, 64 GB 2400 MHz DDR4.

**WORK IN PROGRESS**
