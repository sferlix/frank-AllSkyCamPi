# frank-AllSkyCamPi
A lite AllSkyCam for Raspberry Pi
by Francesco Sferlazza - sferlazza@gmail.com

This software is intended to collect all-sky images with Raspberry Pi, Pi HQ Camera and every camera that is compatible with it.

Install with:

pip3 install frank-AllSkyCamPi

files:

1) __main__.py  => main program
2) imageHeader.py  => module for calculating moon/sun rise/set and moon phase 
3) upload.py => module for uploading images on a FTP server
4) suncalc2.py => The moon/sun calculation based on SuncalcPy library updated 
5) config.txt => configuration file (e.g. lat, log, timezone,..)

Hardware / OS requirements: 
I've tested it on Raspberry Pi4, 4GB RAM, Pi HQ Camera with fisheye, SD Card 64GB
Raspbian Lite, no desktop.
Being really lite, I guess no problems if you run it on Pi3 and 2GB

Optionally, you can also get (if, so contact me !)
- script to control relays for dew heater and cooling fan
- script to read temperature and humidity 

