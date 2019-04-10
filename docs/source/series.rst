.. _working-with-series:

************************
Working with Series
************************

A Raster Series list is a collection of individual raster time series which is represented by this endpoint:

  .. sourcecode:: xml

    https://api.cal-adapt.org/api/series/{slug}/


Slug
-----

A slug is a URL friendly name of a resource in the API. Each climate dataset or resource has it's own unique slug. A resource slug is generally composed of ``{variable}_{period}_{model}_{scenario}``.

  .. sourcecode:: xml

    https://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/


.. _filtering-series:

Filtering Series
--------------------

The series endpoint supports searching by ``name``.

  .. sourcecode:: xml

    https://api.cal-adapt.org/api/series/?name=yearly+average+maximum+temperature

Or by ``slug``.

  .. sourcecode:: xml

    https://api.cal-adapt.org/api/series/?slug=tasmax_year_CCSM4


Get Time Slices
------------------

The complete timeseries can be retrieved by adding ``rasters/`` to the URL.

  .. sourcecode:: xml

    https://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/rasters/

A time slice can be retrieved by adding start and end dates to the URL.

  .. sourcecode:: xml

    https://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/2030-01-01/2040-01-01/


Get Data for a Location
-------------------------

The following example shows an example of requesting timeseries data for a location. The response consists of ``count`` (number of records), ``next`` (link to next page, see :ref:`pagination`), ``results`` (array of JSON objects for each timestep). Among other fields each timestep contains fields  ``image`` (data value), ``event`` (date), and ``units`` (units of data value).

.. http:get:: /api/series/{slug}/rasters/?g=POINT(-121.46+38.58)

   Data for annual averages of Maximum Temperature projections at location (longitude -121.46, latitude 38.58) for CNRM-CM5 model and RCP 4.5 scenario.

   **Example request**:

   .. sourcecode:: http

      GET /api/series/tasmax_year_CNRM-CM5_rcp45/rasters/?g=POINT(-121.46+38.58) HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Allow: GET, POST, OPTIONS
      Content-Type: application/json
      Vary: Accept

      {
        "count": 95,
        "next": "https://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/rasters/?g=POINT%28-121.46+38.58%29&page=2",
        "previous": null,
        "results": [
        {
            "id": 10521,
            "tileurl": "https://api.cal-adapt.org/tiles/tasmax_year_CNRM-CM5_rcp45_2006/{z}/{x}/{y}.png",
            "url": "https://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2006/",
            "image": 297.9866027832031,
            "width": 179,
            "height": 195,
            "geom": "POLYGON ((-124.5625 31.5625, -113.375 31.5625, -113.375 43.75, -124.5625 43.75, -124.5625 31.5625))",
            "event": "2006-01-01",
            "srs": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0],UNIT[\"degree\",0.0174532925199433],AUTHORITY[\"EPSG\",\"4326\"]]",
            "minval": 279.1251220703125,
            "maxval": 307.180908203125,
            "nodata": 1.0000000150474662e+30,
            "xpixsize": 0.0625,
            "ypixsize": -0.0625,
            "name": "yearly average maximum temperature CNRM-CM5 RCP 4.5",
            "slug": "tasmax_year_CNRM-CM5_rcp45_2006",
            "units": "K"
        },
        {
            "id": 10522,
            "tileurl": "https://api.cal-adapt.org/tiles/tasmax_year_CNRM-CM5_rcp45_2007/{z}/{x}/{y}.png",
            "url": "https://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2007/",
            "image": 297.7721862792969,
            "width": 179,
            "height": 195,
            "geom": "POLYGON ((-124.5625 31.5625, -113.375 31.5625, -113.375 43.75, -124.5625 43.75, -124.5625 31.5625))",
            "event": "2007-01-01",
            "srs": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0],UNIT[\"degree\",0.0174532925199433],AUTHORITY[\"EPSG\",\"4326\"]]",
            "minval": 278.38330078125,
            "maxval": 307.52490234375,
            "nodata": 1.0000000150474662e+30,
            "xpixsize": 0.0625,
            "ypixsize": -0.0625,
            "name": "yearly average maximum temperature CNRM-CM5 RCP 4.5",
            "slug": "tasmax_year_CNRM-CM5_rcp45_2007",
            "units": "K"
        },
      ]}

   :query g: a geometry (point, line, polygon) as GeoJSON, WKT, GML or KML
   :query bbox: a bounding box in the form of x1,y1,x2,y2
   :query pagesize: number of records, default is 10
   :query format: one of ``json``, ``csv``, ``tif.zip``
   :query stat: one of ``mean``, ``max``, ``min``, ``count``, ``median``, ``std``, ``var`` for spatial aggregation by polygon/line geometry provided by the ``g`` param.
   :query periods: number of periods to resample to, i.e. from annual to decadal
   :reqheader Accept: the response content type depends on
                      :mailheader:`Accept` header
   :resheader Content-Type: this depends on :mailheader:`Accept`
                            header of request
   :statuscode 200: no error
   :statuscode 400: something is askew with the request, check the error message
   :statuscode 404: the slug may be incorrect
   :statuscode 500: something's wrong on our end
