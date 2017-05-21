Test Flights
============

.. contents::

Overview
---------

The autopilot sub-team has developed numerous resources and strategies to be most efficient and productive at test flights. This page details these methods and consolidates links to essential resources. 

Preparation for a Test Flight
-----------------------------

Please read the `ArduPlane Documentation <http://ardupilot.org/plane/docs/introduction.html>`_  to familiarize yourself with tuning methodologies.

`Here <https://pixhawk.org/users/status_leds>`_ you can also find a description of the meaning of different Pixhawk status LEDs.


Before the Test Flight
-----------------------

`Charging batteries <https://docs.google.com/a/cornell.edu/document/d/1BB32SqGUB9Od7vRuGxLZDtUl3IxABGeZSRhjDGb9uEE/edit?usp=sharing>`_ -- Batteries need to be changed before every flight. This documentation describes how to do so safety. 


`Packing Checklist <https://docs.google.com/a/cornell.edu/document/d/1ayoTEOM1kUWVMDSlj4T_z2wIWLmFvlScaIrMWGEYeLU/edit?usp=sharing>`_ -- Before leaving for a test flight, test accordingly in the lab and ensure these items are packed.


At the Test Flight
-------------------

Roles -- Assigning more limited roles at test flights ensures team members can work concurrently. 

`Preflight Todo Checklist <https://docs.google.com/a/cornell.edu/document/d/1ayoTEOM1kUWVMDSlj4T_z2wIWLmFvlScaIrMWGEYeLU/edit?usp=sharing>`_ -- Follow these steps carefully to avoid common issues with flight

`Tuning guide <https://docs.google.com/a/cornell.edu/document/d/1GEGPoO7C8SVG3ce17zwZWjsApVifKiyOvoxnIkX4Or4/edit?usp=sharing>`_ -- This manual details the steps needed to tunning ArduPlane. Print the manual and follow along accordingly. 

`Flight Cards <https://docs.google.com/a/cornell.edu/presentation/d/1QKiTktPquDpCYcg-_-agLuD5t6N1zBHpDIT-jldJb_s/edit?usp=sharing>`_ -- Fill out one of these at each test flight.

Code to run at test flights
^^^^^^^^^^^^^^^^^^^^^^^^^^^
- `APM Planner <http://ardupilot.com/downloads/#apm_planner_20_9_raquo>`_ -- as a backup APM should be installed on all computers 

- `MAVProxy <http://cuairautopilot.readthedocs.io/en/latest/groundstation.html#ground-station>`_ -- Installation and instructions for using the ground station can be found here.

- `Interoperability <http://cuairautopilot.readthedocs.io/en/latest/groundstation.html#interoperability>`_ -- Setup can use of the interoperability server can be found here

--`Autopilot server <>`_ -- Setup and use of autopilot server for the NUC can be found here.

Hex Flying Procedure Without GCS
-------------------------------
Pre-flight checks: 

- Make sure all the props are placed in the correct directions! There are little red arrows on each motor for the direction that it should spin. 

- Check that all the motors do indeed spin in that direction. If they spin the other way, swap the red and black plugs from the ESC.

- Double and triple check that all props are screwed down tightly. 

Now you can begin flight procedure:

1. Turn on Taranis, make sure you are on the model “hex”
2. Plug in 6s battery.
3. Wait until main light is flashing a single color (preferably green - maybe blue - not yellow).
4. Press and hold safety switch until the ESCs beep and the light on the safety switch becomes solid green. The motors may twitch a bit. Atlas is now live.
5. MAKE SURE EVERYONE IS FAR AWAY FROM THE HEX. 
6. Arm Atlas: On the transmitter, hold the left stick down and right until Pixhawk light becomes a solid color and props start spinning slowly. It is now armed.
7. Fly. Optionally set mode to ‘land’ on ground station for auto landing if GCS is connected.
8. To disarm the hex: hold left stick down and left until props stop spinning and main pixhawk light starts flashing. 
9. Press and hold the safety switch until the ESCs beep and the safety switch begins flashing green. 
10. Unplug the battery.

