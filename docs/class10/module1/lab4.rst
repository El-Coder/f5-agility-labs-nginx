NGINX Plus API Live Monitoring
==============================

Introduction
------------

The `NGINX Plus
API <https://www.nginx.com/products/nginx/live-activity-monitoring/>`__
supports other features in addition to live activity monitoring,
including dynamic configuration of upstream server groups and key‑value
stores.

Live examples:​ \* A `sample
configuration <https://gist.github.com/nginx-gists/a51341a11ff1cf4e94ac359b67f1c4ae>`__
file for the NGINX Plus API \* Example live dashboard:
`demo.nginx.com <https://demo.nginx.com>`__ \* Raw JSON output:
`demo.nginx.com/api​ <https://demo.nginx.com/api>`__ \* Swagger-UI:
`demo.nginx.com/swagger-ui <https://demo.nginx.com/swagger-ui/>`__ \*
API YAML:
`demo.nginx.com/swagger-ui <https://demo.nginx.com/swagger-ui/nginx_api.yaml>`__

Learning Objectives
-------------------

By the end of the lab you will be able to:

-  Use `demo.nginx.com <https://demo.nginx.com>`__ for demo purposes
-  Use the NGINX Plus API to read live monitoring metrics on NGINX Plus
-  Interact with the NGINX Plus API using both
   `Postman <https://www.postman.com>`__ and
   ```cURL`` <https://curl.haxx.se>`__

Exercise 1: Explore the Live Activity Monitoring JSON Feed​ from demo.nginx.com using Postman:
----------------------------------------------------------------------------------------------

When you access the API, NGINX Plus returns a JSON‑formatted document
containing the current statistics. You can request complete statistics
at ``/api/[api-version]/``, where ``[api-version]`` is the version
number of the NGINX Plus API.

Lets look at the Live Activity Monitoring JSON Feed​ in detail.

In this section, we will use ``Postman`` to interact with the NGINX API.
In the Optional section below, we can reproduce the same steps using
``curl``

1. Open ``Postman`` tool found on the desktop

   .. figure:: images/Postman1_2020-08-26.png
      :alt: Open Postman app

      Open Postman app

2. Within the ``Live Activity Monitoring`` collection, open
   ``NGINX Info`` request and then click on ``Send`` button.
   \ ``/api/api-version/nginx/`` is used to retrieve basic version,
   uptime, and identification information​.

   .. figure:: images/Postman2_2020-08-26.png
      :alt: NGINX Info request

      NGINX Info request

3. Next open ``NGINX Connections`` request and then click on ``Send``
   button. \ ``/api/api-version/connections/`` is used to retrieve total
   active and idle connections​.

   .. figure:: images/Postman3_2020-08-26.png
      :alt: NGINX Info request

      NGINX Info request

4. Open ``NGINX Server Zones`` request and then click on ``Send``
   button. \ ``/api/api-version/http/server_zones/`` is used to retrieve
   request and response counts for each HTTP status zone.

   .. figure:: images/Postman4_2020-08-26.png
      :alt: NGINX Info request

      NGINX Info request

5. Open ``NGINX Cache`` request and then click on ``Send`` button.
   \ ``/api/api-version/http/caches/`` is used to retrieve
   instrumentation for each named cache zone.

   .. figure:: images/Postman5_2020-08-26.png
      :alt: NGINX Info request

      NGINX Info request

6. Open ``NGINX Upstreams`` request and then click on ``Send`` button.
   \ ``/api/api-version/stream/upstreams/`` is used to retrieve request
   and response counts, response time, health‑check status, and uptime
   statistics per server in each TCP/UDP upstream group.

   .. figure:: images/Postman6_2020-08-26.png
      :alt: NGINX Info request

      NGINX Info request

7. Open ``NGINX SSL`` request and then click on ``Send`` button.
   \ ``/api/api-version/ssl/`` is used to retrieve SSL/TLS statistics.

   .. figure:: images/Postman7_2020-08-26.png
      :alt: NGINX Info request

      NGINX Info request

Optional: Explore the Live Activity Monitoring JSON Feed​ from demo.nginx.com using cURL:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this section, we will use ``curl`` to interact with the NGINX API.

1. In the ``SSH`` folder found on the desktop, open any Linux SSH
   session found on here, e.g. ``NGINX-PLUS-1``

.. figure:: images/2020-06-29_22-06.png
   :alt: Select ssh session

   Select ssh session

2. In the Terminal Window, using ``curl`` and ``jq`` for JSON
   formatting, make a request to the API endpoint,
   ``/api/api-version/nginx/`` to retrieve basic version, uptime, and
   identification information​

   .. code:: bash

      $> curl -s https://demo.nginx.com/api/6/nginx/ | jq

      {
        "version": "1.19.0",
        "build": "nginx-plus-r22",
        "address": "206.251.255.64",
        "generation": 55,
        "load_timestamp": "2020-06-30T03:00:00.120Z",
        "timestamp": "2020-06-30T04:09:57.399Z",
        "pid": 24706,
        "ppid": 61031
      }

