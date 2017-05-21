Autopilot Configuration and Setup
=================================

.. contents::

Overview
---------

This page documents remaining autopilot configuration procedures that do not relate to ardupilot software.

Setting up RFD900s
-------------------

We use `RFD900+ <http://store.rfdesign.com.au/rfd-900p-modem/>`_ radio modems. Please read the `data sheet <http://files.rfdesign.com.au/Files/documents/RFD900%20DataSheet.pdf>`_ before attempting to change the modem settings.

1. Firmware can be installed on RFD900s with windows using the RFD900 configuration tool. This can be found `here <http://files.rfdesign.com.au/docs/>`_.

2. Settings should match below guide. Make sure to use the same netid on both nodes of a piar and use different netids on different pairs. If you have different settings than shown, you may need update your firmware  ::

    Baudrate 115200
    Airspeed 250
    NetID  xx
    Tx Power 27
    NodeID 1             # GROUND/BASE NODE SHOULD HAVE THESE REVERSED
    Node Destination 0   # GROUND/BASE NODE SHOULD HAVE THESE REVERSED

    Min Freq 902000
    Max Freq 928000
    Number of Channels 50
    Duty Cycle 100
    Node Count 2

    ECC (unchecked)
    Mavlink (checked)
    Sync any (unchecked)
    Op Resent (checked)
    RTCSTS (unchecked)



3. You can check that two RFD900s are paired and communicating with screen. In terminal, run the command ::

    screen /dev/tty.usb<DEVICE_NAME> <BAUDRATE>

For example  ::

    screen /deb/tty.usbmodem1 115200



Using 3DR radios on Mac OS
--------------------------------
Sorry, this is kind of a pain.

1. Confirm you are not using the Apple FDTI driver ::

    cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
    ls AppleUSBFTDI.kext 

If the kext is in this folder, disable it with the following command ::

    sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled

2. Download the latest FTDI driver from http://www.ftdichip.com/Drivers/VCP.htm I used x64 (64-bit) for OSX 10.9+.
3. Find the name of the device in “System Information” -> USB -> USB Device tree. Mine was named "CP2102 USB to UART Bridge Controller"
4. Plug in the the radio and Run ``system_profiler -detailLevel full`` and grep for the name found in step 3. You will need to locate the information for "idVendor", "idProduct", "bcdDevice".  My radio had the following info: ::
    
    "idProduct" = 0xea60
    "bcdDevice" = 0x100
    "idVendor" = 0x10c4

5.  Open /System/Library/Extensions/FTDIUSBSerialDriver.kext/Contents/Info.plist and add a new key/dictionary under IOKitPersonalities and make sure above 3 values(idVendor, idProduct, bcdDevice) are there and correct. You can do this with apple's plist editor or by opening the file and directly editing the XML. All values must be decimals (the values found in step 4 are in hex). I added the following to my XML: ::

    <key>CP2102 USB to UART Bridge Controller</key>
    <dict>
    <key>CFBundleIdentifier</key>
    <string>com.FTDI.driver.FTDIUSBSerialDriver</string>
    <key>IOClass</key>
    <string>FTDIUSBSerialDriver</string>
    <key>IOProviderClass</key>
    <string>IOUSBInterface</string>
    <key>bConfigurationValue</key>
    <integer>1</integer>
    <key>bInterfaceNumber</key>
    <integer>0</integer>
    <key>bcdDevice</key>
    <integer>256</integer>
    <key>idProduct</key>
    <integer>60000</integer>
    <key>idVendor</key>
    <integer>4292</integer>
    </dict>


6. Our driver will no longer match the system's signature so we will need disable System Integrity Protection to load the driver. To do so, first restart into recover mode by restarting your the computer and holding CMD+R as soon as you hear the boot noise until the apple logo appears on the screen. Then run the command ``csrutil disable`` in the terminal.
7. Restart your computer and load the new FTDI driver with the commands ::

    sudo kextunload /System/Library/Extensions/FTDIUSBSerialDriver.kext/
    sudo kextload /System/Library/Extensions/FTDIUSBSerialDriver.kext/

8. You should now see the FTDI device with ``ls /dev/ |grep usbserial``

**Note: Permenatly disabling csrutil and can leave your computer vulnearble to some nasty hacks. When you are done using the radios, rename csr by restarting into recovery mode and entering the command ``csrutil enable``


Binding Transmitter and Receiver
--------------------------------

