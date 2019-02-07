.. _getting-started:


***************
Getting Started
***************

.. _authentication:

Authentication
-----------------

Currently the Cal-Adapt API does not require authentication. You do not need to sign up for a key to start working with the API. We plan to maintain the current level of open access to support a wide range of users. However, authentication may be implemented in the future to support throttled access for selected applications.


.. _entry-point:

Entry Point
-----------------

The entry point or API root is a starting point that provides an overview of all available data in the API. The entry point for the Cal-Adapt API is:

   .. sourcecode:: xml

       http://api.cal-adapt.org/api/

  
.. _browsable-api:

Browsable API View
--------------------

When you open the above entry point in a browser, you will see an easy to read, browsable view of the Cal-Adapt API. The browsable API view provides a quick overview of available data resources in the API and the URLs to access these data resources. This makes it easier and convenient to test requests and their returns in a web browser.


.. _data-formats:

Data Formats
-----------------

In a web browser by default, the API will return data as HTML. One way to request data in a different format is by adding the ``format`` query parameter to the URL.

   .. sourcecode:: xml

       http://api.cal-adapt.org/api/?format=json

The Cal-Adapt API supports the following data formats:

  * Raster and vector data

    * Browsable API view (api)
    * JavaScript Object Notation (json)
  * Raster data only

    * Comma Separated Values (csv)
    * GeoTIFF (tif.zip)
  * Vector data only

    * GeoJSON (geojson)
    * Keyhole Markup Language (kml)
    * Zipped KML files (kmz)

However, our preferred way to indicate data format (instead of adding ``format=json`` in the URL) is to use the appropriate HTTP Accept header in your requests, e.g.:

   .. sourcecode:: xml

       Accept: application/json


.. _pagination:

Pagination
-----------------

The API returns a paginated response for large datasets. Pagination links are provided as part of the content of the response e.g. ``"next": "http://api.cal-adapt.org/api/series/?page=2"``. The default number of records returned in each page is 10. The number of records returned in each page can be controlled by using ``pagesize`` query parameter.

  **Example Request**

   .. sourcecode:: http

       GET /api/series/
       Host: api.cal-adapt.org
       Accept: text/html

  **Response**

   .. sourcecode:: http

    HTTP 200 OK Vary: Accept
    Content-Type: text/html; charset=utf-8
    Allow: GET, HEAD, OPTIONS

    {
      "count": 259,
      "next": "http://api.cal-adapt.org/api/series/?page=2",
      "previous": null,
      "results": [
          {
            "name": "U.C. Merced Wildfire high population scenario CNRM-CM5 rcp45",
            "slug": "fire_CNRM-CM5_rcp45_H_mu",
            "url": "http://api.cal-adapt.org/api/series/fire_CNRM-CM5_rcp45_H_mu/",
            "begin": "1954-01-01T00:00:00Z",
            "end": "2100-12-31T00:00:00Z",
            "rasters": [
                "http://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_H_mu_1954/",
                "http://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_H_mu_1955/",
                "http://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_H_mu_1956/",
                ...
            ],
            "tags": [
                "fire"
            ]
          },
          {
            "name": "U.C. Merced Wildfire low population scenario CNRM-CM5 rcp45",
            "slug": "fire_CNRM-CM5_rcp45_L_mu",
            "url": "http://api.cal-adapt.org/api/series/fire_CNRM-CM5_rcp45_L_mu/",
            "begin": "1954-01-01T00:00:00Z",
            "end": "2100-12-31T00:00:00Z",
            "rasters": [
                "http://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_L_mu_1954/",
                "http://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_L_mu_1955/",
                "http://api.cal-adapt.org/api/rstores/fire_CNRM-CM5_rcp45_L_mu_1956/",
                ...
            ],
            "tags": [
                "fire"
            ]
          }
          ...
        ]
      }
