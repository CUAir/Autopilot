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
          "throttle": 0.0,
          "battery": {
            "time": 0.0,
            "batterypct": 0.0,
            "batteryvoltage": 0.0,
            "batterycurrent": 0.0
          },
          "signal": {
            "time": 0.0,
            "signal_strength": 0
          },
          "safe": true,
          "airspeed": {
            "time": 0.0,
            "airvx": 0.0,
            "airvy": 0.0,
            "airvz": 0.0,
            "speed": 0.0,
            "climb": 0.0,
            "throttle": 0.0
          },
          "wp_count": 0,
          "mav_warning": "",
          "current_wp": 0,
          "attitude": {
            "time": 0.0,
            "roll": 0.0,
            "pitch": 0.0,
            "yaw": 0.0,
            "rollspeed": 0.0,
            "pitchspeed": 0.0,
            "yawspeed": 0.0
          },
          "mav_info": "EKF2 IMU1 is using GPS",
          "link": {
            "plane_link": true,
            "links": null,
            "gps_link": true
          },
          "mode": "MANUAL",
          "mav_error": "",
          "gps_status": {
            "time": 0.0,
            "satellite_number": 0
          },
          "armed": true,
          "wind": {
            "time": 0.0,
            "windvx": 0.0,
            "windvy": 0.0,
            "windvz": 0.0
          },
          "gps": {
            "time": 0.0,
            "rel_alt": 0.0,
            "asl_alt": 0.0,
            "lat": 0.0,
            "lon": 0.0,
            "heading": 0.0,
            "groundvx": 0.0,
            "groundvy": 0.0,
            "groundvz": 0.0
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
          "time": 0.0,
          "roll": 0.0,
          "pitch": 0.0,
          "yaw": 0.0,
          "rollspeed": 0.0,
          "pitchspeed": 0.0,
          "yawspeed": 0.0
        }


Battery [/status/battery]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the current state of the plane's battery, containing:

* batterypct [float]
* batteryvoltage [float]
* batterycurrent [float]

::

 + Response 200 (application/json)
        {
          "time": 0.0,
          "batterypct": 0.0,
          "batteryvoltage": 0.0,
          "batterycurrent": 0.0
        }

        
Link [/status/link]
^^^^^^^^^^^^^^^^^^^

Returns the status of links, containing:

* gps_link [boolean]
* plane_link [boolean]
* links [list]

::

 + Response 200 (application/json)
        {
          "plane_link": true,
          "links": [
            {
              "packet_loss": 0.0,
              "alive": true,
              "device_name": "WiFi",
              "num": 0,
              "device": "tcp:127.0.0.1:5760",
              "num_lost": 0,
              "link_delay": 0.0
            }
          ],
          "gps_link": true
        }

        
GPS [/status/gps]
^^^^^^^^^^^^^^^^^^^^^^^^

Returns various values from the plane's onboard GPS, containing:

* rel_alt [float]
* asl_alt [float]
* lat [float]
* lon [float]
* heading [float]
* groundvx [float]
* groundvy [float]
* groundvz [float]

::

  + Response 200 (application/json)
        {
          "time": 0.0,
          "rel_alt": 0.0,
          "asl_alt": 0.0,
          "lat": 0.0,
          "lon": 0.0,
          "heading": 0.0,
          "groundvx": 0.0,
          "groundvy": 0.0,
          "groundvz": 0.0
        }

        
Mode [/status/mode]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the current flying mode of the plane as a string, e.g. "AUTO", "MANUAL", "FLY_BY_WIRE_A"

* str

::

 Response 200 (text/html)
        "MANUAL"

        
Airspeed [/status/airspeed]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns vectors vx, vy, vz representing the airspeed velocity of the airplane as floats

* speed [float]
* climb [float]
* throttle [float]
* airvx [float]
* airvy [float]
* airvz [float]

::

 + Response 200 (application/json)
        {
          "time": 0.0,
          "airvx": 0.0,
          "airvy": 0.0,
          "airvz": 0.0,
          "speed": 0.0,
          "climb": 0.0,
          "throttle": 0.0
        }


