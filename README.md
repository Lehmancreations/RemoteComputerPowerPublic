# Remote Computer Power Public

This is the public repo for the documentation of the Remote computer power project

Welcome to the RemoteComputerPower wiki!

### What is Remote Computer Power? ###

The hardware allows you to view the power state of a computer as well as commanding the power on and off.

### How to use the software ###
Power the board up and a new wifi network is set up. Use your phone to join the network. Once connected on your phone choose the settings for your wifi network and mqtt server. The device will reboot and connect to your wifi and MQTT server

### MQTT ###
**to send commands to power on or off your computer the topic is**
**RCP/cmnd/HOSTNAME/**
if the payload is OFF it will turn the computer off
if the payload is ON it will turn the computer on
if the payload is FORCE OFF it will force the pc off
if the payload is RESET WLAN it will wipe wifi settings and reboot with the local wifi so you can connect with your phone and reconfigure the settings. 
if the payload is FIRMWARE VERSION it will send back the firmware version on the board

**receive data from the board**
every 60 seconds the board will report the status of the computer in the topic RCP/state/HOSTNAME
every 2 minutes the board will report that it is OK to the topic RCP/state/HOSTNAME.

when the board powers up it will send a message to RCP/state/HOST/PCMCU with Online and when the board goes offline it will send a message offline to that same topic. these messages are retained so you will always know if it is online or off

Also when it powers up it will send a message as to whether it was reconnected or rebooted to the topic RCP/state/HOSTNAME/PCMCU/boot

It will also send the IP address and the firmware version in the topics RCP/state/HOST/PCMU/IP and RCP/state/HOST/PCMU/Firmware

### HTTP ###
If you go to the ip address of the board you will get information on the board (you will have to sign in with the username and password for the firmware update

If you go to ip address/reset_wlan it will erase the wifi settings, reboot, and allow you to connect to its wifi access point and reconfigure the device.

If you go to ip address/version it will tell you what firmware version it is running

If you go to ipaddress/firmware (this is configurable in the setup) you can update the firmware on the machine
