# 1. Register at Amazon

First you need to obtain a set of credentials from Amazon to use the Alexa Voice service. Make a note of these credentials as you will be asked for them during the install process.

- Login at [https://developer.amazon.com](https://developer.amazon.com) and go to `ALEXA`, then `Alexa Voice Service`.
- `Register a Product Type` > `Device`. 
- You are at `Device Type Info` left tab.
    - For the `Device Type ID` and `Display Name` use something like _AlexaPi_ or whatever you want.
     - `Next`
- You are at `Security Profile` left tab.
    - From the drop-down menu choose `Create a new profile`. 
    - Choose whatever for `Security Profile Name` and `Security Profile Description`. Hit `Next`.
    - Under `Web Settings` horizontal tab hit `Edit` and: 
        - `Allowed Origins` - put there `http://localhost:5050` and `http://ALEXA.DEVICE.IP.ADDRESS:5050` 
        - `Allowed Return URLs` put `http://localhost:5050/code` and `http://ALEXA.DEVICE.IP.ADDRESS:5050/code`. 
        You have to replace `ALEXA.DEVICE.IP.ADDRESS` with the IP (for example 192.168.1.123) of your AlexaPi device (for example Raspberry Pi). This is especially necessary when you are installing from another computer than AlexaPi is gonna run on.
- Fill some of the other stuff in.

# 2. Install AlexaPi

## Linux

1. Boot your PC and login to a command prompt.
2. Make sure you are in `/opt` by issuing

    ```
    cd /opt
    ```
3. Make sure you have git installed
    
    ```
    sudo apt-get install git # For Debian OSs (Debian, Raspbian, OSMC, OpenElec...)
    sudo pacman -Sy git # For Arch Linux
    ```

4. Clone this repo
    
    ```
    sudo git clone https://github.com/alexa-pi/AlexaPi.git
    ```
    
    NOTE: You can also clone the repository to any other directory (and lose the `sudo` here, if you have permission to write to that directory), but you won't be able to run AlexaPi on boot with our init scripts. It is therefore recommended for advanced users (who know what they're doing) only.     

5. Run the setup script

    ```
    sudo ./AlexaPi/src/scripts/setup.sh
    ```

    Follow instructions...

## Windows

You need to have theses dependencies:
* [Python](https://www.python.org/downloads/windows/) (tested with 3.6, needs pip)
* ~~[Visual C++ 2015 Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools)~~
* ~~Swigwin-AlexaPi (See on the installation steps)~~
* [VLC](http://www.videolan.org/vlc/download-windows.html)

You have now two option:

### Install with AlexaPiWrapper for Windows

* Download and install [the latest version of AlexaPiWrapper](https://github.com/EmerickH/AlexaPiWrapper/releases/latest)
* Run AlexaPiWrapper **as administrator!**
* Wait for downloading and unzipping
* When the install script appears, follow the instructions (see [below](#setup-script))
* Done!
To stop AlexaPi, right click on the Alexa icon on the taskbar and choose **Exit**

### Install manually

* Download this repo (with git for Windows or with the [ZIP package](https://github.com/alexa-pi/AlexaPi/archive/master.zip))
* ~~Download swigwin-AlexaPi (with git for Windows or with the [ZIP package](https://github.com/EmerickH/swigwin-AlexaPi/archive/master.zip)) an put the `swigwin-AlexaPi-master` folder in the `src/scripts` folder~~
* Run src/scripts/setup.bat (see [below](#setup-script) for instructions)
To run, start **start.bat**
If it's not working, please start **debug.bat** and copy/paste the log in a new issue.

Enjoy :)

### Setup script
1. The install script will download and install Python dependencies (press any key to continue when finished)
2. Modify the src/config.yaml file to add your Amazon keys :
```
# Amazon Alexa settings
alexa:
  Client_ID: ""
  Client_Secret: ""
  Device_Type_ID: ""
  Security_Profile_Description: ""
  Security_Profile_ID: ""
  refresh_token: 
```
3. Press any key to continue
4. Go to `http://<yourlocalip>:5050` or `http://localhost:5050` on your favorite browser and authorize the Amazon API
5. Close the window when finished

# 3. Post-installation steps (For Linux)

Now that you have installed AlexaPi there's a couple of things you need to do.

**DO NOT REPORT AN ISSUE UNLESS YOU HAVE READ THIS THOROUGHLY!**

- Reboot your machine **or** start AlexaPi with 
    ```
    sudo systemctl start AlexaPi.service
    ```
- Check the status of AlexaPi with 
    ```
    sudo systemctl status AlexaPi.service
    ```
    If it is not running, be sure to see the full **[logs](https://github.com/alexa-pi/AlexaPi/wiki/Debugging#logs)**.

- In a lot of cases, you have to **setup your input / output devices properly** in the configuration file. Read the **[Audio setup & debugging](https://github.com/alexa-pi/AlexaPi/wiki/Audio-setup-&-debugging)** section in the documentation.

- If you have a **desktop OS** (such as default Raspbian), you have to set up **[system-wide PulseAudio](https://github.com/alexa-pi/AlexaPi/wiki/Audio-setup-&-debugging#pulseaudio)**. You usually get _dbus_ and _pulseaudio_ error in the log if you don't do this.

- If you got this working, but **audio playback is choppy**, try changing the playback handler in the [config](https://github.com/alexa-pi/AlexaPi/wiki/Configuration-file) from _vlc_ to _sox_. This will be default in later versions of AlexaPi.

- **READ THE WHOLE [DOCUMENTATION](https://github.com/alexa-pi/AlexaPi/wiki) BEFORE ASKING.**

Enjoy :)
