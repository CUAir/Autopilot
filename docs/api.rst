.. CUAir Autopilot Documentation documentation master file, created by
   sphinx-quickstart on Mon May  2 11:28:43 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Autopilot API endpoints
============================

.. contents::

The API for communicating between the autopilot and the ground station.

Status [/status]
----------------

Get the status of the plane: A large json containing each piece of data as a name/value pair. A call can also be made to /status/... to receive an
individual bit of data (below)::

  Response 200 (application/json)
        {
            "attitude" : {
                "pitch" : 0.0,
                "yaw" : 0.0,
                "roll" : 0.0,
                "pitchspeed" : 0.0,
                "yawspeed" : 0.0,
                "rollspeed" : 0.0
                },
            "battery" : {
                "pct" : 0.0,
                "voltage" : 0.0
                },
                
            "link" : {
                "gps_link" : "True",
                "plane_link" : "True"
                },
            
            "time" : 0,
            
            "gps" : {
                "rel_alt" : 0.0,
                "asl_alt" : 0.0,
                "lat" : 0.0,
                "lon" : 0.0,
                "heading" : 0.0,
                "vx" : 0.0,
                "vy" : 0.0,
                "vz" : 0.0
            },
            "mode": "AUTO",
            "airspeed" : {
                "vx" : 0.0,
                "vy" : 0.0,
                "vz" : 0.0
            },
            
            "wind" : {
                "vx" : 0.0,
                "vy" : 0.0,
                "vz" : 0.0
            },
            
            "throttle" : 0,
            
            "waypoints" : [{
                "alt" : 0.0,
                "lon" : 0.0,
                "lat" : 0.0
            }],
            
            "wp_count" : 0,
            "current_wp" : 0,
            "geofences" :  [{
                "lat" : 0.0,
                "lon" : 0.0
            }],
            "hud" : {
            "airspeed" : 0.0,
            "groudspeed": 0.0,
            "heading": 0,
            "throttle": 0,
            "alt": 0.0,
            "climb": 0.0
            }
        }

Attitude [/status/attitude]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Returns the plane's attitude, containing:

* Pitch [float]
* Yaw [float]
* Roll [float]
* Pitchspeed [float]
* Yawspeed [float]
* Rollspeed [float]

::

  + Response 200 (application/json)
  { 
     "pitch" : 0.0,
     "yaw" : 0.0,
     "roll" : 0.0,
     "pitchspeed" : 0.0,
     "yawspeed" : 0.0,
     "rollspeed" : 0.0,
   }

Battery [/status/battery]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the current state of the plane's battery, containing:

* pct [float]
* voltage [float]

::

 + Response 200 (application/json)
        {
            "pct" : 0.0,
            "voltage" : 0.0,
        }
        
Link [/status/link]
^^^^^^^^^^^^^^^^^^^

Returns the status of links, containing:

* gps_link [boolean]
* plane_link [boolean]

::

 + Response 200 (application/json)
        {
            "gps_link" : "True",
            "plane_link" : "True",
        }
        
