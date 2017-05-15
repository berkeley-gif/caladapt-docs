.. _data-catalog:


***************
Data Catalog
***************

We refer to the datasets in the Cal-Adapt API as resources. Each resource is represented by a unique endpoint (URL). The following is a list of climate datasets in the Cal-Adapt API. We are actively adding new resources to the API so this list may not reflect the most up to date information.


Climate Variables
-------------------

  * LOCA downscaled climate projections from Scripps Institution of Oceanography, UC San Diego (`Pierce et al, 2014 <http://journals.ametsoc.org/doi/abs/10.1175/JHM-D-14-0082.1>`_). Data is available for 10 GCMs (Global Climate Model) and 2 RCPs-4.5 and 8.5 (Representatitve Concentration Pathways).

    * Maximum Temperature ``tmax``
    * Minimum Temperature ``tmin``
    * Precipitation ``precip``

  * Climate variables produced by the Variable Infiltration Capacity (VIC) model using downscaled LOCA data. 10 GCM's and 2 RCPs.

    * Snow Water Equivalence ``swe``

  * Gridded historical observed climate data from UW Hydro | Computational Hydrology (`Livneh et al, 2015 <http://www.nature.com/articles/sdata201542>`_)

    * Maximum Temperature ``tmax``
    * Minimum Temperature ``tmin``
    * Precipitation ``precip``

  * Climate variables produced by the Variable Infiltration Capacity (VIC) model using gridded historical observed Livneh data.

    * Snow Water Equivalence ``swe``

  * Sea Level Rise (CalFloD-3D) for San Francisco Bay, Sacramento-San Joaquin Delta and California Coast from UC Berkeley (`Radke et al, 2016 <http://www.energy.ca.gov/publications/displayOneReport.php?pubNum=CEC-500-2017-008>`_). ``slr_sfbay`` ``slr_delta`` ``slr_coast``

  * Widlfire from UC Merced. 10 GCMs, 2 RCPs and 3 scenarios  ``fire``



Global Climate Models
-----------------------
    
    * ACCESS1-0 - Commonwealth Scientific and Industrial Research Organization (CSIRO) and Bureau of Meteorology (BOM) Australia  
    * CanESM2 - Canadian Centre for Climate Modelling and Analysis
    * CCSM4 - University of Miami - RSMAS
    * CESM1-BGC - Community Earth System Model Contributors
    * CMCC-CMS - Centro Euro-Mediterraneo per I Cambiamenti Climatici
    * CNRM-CM5 - Centre National de Recherches Météorologiques/ Centre Européen de Recherche et Formation Avancée en Calcul Scientifique
    * GFDL-CM3 - NOAA Geophysical Fluid Dynamics Laboratory
    * HadGEM2-CC - Met Office Hadley Centre
    * HadGEM2-ES - Met Office Hadley Centre and Instituto Nacional de Pesquisas Espaciais
    * MIROC5 - Atmosphere and Ocean Research Institute (The University of Tokyo), National Institute for Environmental Studies, and Japan Agency for Marine-Earth Science and Technology


Scenarios
------------
  
  * RCP 4.5
  * RCP 8.5
  * Historical


Vector Data
-------------

In addition to climate data, the Cal-Adapt API also has endpoints for vector datasets representing administrative and hydrological boundaries and the LOCA model grid. 