3. Using ``curl`` and ``jq``, make a request to the API endpoint,
   ``/api/api-version/connections/`` to retrieve total active and idle
   connections​

   .. code:: bash

      $> curl -s https://demo.nginx.com/api/6/connections/ | jq

      {
        "accepted": 32284461,
        "dropped": 0,
        "active": 1,
        "idle": 55
      }

4. Using ``curl`` and ``jq``, make a request to the API endpoint,
   ``/api/api-version/http/server_zones/`` to retrieve request and
   response counts for each HTTP status zone​

.. code:: bash

   $> curl -s https://demo.nginx.com/api/6/http/server_zones/ | jq

   {
     "hg.nginx.org": {
       "processing": 0,
       "requests": 0,
       "responses": {
         "1xx": 0,
         "2xx": 0,
         "3xx": 0,
         "4xx": 0,
         "5xx": 0,
         "total": 0
       },
       "discarded": 0,
       "received": 0,
       "sent": 0
     },
     "trac.nginx.org": {
       "processing": 0,
       "requests": 0,
       "responses": {
         "1xx": 0,
         "2xx": 0,
         "3xx": 0,
         "4xx": 0,
         "5xx": 0,
         "total": 0
       },
       "discarded": 0,
       "received": 0,
       "sent": 0
     },
     "lxr.nginx.org": {
       "processing": 0,
       "requests": 2635,
       "responses": {
         "1xx": 0,
         "2xx": 2505,
         "3xx": 17,
         "4xx": 76,
         "5xx": 37,
         "total": 2635
       },
       "discarded": 0,
       "received": 856154,
       "sent": 62626264
     }
   }
   # Trimmed

5. Using ``curl`` and ``jq``, make a request to the API endpoint,
   ``/api/api-version/http/caches/`` to retrieve instrumentation for
   each named cache zone

.. code:: bash

   $> curl -s https://demo.nginx.com/api/6/http/caches/ | jq

   {
     "http_cache": {
       "size": 0,
       "max_size": 536870912,
       "cold": false,
       "hit": {
         "responses": 0,
         "bytes": 0
       },
       "stale": {
         "responses": 0,
         "bytes": 0
       },
       "updating": {
         "responses": 0,
         "bytes": 0
       },
       "revalidated": {
         "responses": 0,
         "bytes": 0
       },
       "miss": {
         "responses": 0,
         "bytes": 0,
         "responses_written": 0,
         "bytes_written": 0
       },
       "expired": {
         "responses": 0,
         "bytes": 0,
         "responses_written": 0,
         "bytes_written": 0
       },
       "bypass": {
         "responses": 0,
         "bytes": 0,
         "responses_written": 0,
         "bytes_written": 0
       }
     }
   }

6. Using ``curl`` and ``jq``, make a request to the API endpoint,
   ``/api/api-version/stream/upstreams/`` to retrieve request and
   response counts, response time, health‑check status, and uptime
   statistics per server in each TCP/UDP upstream group

   .. code:: bash

      $> curl -s https://demo.nginx.com/api/6/stream/upstreams/ | jq

      {                                                                                                                                                           
        "postgresql_backends": {                                                                                                                                  
          "peers": [                                                                                                                                              
            {                                                                                                                                                     
              "id": 0,                                                                                                                                            
              "server": "10.0.0.2:15432",                                                                                                                         
              "name": "10.0.0.2:15432",                                                                                                                           
              "backup": false,                                                                                                                                    
              "weight": 1,                                                                                                                                        
              "state": "up",                                                                                                                                      
              "active": 0,                                                                                                                                        
              "max_conns": 42,                                                                                                                                    
              "connections": 9250,                                                                                                                                
              "connect_time": 1,                                                                                                                                  
              "first_byte_time": 1,                                                                                                                               
              "response_time": 1,                                                                                                                                 
              "sent": 952750,                                                                                                                                     
              "received": 1850000,                                                                                                                                
              "fails": 0,                                                                                                                                         
              "unavail": 0,                                                                                                                                       
              "health_checks": {                                                                                                                                  
                "checks": 5564,                                                                                                                                   
                "fails": 0,                                                                                                                                       
                "unhealthy": 0,                                                                                                                                   
                "last_passed": true                                                                                                                               
              },                                                                                                                                                  
              "downtime": 0,                                                                                                                                      
              "selected": "2020-06-23T17:43:55Z"                                                                                                                  
            },                                                                                                                                                    
            {                                                                                                                                                     
              "id": 1,                                                                                                                                            
              "server": "10.0.0.2:15433",                                                                                                                         
              "name": "10.0.0.2:15433",                                                                                                                           
              "backup": false,                                                                                                                                    
              "weight": 1,                                                                                                                                        
              "state": "up",                                                                                                                                      
              "active": 0,                                                                                                                                        
              "connections": 9250,       

              # Trimmed..

7. Using ``curl`` and ``jq``, make a request to the API endpoint,
   ``/api/api-version/ssl/`` to retrieve SSL/TLS statistics

.. code:: bash

   $> curl -s https://demo.nginx.com/api/6/ssl/ | jq

   {
     "handshakes": 784975,
     "handshakes_failed": 70687,
     "session_reuses": 122210
   }