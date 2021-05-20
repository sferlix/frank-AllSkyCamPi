# frank-AllSkyCamPi
An AllSkyCam software for Raspberry Pi and Pi HQ Camera, Pi Camera 2 and NoIr
by Francesco Sferlazza - sferlazza@gmail.com

This software is intended to collect all-sky images with Raspberry Pi
It allows you to get real-time image of the sky, to generate timelapse and startrail images.

Automatic exposure based on sun rise/sun set, moon presence and illumination.
This is a very lite software.

Hardware / OS requirements: 
I've tested it on Raspberry Pi4, 4GB RAM, Pi HQ Camera with fisheye, SD Card 64GB
Raspbian Lite, no desktop.
Being really lite, I guess no problems if you run it on Pi3 and 2GB

Optionally, you can also get (if, so contact me !):
- script to control relays for dew heater and cooling fan
- script to read temperature and humidity 

## INSTALLATION

pre-requisites:

you will need to install pip:

`sudo apt install python3-pip`

and the pytz library (https://pypi.org/project/pytz/)

`pip3 install pytz` 

if you want automatically generate timelapses, then you need to install ffmpeg:

`sudo apt install ffmpeg`


Then, install with:

`pip3 install frank-AllSkyCamPi`

in case of update, use:

`pip3 install frank-AllSkyCamPi==<x.y.z>`

where x.y.z is the last version number
E.g. if last version is 1.12.0, then you need to type:

`pip3 install frank-AllSkyCamPi==1.12.0`

 
After installing, please configure your own parameters in the file:

`/home/pi/.local/lib/python3.7/site-packages/allskycam/config.txt`

## USE

Before running the allskycam, ensure that:

- you have configured your parameters in config.txt
- output folder exist (e.g. images)

then, you can launch:

`python3 -m allskycam` 

it will generate:
1) skycam_yyyyMMdd_hhmmssssssss.jpg in the output folder (you may use it to build timelapse and startrails)  
  
2) .jpg file in your local webfolder (if needed. file name to be defined in config.txt)

3) .jpg file in your remote FTP Server (if needed. file name to be defined in config.txt)

To make everything automatic, please you need to add some lines in crontab. 
To do so, open the crontab:

`crontab -e`

and add the following lines:


`*/3 0-8,16-23 * * * python3 -m allskycam >/dev/null 2>&1`

`* 9-15 * * * python3 -m allskycam >/dev/null 2>&1`

`0 1 * * *    python3 -m allskycamdelete >/dev/null 2>&1`

`1 9 * * *    python3 -m timelapse >/dev/null 2>&1`


the 1st line collect an all-sky image every 3 minutes from 4pm to 9am
the 2nd line collect an all-sky image every 1 minute from 9am to 4pm
the 3rd line deletes images older than XX days from your output folders (XX can be defined in config file. Default = 3 )
the 4th line automatically generates a 24h timelapse from 9am to 9am every day at 9:01

files:

1) `__main__.py       `=> main program
2) `imageHeader.py    `=> module for calculating moon/sun rise/set and moon phase 
3) `fileManager.py    `=> module for managing file uploads to ftp, copy, and so on
4) `suncalc2.py       `=> The moon/sun calculation based on SuncalcPy library (https://github.com/Broham/suncalcPy) 
5) `timelapse.py      `=> module for generating timelapse
6) `allskycamdelete.py`=> module for cleaning up old files and folders
7) `config.txt        `=> configuration file (e.g. lat, log, timezone,..)



