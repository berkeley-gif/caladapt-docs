.. _working-with-series:


************************
Working with Series
************************

A timeseries is a collection of rasters and is represented by the endpoint:

  .. sourcecode:: http

  http://api.cal-adapt.org/api/series


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


  :query sort: one of ``hit``, ``created-at``
  :query offset: offset number. default is 0
  :query limit: limit number. default is 30
  :reqheader Accept: the response content type depends on
                      :mailheader:`Accept` header
  :resheader Content-Type: this depends on :mailheader:`Accept`
                            header of request
  :statuscode 200: no error
  :statuscode 404: there's no user