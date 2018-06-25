.. _data-catalog:


***************
Data Catalog
***************

We refer to the datasets in the Cal-Adapt API as resources. Each resource is represented by a unique endpoint (URL). The following is a list of climate datasets in the Cal-Adapt API. We are actively adding new resources to the API so this list may not reflect the most up to date information.


.. _climate-variables:

Climate Variables
-------------------

  * LOCA downscaled climate projections from Scripps Institution of Oceanography, UC San Diego (`Pierce et al, 2014 <http://journals.ametsoc.org/doi/abs/10.1175/JHM-D-14-0082.1>`_).

    * Maximum Temperature ``tasmax``, Minimum Temperature ``tasmin``, Precipitation ``precip``
    * Daily and annual averages
    * 10 GCMs, 3 scenarios, Envelope

  * Climate variables produced by the Variable Infiltration Capacity (VIC) model using downscaled LOCA data.

    * Snow Water Equivalence ``swe``
    * Monthly averages
    * 10 GCMs, 3 scenarios

  * Gridded historical observed climate data from UW Hydro | Computational Hydrology (`Livneh et al, 2015 <http://www.nature.com/articles/sdata201542>`_)

    * Maximum Temperature ``tasmax``, Minimum Temperature ``tasmin``, Precipitation ``precip``
    * Daily and annual averages

  * Climate variables produced by the Variable Infiltration Capacity (VIC) model using gridded historical observed Livneh data.

    * Snow Water Equivalence ``swe``
    * Monthly averages

  * Sea Level Rise (CalFloD-3D) for San Francisco Bay, Sacramento-San Joaquin Delta and California Coast from UC Berkeley (`Radke et al, 2016 <http://www.energy.ca.gov/publications/displayOneReport.php?pubNum=CEC-500-2017-008>`_).

    * ``slr_sfbay`` ``slr_delta`` ``slr_coast``
    * SLR scenarios

  * Widlfire from UC Merced (LeRoy Westerling)

    * ``fire``
    * Annual averages

  * Bias-corrected Streamflows for 11 locations (Scripps Institution of Oceanography)

    * ``streamflow``
    * Monthly averages

  * Extended drought (Scripps Institution of Oceanography)

    * ``drought``
    * Daily data for two scenarios that portray 20 year drought conditions.

.. _gcm:

Global Climate Models (GCM)
----------------------------

The following GCMs have been selected by California state agencies as priority models for Fourth Assessment Research. Data for these models is available through the cal-Adapt API. Downscaled data for 22 other GCMs is available as NetCDF files from the `Cal-Adapt Data Server <http://albers.cnr.berkeley.edu/data/>`_.

    * ``ACCESS1-0`` - Commonwealth Scientific and Industrial Research Organization (CSIRO) and Bureau of Meteorology (BOM) Australia
    * ``CanESM2`` - Canadian Centre for Climate Modelling and Analysis
    * ``CCSM4`` - University of Miami - RSMAS
    * ``CESM1-BGC`` - Community Earth System Model Contributors
    * ``CMCC-CMS`` - Centro Euro-Mediterraneo per I Cambiamenti Climatici
    * ``CNRM-CM5`` - Centre National de Recherches Météorologiques/ Centre Européen de Recherche et Formation Avancée en Calcul Scientifique
    * ``GFDL-CM3`` - NOAA Geophysical Fluid Dynamics Laboratory
    * ``HadGEM2-CC`` - Met Office Hadley Centre
    * ``HadGEM2-ES`` - Met Office Hadley Centre and Instituto Nacional de Pesquisas Espaciais
    * ``MIROC5`` - Atmosphere and Ocean Research Institute (The University of Tokyo), National Institute for Environmental Studies, and Japan Agency for Marine-Earth Science and Technology


.. _scenario:

Scenarios
------------

Representatitve Concentration Pathways (RCP). RCP references - `The Beginner's Guide to Representative Concentration Pathways <https://skepticalscience.com/rcp.php>`_ , `IPCC <http://sedac.ipcc-data.org/ddc/ar5_scenario_process/RCPs.html>`_

  * ``rcp45`` - RCP 4.5 (Emissions peak around 2040, then decline)
  * ``rcp85`` - RCP 8.5 (Emissions continue to rise strongly through 2050 and plateau)
  * ``historical`` - Historical


.. _period:

Period
-----------

Different temporal aggregations are available for climate variables through the API. See :ref:`filtering-series` to find out what's available in the API.

  * ``year`` - Annual averages
  * ``month`` - Monthly averages
  * ``day`` - Daily values

.. _vector-data:

Vector Data
-------------

In addition to climate data, the Cal-Adapt API also has endpoints for vector datasets representing administrative boundaries, hydrological boundaries and the LOCA model grid.

    * ``locagrid`` - Model Grid (1/16° - Approximately 6 km)
    * ``counties`` - California counties
    * ``hydrounits`` - Watersheds (HUC10)
    * ``censustracts`` - Census Tracts with CalEnviroScreen 2.0 scores
    * ``cdistricts`` - 114th congressional districts
    * ``place`` - Incorporated & census designated places, 2015
    * ``irwm`` - Integrated Regional Water Management (IRWM) Regions
    * ``wecc-load-area`` - SWITCH Load Zones
    * ``climregions`` - Climate Zones
    * ``electricutilities`` -  Investor and public owned electrical utilities

