# LPJmL Crop Model Output Analysis

Jupyter notebooks for processing and evaluating LPJmL crop model outputs (maize, rainfed and irrigated) against remote-sensing and statistical reference data. The workflow covers converting NetCDF outputs to GeoTIFF, clipping and stacking rasters, computing zonal statistics per administrative unit, compiling results, and comparing simulated sowing date, harvest date, LAI, GPP and above-ground biomass / yield with observations.

**Author:** Pushkar Gaur

## Repository structure

```
notebooks/     All analysis notebooks (see workflow below)
requirements.txt
```

Input and output data are **not** included in this repository. The notebooks use paths relative to the parent of `notebooks/`, so place the data folders next to it:

```
project-root/
├── notebooks/          # this repo
├── data/               # raw inputs (remote sensing, climate, reference data)
├── data(LPJmL)/        # LPJmL NetCDF outputs
├── shape/              # administrative boundary shapefiles
├── tiffs/              # GeoTIFFs produced from NetCDF
├── raster(clip)/       # clipped rasters
├── stats/              # zonal statistics (CSV)
├── compiled values/    # compiled Excel tables
└── gpp graphs/         # figure output
```

## Workflow

| Step | Notebooks |
|---|---|
| 1. Data download | `dataDownload_gee.ipynb` (Google Earth Engine), `data_read_spam.ipynb`, `netcdf exploration.ipynb` |
| 2. NetCDF → GeoTIFF | `NC to tiff_*.ipynb` (agbm, agbm-cleaf, agbm-cpool, agbm-cso, evap_agbm, harvest, hd, lai, sd, swc) |
| 3. Raster processing | `clip raster.ipynb`, `stack raster.ipynb`, `RasterMean.ipynb`, `plot raster.ipynb`, `generate_crop.ipynb`, `shapeMerge.ipynb`, `grid_test.ipynb` |
| 4. Zonal statistics | `zonal_stats.ipynb`, `zonal_stats_masked.ipynb` |
| 5. Compilation | `dataCompilation.ipynb`, `newDataCompilation.ipynb`, `RSDataCompilation.ipynb`, `RSDataCompilation-mnthMean.ipynb`, `CASA data compilation.ipynb`, `compiled agbm.ipynb` |
| 6. Analysis & evaluation | `DataAnalysis_sd.ipynb`, `DataAnalysis_hd.ipynb`, `SowingDate_analysis.ipynb`, `growing season.ipynb`, `dataAnalysis_lai.ipynb`, `dataAnalysis_gpp-so.ipynb`, `dataAnalysis_agbm.ipynb`, `CSO_analysis.ipynb`, `LPJmL parameter analysis.ipynb`, `ClimateDataAnalysis.ipynb`, `statistics.ipynb`, `trendPlot.ipynb` |

## Setup

```bash
conda create -n spatial python=3.11
conda activate spatial
pip install -r requirements.txt
jupyter lab
```

`dataDownload_gee.ipynb` requires a Google Earth Engine account; run `ee.Authenticate()` once on first use.
