---
layout: default
title: Data
parent: Resources
nav_order: 1
---

## 1. Data Resources

### 1.1 Sequence data

#### 1.1.1 GISAID

**What it is:** A database of viral genome sequences and associated metadata, best known for influenza and SARS-CoV-2 (EpiFlu and EpiCoV). It is the main repository for many influenza and SARS-CoV-2 sequences.

**Access:** Free, but you must [register](https://gisaid.org/) and agree to the Terms of Use. Access requests are reviewed, so allow some time.

**Notes:**
- The terms require you to acknowledge the originating and submitting laboratories for any data you use. GISAID provides an acknowledgement table and a data citation for download, so keep these with your analysis.
- Sequences cannot be redistributed. Share accession numbers (e.g. EPI_ISL IDs) rather than the sequences themselves.
- Check the terms before using the data in publications or releasing derived datasets.

#### 1.1.2 NCBI Viruses
**What it is:** The NCBI portal for virus sequence data, drawing on GenBank and RefSeq. It lets you search, filter (by host, country, collection date, sequence length, completeness, etc.), align and download sequences and metadata for any virus.

**Access:** Open, with no registration needed. Go to [ncbi.nlm.nih.gov/labs/virus](https://www.ncbi.nlm.nih.gov/labs/virus/).

**Command-line access:** The [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/docs/v2/) command-line tools are useful for reproducible, scripted downloads:

```bash
conda install -c conda-forge ncbi-datasets-cli
datasets download virus genome taxon "Zika virus" --complete-only
```

**Tips:**
- Record the date of download and the search/filters used, since the database changes daily.
- Metadata quality varies between submissions (especially dates and locations), so check before analysis.

#### 1.1.3 Pathoplexus

**What it is:** An open database for pathogen sequences and metadata, built on the Loculus software and designed to follow open-science principles. Sequences are linked to the international INSDC databases (GenBank, ENA, DDBJ). Data submitters can choose between fully open data and a short period of restricted use before release.

**Access:** [pathoplexus.org](https://pathoplexus.org/). Browsing and downloading open data is free. You may need an account to submit data or to access restricted-use data.

**Tips:**
- Check each dataset's usage terms before analysis or publication, particularly for restricted-use data.
- The range of pathogens covered is growing, so check the website for the current list.

### 1.2 Environmental data

#### 1.2.1 Copernicus

**What it is:** The European Union's Earth observation programme, which provides free and open data on the atmosphere, land, ocean and climate through several services. The two most relevant to us are:

- **Climate Data Store (CDS):** Hosts climate datasets including **ERA5**, the ECMWF global weather and climate reanalysis. It provides hourly estimates of many variables (temperature, precipitation, wind, humidity, etc.) with global coverage from 1940 onwards.
- **Copernicus Land Monitoring Service (CLMS):** Provides land use and land cover products, such as CORINE Land Cover (Europe) and global land cover maps, useful for characterising habitats and tracking environmental change.

**Access:** Free, with registration. Start from [copernicus.eu](https://www.copernicus.eu/), the [Climate Data Store](https://cds.climate.copernicus.eu/) and the [Land Monitoring Service](https://land.copernicus.eu/).

**Tips:**
- ERA5 can be downloaded programmatically with the `cdsapi` Python package, which is better than the web interface for reproducible, scripted downloads. **Only use `cdsapi` if the dataset is small, otherwise use DestinE (see next section)**
- Land cover products differ in coverage, resolution, class definitions and update year, so check these before choosing one and when combining products.
- Cite each dataset according to the licence and citation instructions on its page.

#### 1.2.2 DestinE / Earth Data Hub

**What it is:** Destination Earth (DestinE) is a European Union initiative producing high-resolution digital models of the Earth. The [Earth Data Hub](https://earthdatahub.destine.eu/) provides cloud-based access to analysis-ready datasets, so you can read subsets directly into Python (e.g. with `xarray`) instead of downloading large files. The datasets of most interest to us are:

- **ERA5:** Global weather and climate reanalysis (see section 1.2.1), with hourly temporal resolution.
- **Copernicus DEM:** A global digital elevation model, useful for terrain and elevation covariates.

Land use and land cover data are **not** available here. Use Copernicus (section 1.2.1) for these.

**Access:** Registration is required. Check the website for current access terms and the datasets available.

**Tips:**
- Subset by region and time period before loading to keep memory use manageable. You should pay careful attention to the tutorials on DestinE, before wasting your valuable free allowance!
- Cite the datasets according to the licence and citation instructions on each dataset page.

### 1.3 Livestock and wildlife data

#### 1.3.1 GLW4

**What it is:** The Gridded Livestock of the World (version 4), which provides gridded, high-resolution estimates of the global distribution of livestock. It covers cattle, poultry (chickens and ducks), pigs, buffalo, sheep and goats. It is useful as a covariate for models of disease transmission in animals and spillover.

**Access:** Data are published by the Food and Agriculture Organization of the United Nations (FAO). Start from the [FAO Livestock Systems page](https://www.fao.org/livestock-systems/en/) and check for the current download links and licence.

**Tips:**
- Densities are modelled estimates, so be cautious in areas with sparse input data.

#### 1.3.2 Global Lakes and Wetlands Database (GLWD)

**What it is:** A global, map-based database of lakes, rivers and wetlands. It is relevant to waterbird habitats and to the ecology of avian influenza and other waterbird-associated pathogens. The most recent version (GLWD v2) is a high-resolution raster that classifies wetlands into many types (e.g. freshwater marshes, peatlands, coastal wetlands) and also includes lakes and rivers.

**Access:** Free to download from the [HydroSHEDS website](https://www.hydrosheds.org/). Check the page for the current version and licence.

**Tips:**
- Wetland extent varies seasonally and between years, so treat the maps as an approximation.

#### 1.3.3 European Breeding Bird Atlas

**What it is:** The European Breeding Bird Atlas (EBBA2) provides standardised maps of the distribution and abundance of breeding bird species across Europe, compiled from national atlas data and surveys by volunteers. It is useful for describing the distribution of potential wild bird hosts.

**Access:** See the [EBBA2 website](https://ebba2.info/) (run by the European Bird Census Council) for maps and data requests.

**Tips:** Atlas data represent breeding season distributions, so they do not capture migration or winter distributions.

#### 1.3.4 BirdLife International

**What it is:** A global partnership of conservation organisations. Its [DataZone](https://datazone.birdlife.org/) hosts species factsheets and maps of bird species ranges, Important Bird and Biodiversity Areas (IBAs), and threat and conservation status.

**Access:** Factsheets and summaries are freely available. Spatial data (e.g. species range maps) are available on request for non-commercial research via a data request form. Check the licence and citation requirements.

#### 1.3.5 Seabird Tracking Database

**What it is:** A [community database](https://www.seabirdtracking.org/) run by BirdLife International that collates tracking data (GPS and other loggers) from seabirds around the world, showing where birds forage and migrate. It is useful for studying movement and contact between colonies and species.

**Access:** The data are owned by individual contributors. You can explore summaries openly, but access to the raw tracking data generally requires a request to the data owners via the database.