Wind [/status/wind]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns vectors vx, vy, vz representing the wind velocity vector as floats

* windvx [float]
* windvy [float]
* windvz [float]

::

 Response 200 (application/json)
        {
          "time": 0.0,
          "windvx": 0.0,
          "windvy": 0.0,
          "windvz": 0.0
        }
  

Signal [/status/signal]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the time and the signal strength as an integer of the transmitter connection. 0: 0%, 100: 100%, 255: invalid/unknown. See `_RC_CHANNELS* packet <http://mavlink.org/messages/common#RC_CHANNELS_SCALED>`_ rssi field.

* signal_strength

::

 + Response 200 (application/json)
        {
          "time": 0.0,
          "signal_strength": 0
        }

        
Flight Time [/status/flight_time]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the information about the flight time conntaing:

* time_start [float]|[null]
* if_flying [boolean]

::

 + Response 200 (application/json)
        {
          "time": 0.0,
          "time_start": null,
          "is_flying": true
        }

        
GPS Status [/status/gps_status]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the gps connection represented by an integer number of satellites visible

* satellite_number [int]

::

 + Response 200 (application/json)
        {
          "time": 0.0,
          "satellite_number": 0
        }


Throttle [/status/throttle]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An integer from 0 to 100 representing the current throttle level of the plane

::

 Response 200 (text/html)
        0.0

        
Waypoint Count [/status/wp_count]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns an integer representing the current number of waypoints

::

 + Response 200 (text/html)
        0

        
Current Waypoint [/status/current_wp]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns an integer representing the current waypoint

::

 + Response 200 (text/html)
        0


Calibration [/cali]
---------------------

Accelerometer Calibration [/cali/accel]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **POST**

Starts the accelerometer calibration process::

 Response 200 (text/html)
      "Started accelerometer calibration."

* **PUT**

Continues calibration process (mostly for accelerometer)::

 Response 200 (text/html)
      "Continuing."

Gyroscope Calibration [/cali/gyro]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **POST**

Starts the gyroscope calibration process::

 Response 200 (text/html)
      "True"

RC Calibration [/cali/rc]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **POST**

Starts the RC calibration process::

 Response 200 (text/html)
      "True"

* **DELETE**

Stops the RC calibration process::

 Response 200 (text/html)
      "True"

Extras
--------

Cache Map [/cachemaps]
^^^^^^^^^^^^^^^^^^^^^^^

* **POST**

