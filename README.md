Wildfires in Alaska, 1992 to 2015

This project investigates wildfire activity in the United States between 1992 and 2015, with a specific focus on Alaska. The goal was to prepare a report for public authorities, highlight the environmental implications of wildfire activity, and suggest straightforward strategic recommendations that could support future planning.

The work is based on exploratory analysis in Python and a Power BI report built on several datasets, the main dataset was provided during my training at DataScientest, it features artificial difficulty (traps) that were included for training purposes. Since the original files were internal, they are not included in the repository. The structure and content of each table are described in the data folder so that the project can be understood without redistributing the raw material.

The analysis covers national patterns and then narrows down to Alaska to show what makes the state an outlier compared with the rest of the country.

Objectives

- I structured the project around several practical questions :
- What are the overall trends in wildfire activity across the United States during the period?
- How Alaska differs from the rest of the country?
- What the main ignition causes are, and how these vary by region and season?
- Which environmental and demographic indicators can help explain the vulnerability of specific areas in Alaska?
- How infrastructure, distance, and geography affect the state’s capacity to detect and respond to fires?
- What insights can help decision makers allocate resources more effectively?

Main Findings

A few points stood out clearly during the analysis:

- Alaska’s ignition profile is unusual.
- Lightning accounts for the majority of fires in Alaska. This is not the case in most other states, where human activity generally dominates.
- Fire size patterns differ sharply from the national picture.
- Alaska sees fewer incidents but significantly larger burned areas, most fires are Mega-Fires (G rank). Geography and limited accessibility slow down early detection, which gives fires more time to expand.
- Areas with permafrost, ecologically sensitive zones, and sparsely populated regions tend to overlap with documented fire activity. Some of these regions are difficult to protect once a fire starts.

Infrastructure coverage is uneven.
- Mapping Alaska’s firefighting departments and operational zones shows several large regions without nearby facilities. These gaps correspond with long response times as well as large burn areas. These areas are mostly away from the population, fires are left to burn despite high CO2 emissions.

Certain years show clear crisis patterns.
Especially the year 2004 and 20015.

Recommendations

The recommendations are straightforward and based directly on the observations.

- Reinforce firefighting presence in interior and western Alaska, where distances between facilities are large and fires tend to expand rapidly.
- Concentrate monitoring efforts, especially during the peak lightning season.
- Prioritize the protection of zones that combine environmental sensitivity and a history of large events.
- Improve early detection using satellite and drone monitoring, since ground-based detection is limited in remote areas.
- Focus public campaigns only where human-driven fires matter. In Alaska this is marginal, so most prevention should rely on weather and lightning forecasting rather than behavioral messaging.

Dataset Information

The data used in this project came from internal course material and cannot be redistributed. A summary of each table is available in data/README.md, including column descriptions and equivalent public sources when possible.

The main tables include:

- Wildfire incidents for the whole United States
- Alaska weather observations from 1992 to 2015
- Fire departments and operational metadata
- Alaska environmental and demographic indicators
- Reference measurements for state land areas

Repository Structure

Wildfires_Alaska

data :
Descriptions of the source datasets (WIP)

notebooks :
Exploratory analysis and geospatial work

powerbi :
Screenshots and documentation for the dashboard


README.md

Tools Used

Python (pandas, geopandas, matplotlib, seaborn, numpy...) for analysis and mapping.
Power Querry for transformative work, I had some issues with dtypes on import and had to re-transform for power bi.
Power BI Desktop for the dashboard and final reporting.
Excel for preliminary inspection and creation of new datasets to enrich the provided one.

Sources

Primary Dataset
FPA-FOD (1992–2015) – USDA Forest Service
USDA Forest Service – FPA-FOD
(Modified version)
https://research.fs.usda.gov/firelab/products/dataandtools/us-wildfires

Environmental & Climatic Data
ERA5 Reanalysis (ECMWF) – Copernicus Climate Data Store
Copernicus CDS – ERA5

Geospatial & Territorial Data
Alaska Geoportal
Alaska Mapped
https://www.alaskamapped.org/

Surface Area Data
INSEE & Eurostat
INSEE
https://www.insee.fr/fr/accueil
Eurostat
https://ec.europa.eu/eurostat

Scientific Literature
Kasischke et al. (2012), Turetsky et al. (2015)
Used to estimate CO₂ emissions from boreal fires (approx. 30 tons/hour).
Nature article on permafrost emissions
https://www.nature.com/articles/nature14338


Biodiversity & Protection Zones
IUCN Red List & US Fish & Wildlife Service
IUCN Red List
https://www.iucnredlist.org/
U.S. FWS – National Wildlife Refuges
