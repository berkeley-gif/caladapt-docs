.. _resources:


***************
Resources
***************

We refer to the data assets of an API as resources. They are represented by so-called endpoints referred to by an unambiguous URL.

.. _basic-principles:

Basic Principles
==================

* The API returns data formats according to the ``Accept``-field in the request header if possible. E.g. ``Accept: application/json`` if this particular format can be provided. Otherwise it will fall back to the HTML based browse-able API view.
* Be aware of the fact that there might be different flavors of returns that are covered by one single accept type. In this case the flavor can be determined with the ``?format=`` query parameter. E.g. ``?format=geojson`` will return GeoJSON.
* ``Accept: text/html`` will return a browse-able API view.
* The endpoint URL will return a paginated list view (e.g. ``/api/observations/``).
* Adding a unique identifier will return a single item view (e.g. ``/api/observations/LACM:Birds:15913/``) if applicable.


.. _entry-point:

Entry Point
==================

The entry point provides an overview over the available resources and actions. It is a starting point to navigate the API. It provides URLs for all endpoints

The entry point provides an overview over the available resources and
actions. It is a starting point to navigate the API. It provides URLs for
all endpoints including  meta data, data, and specific operations that can
be performed on the data (currently ``/api/search/``).

   The entry endpoint of the API.

   **Example Request**

   .. sourcecode:: http

       GET /api/ HTTP/1.1
       Host: ecoengine.berkeley.edu
       Accept: text/html

   **Response**

   .. sourcecode:: http

    HTTP 200 OK Vary: Accept
    Content-Type: text/html; charset=utf-8
    Allow: GET, HEAD, OPTIONS

    {
        "wieslander_vegetation_type_mapping": {
            "vtm_plot_data_tree_attributes": "https://ecoengine.berkeley.edu/api/vtmplots_trees/",
            "vtm_plot_data": "https://ecoengine.berkeley.edu/api/vtmplots/",
            "vtm_plot_data_brushes_attributes": "https://ecoengine.berkeley.edu/api/vtmplots_brushes/",
            "vtm_features": "https://ecoengine.berkeley.edu/api/vtmveg/"
        },
        "data": {
            "checklists": "https://ecoengine.berkeley.edu/api/checklists/",
            "sensors": "https://ecoengine.berkeley.edu/api/sensors/",
            "observations": "https://ecoengine.berkeley.edu/api/observations/",
            "photos": "https://ecoengine.berkeley.edu/api/photos/"
        },
        "actions": {
            "search": "https://ecoengine.berkeley.edu/api/search/"
        },
        "meta-data": {
            "footprints": "https://ecoengine.berkeley.edu/api/footprints/",
            "data_sources": "https://ecoengine.berkeley.edu/api/sources/"
        }
    }


Explore the browsable API `</api/>`_.
The browsable API provides a layer of additional documentation, a quick way
to get an overview over the data, as well as the possibility to test
URLs and requests and their returns conveniently in a web browser.
