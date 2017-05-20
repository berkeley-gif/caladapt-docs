.. _working-with-raster-store:


**************************
Working with Raster Store
**************************

A Raster Store is an individual raster and is represented by the endpoint:

  .. sourcecode:: xml

    http://api.cal-adapt.org/api/rstores/<slug>/


Slug
-----

A slug is a URL friendly name of a resource in the API. Each climate dataset or resource has it's own unique slug. A resource slug is generally composed of ``{variable}_{period}_{model}_{scenario}_{timestep}``.

  .. sourcecode:: xml

    http://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2030/
