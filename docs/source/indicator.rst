Climate Indicators
==================


Cooling Degree Days and Heating Degree Days
-------------------------------------------
Cooling Degree Days (CDD) and Heating Degree Days (HDD) are a measure of energy demand for cooling and heating of buildings. They are defined as the number of degrees above or below a reference temperature. See the `degree days tool <http://cal-adapt.org/tools/degree-days/>`_ for more information and charting of the available data.

.. http:get:: /api/series/{slug}/hdd/

   Return heating degree days for any location.

.. http:get:: /api/series/{slug}/cdd/

   Return cooling degree days for any location.

   **Example request**:

   .. code-block:: http

      GET /api/series/tasmax_day_HadGEM2-ES_rcp85/cdd/?g=POINT(-121.46+38.59)&freq=A HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Example response**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Allow: GET, POST, OPTIONS
      Content-Type: application/json
      Vary: Accept

      {
      "data": [
          1272.4594726562,
          2066.6245117188,
          1458.0538330078,
          1674.4998779297
          ,
      ],
      "index": [
          "2006-12-31T00:00:00Z",
          "2007-12-31T00:00:00Z",
          "2008-12-31T00:00:00Z",
          "2009-12-31T00:00:00Z",
          ,
      ]}

   :arg slug: series slug identifier for daily tasmax or tasmin
   :query g: a geometry (point, line, polygon) as GeoJSON, WKT, GML or KML
   :query freq: resampling frequency string such as ``M``, ``A``, ``10A``, or any `Pandas offset <http://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#dateoffset-objects>`_
   :query float thresh: the reference temperature in F, defaults to ``65``


Extreme Precipitation
---------------------
Extreme precipitation events can be characterized using Extreme Value Analysis (EVA) by return levels, including confidence intervals, using the peak over threshold methodology. See the `extreme precipitation tool <http://cal-adapt.org/tools/extreme-precipitation/>`_ for more information and charting of the available data.

.. http:get:: /api/series/{slug}/pot/

   Response fields include ``returnlevels``, ``threshold``, and ``units`` (unit of measurement). The return levels are summarized over historic, mid, and end of century time frames. Each return interval is a 3-item array of the lower, estimated return level, and upper confidence interval.

   **Example request**:

   .. code-block:: http

      GET /api/series/pr_day_ACCESS1-0_rcp45/pot/?g=POINT(-121.4687+38.5938)&duration=2 HTTP/1.1
      Host: api.cal-adapt.org
      Accept: application/json

   **Example response**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Allow: GET, POST, OPTIONS
      Content-Type: application/json
      Vary: Accept

      {
      "returnlevels": {
          "1961-10-01:1990-09-30": {
              "10": [ 3.3738083898103706, 3.9522201904266527, 5.228567088406137 ],
              "100": [ 4.792120480767816, 6.491227596207121, 11.655569842787486 ],
              "2": [ 2.317027627106765, 2.5667466512434016, 2.941214643156155 ],
              "20": [ 3.781685742237907, 4.640839376130399, 6.677332244692823 ],
              "5": [ 2.9107509896073562, 3.321044449279986, 4.080450921786112 ],
              "50": [ 4.368586837537248, 5.648252163486491, 9.185085270172545 ],
              "n": 159
          },
          "2035-10-01:2064-09-30": {
              "10": [ 3.7262371212589867, 4.236568397086659, 5.240493845112521 ],
              "100": [ 4.906061402196474, 6.0225286812315595, 9.111781051084918 ],
              "2": [ 2.688362812028139, 2.9617466455337116, 3.315414408012187 ],
              "20": [ 4.134337164339881, 4.778850804514478, 6.252823005631932 ],
              "5": [ 3.312975478107658, 3.690233369085343, 4.342160397675551 ],
              "50": [ 4.571528643603971, 5.4895406091554895, 7.7864184564943955 ],
              "n": 175
          },
          "2070-10-01:2099-09-30": {
            "10": [ 4.241220088665857, 5.0994935705499715, 6.9916568467598665 ],
            "100": [ 6.244111144979032, 8.769602618538272, 16.754704790152964 ],
            "2": [ 2.820991602527356, 3.1581853987832025, 3.650831557730822 ],
            "20": [ 4.851689971070942, 6.081585627582591, 9.144602394922993 ],
            "5": [ 3.631161165606033, 4.209052130230058, 5.315306960831256 ],
            "50": [ 5.653315714995296, 7.536659927706938, 12.944282870291804 ],
            "n": 165
          },
          "threshold": 1.0,
      },
      "units": "inches"
      }

   :arg slug: series slug identifier
   :query g: a geometry (point, line, polygon) as GeoJSON, WKT, GML or KML
   :query stat: one of ``max``, ``mean``, ``median``, ``min``, ``sum`` for spatial aggregation by polygon/line provided by the ``g`` param, defaults to ``mean``
   :query integer duration: duration of extreme event in days
   :query intervals: comma separated list of return intervals, returns levels for 2, 5, 10, 20, 50, and 100 year events by default
   :query float pct: percentile to use for exceedance threshold, when not specified the min value from the annual maxima series (AMS) is used
