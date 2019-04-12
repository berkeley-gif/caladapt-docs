Getting Started
===============


Authentication
--------------
Currently the Cal-Adapt API does not require authentication. You do not need to sign up for a key to start working with the API. We plan to maintain the current level of open access to support a wide range of users. However, authentication may be implemented in the future to support throttled access for selected applications.


Entry Point
-----------
The entry point or API root is a starting point that provides an overview of all available data in the API. The entry point for the Cal-Adapt API is at https://api.cal-adapt.org/api/. ::

   curl https://api.cal-adapt.org/api/

  
Browsable API View
------------------
When you visit the above entry point in a browser, you will see an easy to read, browsable view of the Cal-Adapt API. The browsable API view provides a quick overview of available data resources in the API and the URLs to access these data resources. This makes it easier and convenient to test requests and their returns in a web browser.


Representations
---------------
The Cal-Adapt API supports the following representations or data formats listed
with their content type followed by format identifier:

  * Raster and vector data

    * Browsable API view ``text/html`` ``api``
    * JavaScript Object Notation ``application/json`` ``json``

  * Raster data only

    * Comma Separated Values ``text/csv`` ``csv``
    * Zipped GeoTIFF ``application/zip`` ``tif.zip``

  * Vector data only

    * GeoJSON ``application/vnd.geo+json`` ``geojson``
    * Keyhole Markup Language ``application/vnd.google-earth.kml+xml`` ``kml``
    * Zipped KML files ``application/vnd.google-earth.kmz`` ``kmz``

The HTTP Accept header is used in performing content negotiation. The server
will return JSON when a client does not specify. The following command confirms
the `Contenty-Type: application/json` header in the response. ::

    curl -IH 'Accept: application/json' https://api.cal-adapt.org/api/

.. code-block:: http

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

Or, HTML which returns the browsable API page. ::

    curl -IH 'Accept: text/html' https://api.cal-adapt.org/api/

.. code-block:: http

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: text/html; charset=utf-8

If necessary, content negotiation can be overridden by adding the ``format``
query parameter to the URL like https://api.cal-adapt.org/api/?format=json.


Pagination
----------
The API returns a paginated response for large datasets. Pagination links are provided as part of the content of the response so consumers can fetch additional pages as needed with the `next` property which links to https://api.cal-adapt.org/api/series/?page=2. The default number of records returned per page is 10. The number of records returned in each page can be controlled by using ``pagesize`` query parameter.

  **Example Request**

   .. code-block:: http

       GET /api/series/ HTTP/1.1
       Host: api.cal-adapt.org
       Accept: application/json

  **Response**

   .. code-block:: json

    {
      "count": 259,
      "next": "https://api.cal-adapt.org/api/series/?page=2",
      "previous": null,
      "results": [
          {
            "name": "U.C. Merced Wildfire high population scenario CNRM-CM5 rcp45",
            "slug": "fire_CNRM-CM5_rcp45_H_mu",
            "url": "https://api.cal-adapt.org/api/series/fire_CNRM-CM5_rcp45_H_mu/",
            "begin": "1954-01-01T00:00:00Z",
            "end": "2100-12-31T00:00:00Z",
            "rasters": [
                "https://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_H_mu_1954/",
                "https://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_H_mu_1955/",
                "https://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_H_mu_1956/"
                ,
            ],
            "tags": [
                "fire"
            ]
          },
          {
            "name": "U.C. Merced Wildfire low population scenario CNRM-CM5 rcp45",
            "slug": "fire_CNRM-CM5_rcp45_L_mu",
            "url": "https://api.cal-adapt.org/api/series/fire_CNRM-CM5_rcp45_L_mu/",
            "begin": "1954-01-01T00:00:00Z",
            "end": "2100-12-31T00:00:00Z",
            "rasters": [
                "https://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_L_mu_1954/",
                "https://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_L_mu_1955/",
                "https://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_L_mu_1956/"
                ,
            ],
            "tags": [
                "fire"
            ]
          }
          ,
        ]
      }