Tells the backend to cache a map location::

   Headers
      Content-Type: application/json

   Requests
      name: <string>       [The location name]
      lat: <float>         [The location's latitude]
      lon: <float>         [The location's longitude]

   Response 200 (application/json) 
        {
            'topLat': 1,
            'bottomLat': 0,
            'leftLon': 0,
            'rightLon': 1,
            'centerLat': 0.5,
            'centerLon': 0.5  
        }

Get Locations [/getlocations]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **GET**

Retrieves the list of cached map locations::

   Headers
      Content-Type: application/json

   Response 200 (application/json) 
      {
        "Cornell_Campus": {
          "leftLon": -76.4950662435,
          "imageURL": "img/satellites/Cornell_Campus_Satellite.png",
          "bottomLat": 42.4384214463,
          "topLat": 42.4586880256,
          "rightLon": -76.4676004232
        },
        "Game_Farm": {
          "leftLon": -76.4650662435,
          "imageURL": "img/satellites/Game_Farm_Satellite.png",
          "bottomLat": 42.4333928552,
          "topLat": 42.4536610611,
          "rightLon": -76.4376004232
        }
      }

Arming [/arm]
^^^^^^^^^^^^^^

* **POST**

Arms the plane::

   Headers
      Content-Type: application/json
      token: <secret token>
      confirm: confirm

   Response 200 (text/html)
     "True"

* **DELETE**

Disarms the plane::

   Headers
      Content-Type: application/json
      token: <secret token>
      confirm: confirm

   Response 200 (text/html)
     "True"

Set Flight Mode [/set_mode]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **POST**

Sets the plane mode::

  Headers
      Content-Type: application/json
      token: <secret token>

  Requests
      mode: <string>    [The name of the mode to switch into]

  Response 200 (text/html)
      "Accepted Mode Change."

Get Flight Mode [/flight_mode]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **GET**

Gets the plane mode::

  Response 200 (text/html)
      "MANUAL"

Reboot [/reboot]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **POST**

Causes the plane to reboot

  Headers
      Content-Type: application/json
      token: <secret token>
      confirm: confirm

  Response 200 (text/html)
      "True"

SDA [/sda]
-----------

* **GET**
Returns whether SDA is enabled::

  Response 200 (text/html)
    true

* **POST**
Activates SDA::

  Headers
      Content-Type: application/json
      token: <secret token>

  Response 200 (application/json)
    true

* **DELETE**
Deactivates SDA::

  Headers
      Content-Type: application/json
      token: <secret token>

  Response 200 (application/json)
    True


Geofences [/geofence]
----------------------

* **GET**
Returns the geofence points::

  Response 200 (application/json)
    [{
      "lat": 0.0 [degrees]
      "lon": 0.0 [degrees]
    }, {
      "lat": 0.0,
      "lon": 0.0
    }]

* **POST**
Sets the geofence points::

  Headers
      Content-Type: application/json
      token: <secret token>
   Requests
    list of:
      lat: <float>         [The fence point's latitude]
      lon: <float>         [The fence point's longitude]

  Response 200
    "Added Fence"

Waypoints [/wp]
-----------------

* **GET**

Returns a list of waypoints, each containing, altitude, longitude, latitude, current waypoint, waypoint type or `MAV_CMD <http://mavlink.org/messages/common>`_ , waypoint index::

   Response 200 (application/json)
        [
          {
            "command": 0,
            "current": 0,
            "param1": 0.0,
            "param2": 0.0,
            "param3": 0.0,
            "param4": 0.0,
            "lat": 0.0,
            "lon": 0.0,
            "alt": 0.0,
            "index": 0,
            "min_dist": 0.0
          }
        ]

    
*  **GET with arguments [GET /wp/{?wpnum}]**

The response field, "type" in GET is the same as the "command" field in POST and PUT. 
The associated waypoint types and numbers are listed under POST. 

Parameters: *wpnum*  - the index of the waypoint you wish to recieve::

  Response 200 (application/json)
        {
          "command": 0,
          "current": 0,
          "param1": 0.0,
          "param2": 0.0,
          "param3": 0.0,
          "param4": 0.0,
          "lat": 0.0,
          "lon": 0.0,
          "alt": 0.0,
          "index": 0,
          "min_dist": 0.0
        }


        
* **DELETE**
   Delete a specific waypoint.
   
   Parameters: *wpnum*  - The waypoints index

::

   Response 200 (text/html)
        "True"

* **POST**


::

   Headers
      Content-Type: application/json
      token: <secret token>

   Requests
      lat: <float>         [The waypoint's latitude]
      lon: <float>         [The waypoint's longitude]
      alt: <float>         [The waypoint's altitude]
      index: <int>         [The waypoints index]
      command: <int>       [The waypoints type or `MAV_CMD <http://mavlink.org/messages/common>`]

   Response 200 (text/html)
      "True"

* **PUT**

   PUT has the same parameters as POST but will update the values of the waypoint at the specified index.

::

   Headers
      Content-Type: application/json
      token: <secret token>

   Requests
      lat: <float>         [The waypoint's latitude]
      lon: <float>         [The waypoint's longitude]
      alt: <float>         [The waypoint's altitude]
      index: <int>         [The waypoints index]
      command: <int>       [The waypoints type or `MAV_CMD <http://mavlink.org/messages/common>`]

   Response 200 (text/html)
      "True"


Interop [/interop]
------------------


Server Control [ground/api/v3/interop]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* **POST**

  Sending a POST request to this endpoint starts the interop backend. To do this, it creates a new instance of the backend object, then starts the backend on a separate thread and sets the server to active. It will fail if the server is either already started, or if it has been less that a half second since the server was either started or stopped last. Requires a valid JSON containing the server data (username, password, and url fields). Requires a valid auth token to access. ::

    Response 200


* **DELETE**

  Sending a DELETE request to this endpoint will stop the interop backend. It simply sets the Data.server_active global variable to false. This is the loop condition on the backend, so the server will stop as soon as it completes its current loop. This will fail if the server is either already stopped or if it has been less that a half second since the server was either started or stopped last. Requires a valid auth token to access ::

    Response 200


* **GET**

  Returns a JSON string containing all available server info

  * "Obstacles" : Data structure containg obstacles ({"moving_obstacles":[],"stationary_obstacles":[]})
  * "server_working" : Does the server believe it is functioning correctly (boolean)
  * "hz" : Rolling frequency of interop telemetry posts (integer)
  * "active" : Is the server active (boolean)
  * "wp_distances" : Closest point of approach to each waypoint (integer list)
  * "active_mission" : JSON of active mission as described by the `interop documentation <http://auvsi-suas-competition-interoperability-system.readthedocs.io/en/latest/specification.html#missions>`_. 

  ::

    Response 200 (application/json)
        {
          "hz": 0.0,
          "active_mission": {
            "emergent_last_known_pos": {
              "latitude": 0.0,
              "longitude": 0.0
            },
            "fly_zones": [
              {
                "boundary_pts": [
                  {
                    "latitude": 0.0,
                    "order": 0,
                    "longitude": 0.0
                  },
                  {
                    "latitude": 0.0,
                    "order": 0,
                    "longitude": 0.0
                  },
                  {
                    "latitude": 0.0,
                    "order": 0,
                    "longitude": 0.0
                  }
                ],
                "altitude_msl_max": 0.0,
                "altitude_msl_min": 0.0
              }
            ],
            "mission_waypoints": [
              {
                "latitude": 0.0,
                "altitude_msl": 0.0,
                "order": 0,
                "longitude": 0.0
              },

            ],
            "off_axis_odlc_pos": {
              "latitude": 0.0,
              "longitude": 0.0
            },
            "search_grid_points": [
              {
                "latitude": 0.0,
                "altitude_msl": 0.0,
                "order": 0,
                "longitude": 0.0
              }
            ],
            "active": true,
            "id": 0,
            "home_pos": {
              "latitude": 0.0,
              "longitude": 0.0
            },
            "air_drop_pos": {
              "latitude": 0.0,
              "longitude": 0.0
            }
          },
          "obstacles": {
            "moving_obstacles": [
              {
                "latitude": 0.0,
                "sphere_radius": 0.0,
                "altitude_msl": 0.0,
                "longitude": 0.0,
                "time": 0.0
              }
            ],
            "stationary_obstacles": [
              {
                "latitude": 0.0,
                "cylinder_height": 0.0,
                "cylinder_radius": 0.0,
                "longitude": 0.0
              }
            ]
          },
          "mission_waypoints": [
            {
              "latitude": 0.0,
              "altitude_msl": 0.0,
              "order": 0,
              "longitude": 0.0
            },
          ],
          "server_working": true,
          "mission_wp_dists": [
            0.0,
          ],
          "active": true
        }

    

Obstacles [/ground/api/v3/interop/obstacles]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a JSON object string that contains a list of both moving and stationary objects. Checks to see if the server is active, and, if so, retrieves data from the MAVProxy.modules.server.data module, jsonifies it and returns it. ::

  Response 200 (application/json)
        {
          "moving_obstacles": [
            {
              "latitude": 0.0,
              "sphere_radius": 0.0,
              "altitude_msl": 0.0,
              "longitude": 0.0,
              "time": 0.0
            }
          ],
          "stationary_obstacles": [
            {
              "latitude": 0.0,
              "cylinder_height": 0.0,
              "cylinder_radius": 0.0,
              "longitude": 0.0
            }
          ]
        }


Hz [/ground/api/v3/interop/hz]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a string containing the rolling average of the frequency that the interop server has been posting telemetry data ::

  Response 200
        0.0

Server Active [/ground/api/v3/interop/active]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a boolean string telling whether the interop server is currently active or not ::

  Response 200
          true


Status [/ground/api/v3/interop/status]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns a boolean string telling whether the interop server believes it is working as intended right now. Automatically true if the server is not active ::

  Response 200
          true
