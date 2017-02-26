MAVProxy Playback
===================

.. contents::

The equivalent to the database and API endpoints for MAVProxy intended for use
by the distibuted team to replay testflights

How to Set Up 
--------------

Dumping the Database after the Testflight
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once the flight is complete from MAVProxy dump the database into a file named mysqldump.txt

::

	sudo mysqldump --result-file=mydump.sql -paeolus mavproxy

Loading the Dump File into the Playback Database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

once the file is copied into the playback folder this will reload the data into this database

::
    
    sudo mysql -paeolus mavproxy < mydump.sql 

*if you get the can't connect to mySQL server through socket ... erorr try 

::

	mysqld

*if this is the first time you are running the database on your computer or you get the no database error try

::
	
    ./setup_db_osx.sh

Launching the Flask App
^^^^^^^^^^^^^^^^^^^^^^^^

::
	
    export FLASK_APP=playbackStatus.py
    python playbackStatus.py


API endpoints
--------------

Status [/status]
^^^^^^^^^^^^^^^^

Get the status of the plane: A large json containing each piece of data as a name/value pair. A call can also be made to /status/... to receive an
individual bit of data (below)::

  + Response 200 (application/json)
        {
            "attitude" : {
                "pitch" : 0.0,
                "yaw" : 0.0,
                "roll" : 0.0,
                "pitchspeed" : 0.0,
                "yawspeed" : 0.0,
                "rollspeed" : 0.0
                },

            "airspeed" : {
                "vx" : 0.0,
                "vy" : 0.0,
                "vz" : 0.0
            },
            
            "climb": 0.0,
            
            "flight_time" : {
                "time" : 0.0,
                "time_start" : 0.0,
                "is_flying" : "False"
            },
            
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

            "throttle": 0,

            "wind" : {
                "vx" : 0.0,
                "vy" : 0.0,
                "vz" : 0.0
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

Climb [/status/climb]
^^^^^^^^^^^^^^^^^^^^^^

Returns a float value representing the climb of the plane

::

 + Response 200 (application/json)
        {
            0.0
        }

Flight Time [/status/flight_time]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns the information about the flight time conntaing:

* time_start [float]
* if_flying [boolean]

::

 + Response 200 (application/json)
        {
            "time" : 0.0,
            "time_start" : 0.0,
            "is_flying" : "False"
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
 
Throttle [/status/throttle]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An integer from 0 to 100 representing the current throttle level of the plane

::

 + Response 200 (application/json)
        {
            0
        }
 
Wind [/status/wind]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Returns vectors vx, vy, vz representing the wind velocity vector as floats

::

 + Response 200 (application/json)
        {
            "vx" : 0.0,
            "vy" : 0.0,
            "vz" : 0.0
        }    
