# Quick Start

Getting started is easy. Follow the directions below to get GramAddict installed and check out the [sensible examples](/?id=sensible-examples) to get rolling!

## Requirements

- Python 3.6+

## How to Install
1. Clone project: `git clone https://github.com/GramAddict/bot.git gramaddict`
2. Go to GramAddict folder: `cd gramaddict`
3. (Optionally) Use virtualenv or similar to make a virtual environment `virtualenv -p python3 .venv` and enter the virtual environment `source .venv/bin/activate`
4. Install required libraries: `pip3 install -r requirements.txt`
5. Download and unzip [Android platform tools](https://developer.android.com/studio/releases/platform-tools), move them to a directory where you won't delete them accidentally, e.g.
```
mkdir -p ~/Library/Android/sdk
mv <path-to-downloads>/platform-tools/ ~/Library/Android/sdk
```
6. [Add platform-tools path to the PATH environment variable](https://github.com/GramAddict/bot/wiki/Adding-platform-tools-to-the-PATH-environment-variable). If you do it correctly, terminal / command prompt command `adb devices` will print `List of devices attached`
7. Run the script `python3 run.py --blogger-followers username`

## How to Install on Raspberry Pi OS
1. Update apt-get: `sudo apt-get update`
2. Install ADB and Fastboot: `sudo apt-get install -y android-tools-adb android-tools-fastboot`
3. Clone project: `git clone https://github.com/GramAddict/bot.git gramaddict`
4. Go to GramAddict folder: `cd gramaddict`
5. (Optionally) Use virtualenv or similar to make a virtual environment `virtualenv -p python3 .venv` and enter the virtual environment `source .venv/bin/activate`
6. Install required libraries: `pip3 install -r requirements.txt`
7. Run the script `python3 run.py --blogger-followers username`

## Running GramAddict

If you have a screen lock pin or swipe, you will need to unlock the script before each use. Otherwise - the script will do it for you. Additionally, the script also handles opening Instagram for you as well.

1. Connect Android device to your computer with a USB cable
2. Enable [Developer options](https://developer.android.com/studio/debug/dev-options#enable) on the device
3. Switch on **USB debugging** (and **Install apps via USB** if there is such option) on the Developer options screen.
4. Device will ask you to allow computer connection. Press "Connect"
5. Type `adb devices` in terminal. It will display attached devices. There should be exactly one device unless you have multiple attached:
```
List of devices attached
A0B1CD2345678901	device
```
6. Finally run the script (it works on Python 3) using your preferred options outlined below:
```
cd <path-to-project>/gramaddict
python3 run.py --blogger-followers <username1> <username2> ...
```