Time [/status/time]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the current time as an long representing a [unix timestamp](https://en.wikipedia.org/wiki/Unix_time) 


::

  + Response 200 (application/json)
        {
           0
        }
        
GPS [/status/gps]
^^^^^^^^^^^^^^^^^^^^^^^^

Returns various values from the plane's onboard GPS, containing:

* rel_alt [float]
* asl_alt [float]
* lat [float]
* lon [float]
* heading [float]
* vx [float]
* vy [float]
* vz [float]

::

  + Response 200 (application/json)
        {
            "rel_alt" : 0.0,
            "asl_alt" : 0.0,
            "lat" : 0.0,
            "lon" : 0.0,
            "heading" : 0.0,
            "vx" : 0.0,
            "vy" : 0.0,
            "vz" : 0.0,
        }
        
Mode [/status/mode]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the current flying mode of the plane as a string, e.g. "AUTO", "MANUAL", "FLY_BY_WIRE_A"

::

 Response 200 (application/json)
        {
           "AUTO"
        }
        
Airspeed [/status/airspeed]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns vectors vx, vy, vz representing the airspeed velocity of the airplane as floats

::

 + Response 200 (application/json)
        {
            "vx" : 0.0,
            "vy" : 0.0,
            "vz" : 0.0
        }

Wind [/status/wind]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns vectors vx, vy, vz representing the wind velocity vector as floats

::

 Response 200 (application/json)
        {
            "vx" : 0.0,
            "vy" : 0.0,
            "vz" : 0.0
        }    
        
Throttle [/status/throttle]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An integer from 0 to 100 representing the current throttle level of the plane

::

 Response 200 (application/json)
        {
            0
        }
        
Waypoints [/status/waypoints]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a list of JSON objects representing the current waypoints altitude, latitude, and longitude

::

 + Response 200 (application/json)
        [{
                "alt" : 0.0,
                "lon" : 0.0,
                "lat" : 0.0,
        }]
        
Waypoint Count [/status/wp_count]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns an integer representing the current number of waypoints

::

 + Response 200 (application/json)
        {
            0
        }
        
Current Waypoint [/status/current_wp]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns an integer representing the current waypoint

::

 + Response 200 (application/json)

        {
            0
        }
        
Geofence [/status/geofences]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a list of JSON objects representing the latitude and longitude of the geofences

:: 

 Response 200 (application/json)
        [{
            "lat" : 0.0,
            "lon" : 0.0,
        }]

HUD [/status/hud]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a list of values needed for the HUD, containing,

* airspeed [float]
* groundspeed [float]
* heading [integer]
* throttle [integer]
* alt [float]
* climb [float]

:: 

 Response 200 (application/json)
        {
            "airspeed" : 0.0,
            "groudspeed": 0.0,
            "heading": 0,
            "throttle": 0,
            "alt": 0.0,
            "climb": 0.0
        }

Software Status [/status/softstatus?time=TIME]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Use the GET argument "time" (/status/softstatus?time=TIME) to request a status at a specific time. If an exact value is not available, an interoplated value will be provided.

::

 Response 200 (application/json)
        {      
        attitude: {
            'roll': 0,
            'pitch': 0,
            'yaw': 0,
            'rollspeed': 0,
            'yawspeed': 0,
            'pitchspeed': 0
            
        },
        gps:{
             lat: 0,
             lon: 0,
             asl_alt: 0,
             vx: 0,
             vy: 0,
             vz: 0,
             heading: 0,
             rel_alt: 0
         },
         airspeed:{
             'vx': 0,
             'vy': 0,
             'vz': 0
         },
         wind: {
             'vx': 0,
             'vy': 0,
             'vz': 0
         }


Waypoints [/wp]
-----------------

* **GET**

Returns a list of waypoints, each containing, altitude, longitude, latitude, current waypoint, waypoint type or `MAV_CMD <http://mavlink.org/messages/common>`_ , waypoint index::

 Response 200 (application/json)
        [{
            "alt" : 0.0, [meters]
            "lon" : 0.0, [degrees]
            "lat" : 0.0, [degrees]
            "current": 0, 
            "type": 12, 
            "index": 0 
        }, 
        {
            "alt" : 0.0,
            "lon" : 0.0,
            "lat" : 0.0,
            "current": 0,
            "type": 16,
            "index": 0
        }]
    
*  **GET with arguments [GET /wp/{?wpnum}]**

The response field, "type" in GET is the same as the "command" field in POST and PUT. 
The associated waypoint types and numbers are listed under POST. 

Parameters: *wpnum*  - the index of the waypoint you wish to recieve::

  Response 200 (application/json)

        {
            "alt" : 0.0,
            "lon" : 0.0,
            "lat" : 0.0,
            "current": 0,
            "type": 21,
            "index": 0
        }
        
* **DELETE**
   Delete a specific waypoint.
   
   Parameters: *wpnum*  - The waypoints index

::

   Response 200 (application/json)
        "True"

* **POST**


::

   Headers
      Content-Type: application/json
      token: <secret token>

   Requests
      "lat: <lat>,        [The waypoint's latitude]
      lon: <lon>,        [The waypoint's longitude]
      alt: <alt>,        [The waypoint's altitude]
      index: <index>,    [The waypoints index]
      commant: <command> [The waypoints type or `MAV_CMD <http://mavlink.org/messages/common>`]

   Response 200 (application/json)
        "True"

* **PUT**

   PUT has the same parameters as POST but will update the values of the waypoint at the specified index.

::

   Headers
      Content-Type: application/json
      token: <secret token>

   Requests:
    "lat: <lat>,        [The waypoint's latitude]
     lon: <lon>,        [The waypoint's longitude]
     alt: <alt>,        [The waypoint's altitude]
     index: <index>,    [The waypoints index]
     commant: <command> [The waypoints type or `MAV_CMD <http://mavlink.org/messages/common>`]

   Response 200 (application/json)
        "True"


Interop [/interop]
------------------


Server Control [/v1/interop] [ground/api/v3/interop]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* **POST**

  Sending a POST request to this endpoint starts the interop backend. To do this, it creates a new instance of the backend object, then starts the backend on a separate thread and sets the server to active. It will fail if the server is either already started, or if it has been less that a half second since the server was either started or stopped last. Requires a valid JSON containing the server data (username, password, and url fields). Requires a valid auth token to access. ::

    Response 200


* **DELETE**

  Sending a DELETE request to this endpoint will stop the interop backend. It simply sets the Data.server_active global variable to false. This is the loop condition on the backend, so the server will stop as soon as it completes its current loop. This will fail if the server is either already stopped or if it has been less that a half second since the server was either started or stopped last. Requires a valid auth token to access ::

    Response 200


* **GET**

  Returns a JSON string containing the obstacle data and server info ::

    Response 200 (application/json)
            {
              obstacles : {
                        stationary_obstacles : [{
                              cylinder_height : 0.0, 
                              cylinder_radius : 0.0, 
                              latitude : 0.0, 
                              longitude : 0.0
                            }],
                        moving_obstacles : [{
                              altitude_msl: 0.0, 
                              latitude : 0.0, 
                              longitude : 0.0, 
                              sphere_radius : 0.0
                        }],
              },
              server_info : {
                  message : "Hello World!", 
                  message_timestamp : "2015-08-02T01:16:15.609002+00:00", 
                  server_time : "2015-10-31T18:12:44.210815"
              }
              server_working : "True"
            }
    

Obstacles [/v1/interop/obstacles] [/ground/api/v3/interop/obstacles]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a JSON object string that contains a list of both moving and stationary objects. Checks to see if the server is active, and, if so, retrieves data from the MAVProxy.modules.server.data module, jsonifies it and returns it. ::

  Response 200 (application/json)
          {
            stationary_obstacles : [{
                  cylinder_height : 0.0, 
                  cylinder_radius : 0.0, 
                  latitude : 0.0, 
                  longitude : 0.0
                }],
            moving_obstacles : [{
                  altitude_msl : 0.0, 
                  latitude : 0.0, 
                  longitude : 0.0, 
                  sphere_radius : 0.0
            }],
          }


Server Info [/v1/interop/server_info] [/ground/api/v3/interop/server_info]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a JSON object string that contains the server message, message timestamp, and the server time at last retrieval. Checks to see if the server is active, and, if so, retrieves data from the MAVProxy.modules.server.data module, jsonifies it and returns it. ::

  Response 200 (application/json)
        {
          message : "Hello World!", 
          message_timestamp : "2015-08-02T01:16:15.609002+00:00", 
          server_time : "2015-10-31T18:12:44.210815"
        }


Time [/v1/interop/time] [/ground/api/v3/interop/time]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a single string that represents the server time at last retrieval. Checks to see if the server is active, and, if so, retrieves data from the MAVProxy.modules.server.data module, then returns it as a raw string. ::

  Response 200 (application/json)

        "2015-10-27T16:34:33.594240"
