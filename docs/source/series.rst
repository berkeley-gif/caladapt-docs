.. _working-with-series:


************************
Working with Series
************************

A timeseries is a collection of rasters and is represented by the endpoint:

  .. sourcecode:: xml

    http://api.cal-adapt.org/api/series/


Slug
-----

A slug is a URL friendly name of a resource in the API. Each climate dataset or resource has it's own unique slug.

  .. sourcecode:: xml

    http://api.cal-adapt.org/api/series/<slug>

A resource slug is generally composed of ``variable_period_model_scenario``.


Searching for a Resource
---------------------------


Temporal Aggregation
-------------------------



Query Parameters
------------------

The following query parameters can be used with the ``series`` endpoint. 

.. http:get:: http://api.cal-adapt.org/api/series/<slug>

   The timeseries for a climate variable.

   **Example request**:

   .. sourcecode:: http

      GET /api/tasmax_year_CNRM-CM5_rcp45/
      Host: api.cal-adapt.org
      Accept: application/json

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Vary: Accept
      Content-Type: text/javascript

      [
        {
          "post_id": 12345,
          "author_id": 123,
          "tags": ["server", "web"],
          "subject": "I tried Nginx"
        },
        {
          "post_id": 12346,
          "author_id": 123,
          "tags": ["html5", "standards", "web"],
          "subject": "We go to HTML 5"
        }
      ]

   :query g: a geometry object
   :query pagesize: number of records. default is 10
   :query format: ``json``, ``csv``, ``tif.zip``, ``img.zip``
   :reqheader Accept: the response content type depends on
                      :mailheader:`Accept` header
   :resheader Content-Type: this depends on :mailheader:`Accept`
                            header of request
   :statuscode 200: no error
   :statuscode 404: there's no timeseries with this slug