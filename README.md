# frank-AllSkyCamPi
A lite AllSkyCam for Raspberry Pi
by Francesco Sferlazza - sferlazza@gmail.com

This software is intended to collect all-sky images with Raspberry Pi, Pi HQ Camera and every camera that is compatible with it.

Hardware / OS requirements: 
I've tested it on Raspberry Pi4, 4GB RAM, Pi HQ Camera with fisheye, SD Card 64GB
Raspbian Lite, no desktop.
Being really lite, I guess no problems if you run it on Pi3 and 2GB

Optionally, you can also get (if, so contact me !):
- script to control relays for dew heater and cooling fan
- script to read temperature and humidity 

___INSTALLATION

pre-requisites:

__`sudo apt install python3-pip`
__`pip3 install pytz` 

Then, install with:

__`pip3 install frank-AllSkyCamPi`

After installing, please configure your own parameters in the file:

`/home/pi/.local/lib/python3.7/site-packages/allskycam/config.txt`

___USE

`python3 -m allskycam` 

it will generate:
1) skycam_<timestamp>.jpg in the output folder (you may use it to build timelapse and startrails)
2) .jpg file in your local webfolder (if needed. file name to be defined in config.txt)
3) .jpg file in your remote FTP Server (if needed. file name to be defined in config.txt)

please note that the command line need to be added as cron job. 
To do so, open the crontab:

`crontab -e`

and add the following lines:
`
0 1 * * * find /home/pi/sky/img/ -mtime +2 -type f -delete >/dev/null 2>&1
*/3 0-8,16-23 * * * sudo killall raspistill; python3 /home/pi/sky/skycamv4.py >/dev/null 2>&1
* 9-15 * * * sudo killall raspistill; python3 /home/pi/sky/skycamv4.py >/dev/null 2>&1
`
files:

1) `__main__.py     `=> main program
2) `imageHeader.py  `=> module for calculating moon/sun rise/set and moon phase 
3) `upload.py       `=> module for uploading images on a FTP server
4) `suncalc2.py     `=> The moon/sun calculation based on SuncalcPy library (https://github.com/Broham/suncalcPy) 
5) `config.txt      `=> configuration file (e.g. lat, log, timezone,..)


