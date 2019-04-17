.. _raster-series:

Raster Series
=============
A raster series is a collection of individual rasters comprising an entire time series.


List Raster Series
------------------
.. http:get:: /api/series/

   List all available raster time series.

   :query slug: search series slugs containing the provided value
   :query name: search series names containing the provided value
   :query tags: filter on tags
   :query integer page: page number
   :query integer pagesize: number of records, default is 10


Raster Series Detail
--------------------
.. http:get:: /api/series/{slug}/

   Request an individual series with a provided slug. A slug is a URL friendly name of a resource in the API. Each climate dataset or resource has it's own unique slug. A resource slug is generally composed of ``{variable}_{period}_{model}_{scenario}``.

   **Example request**:

   .. code-block:: http

      GET /api/series/tasmax_year_CNRM-CM5_rcp45/ HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Response**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Vary: Accept
      Content-Type: application/json

      {
      "begin": "2006-01-01T00:00:00Z",
      "end": "2100-12-31T00:00:00Z",
      "name": "yearly average maximum temperature CNRM-CM5 RCP 4.5",
      "rasters": [
          "http://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2006/",
          "http://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2007/",
          "http://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2008/"
          ,
      ]
      "slug": "tasmax_year_CNRM-CM5_rcp45",
      "tags": [
          "climate",
          "tasmax",
          "temperature"
      ],
      "url": "http://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/"
      }

   :arg slug: series slug identifier


Time Series
-----------
.. http:get:: /api/series/{slug}/events/

   Return the entire time series for any location, with optional temporal and/or rolling aggregations applied. The response consists of ``columns``, ``data``, and ``index``.

   **Example request**:

   .. code-block:: http

      GET /api/series/tasmax_day_HadGEM2-ES_rcp85/events/?g=POINT(-121.46+38.58) HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Response**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Vary: Accept
      Content-Type: application/json

      {
      "data": [
          284.2241516113,
          283.9797973633,
          283.4098815918
          ,
      ],
      "index": [
          "2006-01-01T00:00:00Z",
          "2006-01-02T00:00:00Z",
          "2006-01-03T00:00:00Z"
          ,
      ],
      "name": "tasmax_day_HadGEM2-ES_rcp85"
      }

   :arg slug: series slug identifier
   :query g: a geometry (point, line, polygon) as GeoJSON, WKT, GML or KML
   :query stat: one of ``max``, ``mean``, ``median``, ``min``, ``sum`` for spatial aggregation by polygon/line provided by the ``g`` param, defaults to ``mean``
   :query freq: resampling frequency string such as ``M``, ``A``, ``10A``, or any `Pandas offset <http://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#dateoffset-objects>`_
   :query rolling: rolling statistic, one of ``max``, ``mean``, ``median``, ``min``, ``sum``
   :query integer window: rolling window size
   :query float thresh: only return values above a given threshold
   :query boolean imperial: use imperial units, defaults to false
   :query format: ``json`` or ``csv``
   :query integer pagesize: number of records, default is 10
   :reqheader Accept: the response content type depends on
                      :mailheader:`Accept` header
   :resheader Content-Type: this depends on :mailheader:`Accept`
                            header of request
   :statuscode 200: no error
   :statuscode 400: something is askew with the request, check the error message
   :statuscode 404: the slug may be incorrect
   :statuscode 500: something's wrong on our end

.. http:post:: /api/series/{slug}/events/

   Use POST when providing a feature set to return data for multiple locations.
   The same parameters as with GET are available.

   :query features: file upload to provide multiple geometries as part of a feature set, any `OGR supported <https://gdal.org/ogr_formats.html>`_ format or zip file

Return monthly data aggregated from daily values for a point location using
`freq`:

.. code-block:: http

  GET /api/series/tasmax_day_HadGEM2-ES_rcp85/events/?g=POINT(-121.46+38.58)&freq=M HTTP/1.1
  Host: api.cal-adapt.org
  Accept: application/json

**Response**:

.. code-block:: http

  HTTP/1.1 200 OK
  Vary: Accept
  Content-Type: application/json

  {
  "columns": [
      "min",
      "mean",
      "max",
      "std",
      "count"
  ],
  "data": [
      [
          275.4864807129,
          283.8988342285,
          288.8237304688,
          3.3650608063,
          31
      ],
      [
          283.4172058105,
          290.7746276855,
          298.8256835938,
          3.4072315693,
          28
      ],
      [
          286.8976745605,
          293.8493652344,
          300.5709533691,
          4.2584190369,
          31
      ]
      ,
  ],
  "index": [
      "2006-01-31T00:00:00Z",
      "2006-02-28T00:00:00Z",
      "2006-03-31T00:00:00Z"
      ,
  ]}


List Series Rasters
-------------------
.. http:get:: /api/series/{slug}/rasters/

   List all rasters in the series. See the :ref:`raster-store` description.

   **Example request**:

   .. code-block:: http

      GET /api/series/tasmax_year_CNRM-CM5_rcp45/rasters/ HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Example response**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Allow: GET, POST, OPTIONS
      Content-Type: application/json
      Vary: Accept

      {
        "count": 95,
        "next": "https://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/rasters/?page=2",
        "previous": null,
        "results": [{
            "id": 10521,
            "tileurl": "https://api.cal-adapt.org/tiles/tasmax_year_CNRM-CM5_rcp45_2006/{z}/{x}/{y}.png",
            "url": "https://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2006/",
            "image": "https://api.cal-adapt.org/media/img/tasmax_year_CNRM-CM5_rcp45_r1i1p1_2006.LOCA_2016-04-02.16th.CA_NV.tif",
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
        }, {
            "id": 10522,
            "tileurl": "https://api.cal-adapt.org/tiles/tasmax_year_CNRM-CM5_rcp45_2007/{z}/{x}/{y}.png",
            "url": "https://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2007/",
            "image": "https://api.cal-adapt.org/media/img/tasmax_year_CNRM-CM5_rcp45_r1i1p1_2007.LOCA_2016-04-02.16th.CA_NV.tif",
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
        }
        ,
        ]
      }

   :arg slug: series slug identifier
   :query g: a geometry (point, line, polygon) as GeoJSON, WKT, GML or KML
   :query bbox: a bounding box in the form of x1,y1,x2,y2
   :query pagesize: number of records, default is 10
   :query format: ``json`` or ``tif.zip``
   :query stat: one of ``mean``, ``max``, ``min``, ``count``, ``median``, ``std``, ``var`` for spatial aggregation by polygon/line geometry provided by the ``g`` param.
   :reqheader Accept: the response content type depends on
                      :mailheader:`Accept` header
   :resheader Content-Type: this depends on :mailheader:`Accept`
                            header of request
   :statuscode 200: no error
   :statuscode 400: something is askew with the request, check the error message
   :statuscode 404: the slug may be incorrect
   :statuscode 500: something's wrong on our end

.. http:get:: /api/series/{slug}/{begin}/{end}/

   Filter series rasters from start to end date

   :arg slug: series slug identifier
   :arg date begin: starting date
   :arg date end: ending date

A time slice or subset can be retrieved by adding start and end dates to the URL. ::

    curl https://api.cal-adapt.org/api/series/tasmax_year_CNRM-CM5_rcp45/2030-01-01/2040-01-01/
