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


Waypoints [/waypoints]
----------------------

Interop [/interop]
------------------
