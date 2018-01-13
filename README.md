# MeteorOdroidReceiver

This is a fork of MeteorRpiReceiver. It has been modified to work with Odroid, Linux and Mac.

A set of python scripts to automatically capture, decode Meteor-M2 satellite images.

This project uses a good ol' DVB-T stick and gnuradio to capture the raw data. The processing of the raw data is performed by 'medet' (medet_arm in this case) developed by Artlav.

The only part which is a bit harder to get over-the-counter is the antenna. I would recommend a QFH antenna, but e.g. crossed dipoles seem to render good results for others. Plans to build them are scattered across the internet.

The 'scheduler' python script is all you need to run.

### Let's get started

1. Install required modules. You'll need pip

   To install pip:

```
$ sudo apt-get install python-pip python-dev build-essential
$ sudo pip install --upgrade pip
```

   To install the required modules:
```
$ sudo pip install -r requirements.txt
```

2. Edit user_location.txt. I retrieve my lat lon using Google Maps. The numbers are found in the url.


3. Execute scheduler.py. This will download satellite pass schedules from Celestrak

```
$ ./scheduler.py
```

   Note(s): Please report if there are other modules that won't be found. I'll add it to requirements.txt.

   Tip(s): manually execute the binaries in bin directories to find out if it is working or not.


3. Done!



### In summary:

The script will:
- create a log file
- create the Data, Images and TLE directories if they don't exist
- load the user location from user_location.txt (you need to modify this file with your location)
- calculate the current position of Meteor-M2 and wait for it to appear above the horizon
- launch the GRC script (some paths might need to be modified in the GRC script to match your wishes)
- wait for the satellite to disappear under the horizon again
- stop the GRC script
- decode the raw data using medet_arm by Artlav
- process the raw image (if any was decoded) into a daytime and nighttime image (122 & 555)
- calculate and wait for the satellite to appear above the horizon again
- etc.

Have fun!

Notes:
- In a couple of weeks time, I only had to reboot my rPi once as the GRC script was not producing any data. No idea what the issue was, but just a heads up. It was obvious by the generation of .s files with 0Bytes size.
- This is/was my introduction to Python, all improvements are most welcome!
