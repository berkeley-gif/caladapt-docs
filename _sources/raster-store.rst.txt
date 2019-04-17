.. _raster-store:

Raster Store
============
A Raster Store is an individual raster file and associated information like
spatial resolution, coordinate system reference, and bounding box.


List Raster Stores
------------------
.. http:get:: /api/rstores/

   List all raster stores.

   :query name: search raster names containing the provided value
   :query integer page: page number
   :query integer pagesize: number of records, default is 10


Raster Store Detail
-------------------
.. http:get:: /api/rstores/{slug}/

   Request an individual raster with a provided slug. A slug is a URL friendly
   name of a resource in the API. Each climate dataset or resource has its own
   unique slug. A resource slug is generally composed of ``{variable}_{period}_{model}_{scenario}_{timestep}``.

   Response fields include ``image`` (raster file link), ``event`` (date), and ``units`` (unit of measurement for pixel values). Image statistics for ``min`` and ``max`` with regard to the ``nodata`` value, and dimensions ``xpixsize`` ``ypixsize``. Map tiles can be requested with the url template at ``tileurl``.

   **Example request**:

   .. code-block:: http

      GET /api/rstores/tasmax_year_CNRM-CM5_rcp45_2030/ HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Example response**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Allow: GET, POST, OPTIONS
      Content-Type: application/json
      Vary: Accept

      {
        "event": "2030-01-01",
        "geom": {
            "coordinates": [
                [
                    [
                        -124.5625,
                        31.5625
                    ],
                    [
                        -113.375,
                        31.5625
                    ],
                    [
                        -113.375,
                        43.75
                    ],
                    [
                        -124.5625,
                        43.75
                    ],
                    [
                        -124.5625,
                        31.5625
                    ]
                ]
            ],
            "type": "Polygon"
        },
        "height": 195,
        "id": 10545,
        "image": "http://api.cal-adapt.org/media/img/tasmax_year_CNRM-CM5_rcp45_r1i1p1_2030.LOCA_2016-04-02.16th.CA_NV.tif",
        "maxval": 307.184326171875,
        "minval": 278.8943786621094,
        "name": "yearly average maximum temperature CNRM-CM5 RCP 4.5",
        "nodata": 1.0000000150474662e+30,
        "slug": "tasmax_year_CNRM-CM5_rcp45_2030",
        "srs": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0],UNIT[\"degree\",0.0174532925199433],AUTHORITY[\"EPSG\",\"4326\"]]",
        "tileurl": "http://api.cal-adapt.org/tiles/tasmax_year_CNRM-CM5_rcp45_2030/{z}/{x}/{y}.png",
        "units": "K",
        "url": "http://api.cal-adapt.org/api/rstores/tasmax_year_CNRM-CM5_rcp45_2030/",
        "width": 179,
        "xpixsize": 0.0625,
        "ypixsize": -0.0625
      }

   :arg slug: raster slug identifier