We use an `EzUHF 4 Channel Receiver <http://www.immersionrc.com/fpv-products/ezuhf-4ch-receiver/>`_ and an `EzUHF Transmitter JR Module <http://www.immersionrc.com/fpv-products/ezuhf-jr-module/>`_ on a Taranis Transmitter. Refer to their respective documentation if there is any confusion about the following binding procedure.


1. Download `ImmersionRC update config tool software <http://www.immersionrc.com/?download=4894>`_

2. Connect the transmitter to the computer with the config software.

3. On the software, set the transmitter to extreme hopping

4. Connect the receiver to the computer with the config software

5. On the receiver, set the frequency band to match the transmitter frequency band

6. On the servo mapping tab set PPM slot and servo output as follows ::

    PPM1 CH2
    PPM2 CH3
    PPM3 CH1
    PPM4 CH4
    PPM5 CH5
    PPM6 CH6
    PPM7 CH7
    PPM8 CH8

    CH1 PPM Muxed
    CH2 -
    CH3 -
    CH4 -

7. Put the transmitter into bind mode by turning it off and then holding the bind button on the module on the back as it turns on. It should start beeping slowly.

8. Put the receiver into bind mode with the bind tab in the software. 

9. The software should tell you that you have successfully bound the receiver!


Wiring guide
-------------

+------------+------+----------------+----------------------+
| Output pin | Mode | Surface        | Inverted Transmitter |
+------------+------+----------------+----------------------+
| 8          | 19   | Left Elevator  | Yes                  |
+------------+------+----------------+----------------------+
| 9          | 21   | Rudder         |                      |
+------------+------+----------------+----------------------+
| 11         | 2    | Left Flap      |                      |
+------------+------+----------------+----------------------+
| 5          | 4    | Left Aileron   | Yes                  |
+------------+------+----------------+----------------------+
| 10         | 2    | Right Flap     |                      |
+------------+------+----------------+----------------------+
| 12         | 4    | Right Aileron  | Yes                  |
+------------+------+----------------+----------------------+
| 3          | na   | Throttle       |                      |
+------------+------+----------------+----------------------+
| 7          | 19   | Right Elevator | Yes                  |
+------------+------+----------------+----------------------+

Hexacopter Setup
----------------

Atlas is a portable, lightweight test system to allow subteams to test without needing to do a full test flight. It is able to carry several pounds of payloads that can be mounted as necessary and is significantly easier to fly than a fixed wing aircraft. 

The base onboard electronics include:

- 1x `Pixhawk <https://3dr.com/wp-content/uploads/2014/03/pixhawk-manual-rev7.pdf>`_ autopilot with gps module running `ArduCopter <http://ardupilot.org/copter/>`_

- 6x `30A ESCs <https://hobbyking.com/en_us/turnigy-multistar-30a-slim-v2-esc-with-blheli-opto-2-6s.html>`_

- 1x `RFD900 <http://cuairautopilot.readthedocs.io/en/latest/autopilot_configuration.html#id3>`_ -- setup is identical to the plane radios.

ArduCopter setup is very similar to ArduPlane setup and is completely documented `here <http://ardupilot.org/copter/docs/initial-setup.html>`_. The key difference is `ESC calibration <http://ardupilot.org/copter/docs/esc-calibration.html>`_ which must be re-done after major system changes like receiver replacement or motor replacement. 

Atlas flight instructions can be found `here <https://docs.google.com/a/cornell.edu/document/d/1p07ljg8zF4MjSbM2MOx6P8YeXyO3xy7GhyED3VAolZA/edit?usp=sharing>`_.

Telemetry to autopilot wire pin out 
-----------------------------------

+----------------------------------+--------+--------------------+
| RFD side (Left when flat side up)|        | Autopilot side left|
+----------------------------------+--------+--------------------+
| 1                                | white  | 6                  |
+----------------------------------+--------+--------------------+
| 2                                | black  | 1                  |
+----------------------------------+--------+--------------------+
| 3                                | black  | 5                  |
+----------------------------------+--------+--------------------+
| 4                                | red    | 2                  |
+----------------------------------+--------+--------------------+
| 5                                | black  | 3                  |
+----------------------------------+--------+--------------------+
| 6                                | black  | 4                  |
+----------------------------------+--------+--------------------+
| right                            | white  | right              |
+----------------------------------+--------+--------------------+

