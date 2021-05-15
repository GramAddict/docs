# Quick Start

Getting started is easy. Follow the directions below to get GramAddict installed and check out the [example configs](examples.md) to get rolling.

## Requirements

- Python 3.6+
- PIP
- ADB
- Only devices with Android 4.4+ (SDK 19) are supported.
  There are few emulators you can use instead: google for them. e.g. Memu, LDPlayer, Android Studio and so on.

<br /><br />

## Step 1: Install Python (if not installed)

### Windows

1. Open the Python website in your web browser and navigate to: [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/).
2. Download the latest Python 3 release. At this time, that release is [3.9.4](https://www.python.org/downloads/release/python-394/).
3. Run the setup file. Make sure you select the "Install launcher for all users" option as well as "Add Python 3.9 to PATH" checkboxes.
4. (If prompted) Choose to "Disable path length limit".
5. Test to make sure it's working. Open up **cmd** or **powershell** (if they are already open, close them first) and run `python –V` or `python3 –V`.
   (Multiple versions of Python can be installed alongside each other and which version of Python to use can be selected by the user. So refer to python/python3 according to the result of the version check above. Remember that the version must be 3.6+)
7. Test to make sure **pip** is installed by running `pip3 -V`. If it is not installed, download the [get-pip.py](https://bootstrap.pypa.io/get-pip.py) file and run `python3 get-pip.py` from the folder that contains the file you just downloaded.


### Mac

1. Start off by installing `brew` if it is not already installed: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
2. Install Python 3 with `brew install python`.
3. Verify that python3 and pip3 are installed: `python3 –V` and `pip3 -V`

<br /><br />

## Step 2: Install GramAddict

There are two ways to install GramAddict. Via `git` or via `pip`. If you plan on **modifying code**, **contributing**, **being a beta tester**, or otherwise **inspecting** the code. You should install GramAddict with `git`. Otherwise you should install it with `pip`. We recommend installing with `pip` for the average user. 

Regardless of which method you use, if you are familiar with `virtualenv` or if you plan on using/developing other python scripts, we recommend that you set up a **virtual environment**.

### Using `pip`

1. Create a new folder in the directory of your choice. A reccomentation would be in your user folder or documents folder.
2. Go into that folder: `cd gramaddict`
3. (Optionally) Use virtualenv or similar to make a virtual environment `virtualenv -p python3 .venv` and enter the virtual environment `source .venv/bin/activate`/`.venv\Scripts\activate.bat` (on windows)
4. Install GramAddict with **pip**: `pip3 install gramaddict`
5. Create a file named `run.py` with the following content in it (or [download it here](https://raw.githubusercontent.com/GramAddict/bot/master/run.py)): 

```
import GramAddict

GramAddict.run()
```


### Using `git`

1. Clone project: `git clone https://github.com/GramAddict/bot.git gramaddict`
2. Go to GramAddict folder: `cd gramaddict`
3. (Optionally) Use virtualenv or similar to make a virtual environment `virtualenv -p python3 .venv` and enter the virtual environment `source .venv/bin/activate`/`.venv\Scripts\activate.bat` (on windows)
4. Install required libraries: `pip3 install -r requirements.txt`

<br /><br />

## Step 3: Install `adb`

1. Download and unzip [Android platform tools](https://developer.android.com/studio/releases/platform-tools), move them to a directory where you won't delete them accidentally, e.g.
```
mkdir -p ~/Library/Android/sdk
mv <path-to-downloads>/platform-tools/ ~/Library/Android/sdk
```
2. Add platform-tools path to the PATH environment variable

```
Linux/macOS

    1. Open ~/.bash_profile with any text editor you like.
    2. Add the following line with the full path to the platform-tools directory: export PATH=~/Library/Android/sdk/platform-tools/:$PATH. This path may be different depending on the way you installed platform-tools.
    3. Save file and restart Terminal.

Windows

    1. On the Windows desktop, right-click My Computer.
    2. In the pop-up menu, click Properties.
    3. In the System Properties window, click the Advanced tab, and then click Environment Variables.
    4. In the System Variables window, highlight Path, and click Edit.
    5. In the Edit System Variables window, insert the cursor at the end of the Variable value field.
    6. If the last character is not a semi-colon (;), add one.
    7. After the final semi-colon, type the full path to the platform-tools directory: C:\Users\USERNAME\AppData\Local\Android\sdk\platform-tools. This path may be different depending on the way you installed platform-tools.
    8. Click OK in each opened window and restart Command Prompt.
```

If you do it correctly, terminal / command prompt command `adb devices` will print `List of devices attached`

<br /><br />

## Step 4: Run GramAddict

Now that all of the prep work is done, we can just about start the script. 

If you have not already you should make sure you have [Developer options](https://developer.android.com/studio/debug/dev-options#enable) turned on, **USB debugging** enabled, as well as **Install apps via USB** (if available) on your phone. 


### First Run
1. Connect Android device to your computer with a USB cable
2. Device will ask you to allow computer connection. Press "Connect"
3. Type `adb devices` in terminal. It will display attached devices. There should be exactly one device unless you have multiple attached:
```
List of devices attached
A0B1CD2345678901	device
```
4. Proceed to set up your [configuration](configuration.md) (important).
5. Finally, you can run the script from the location where you put the run.py file: 
```
python3 run.py --config accounts/username/config.yml
```
Possible problems:
- if you run the bot but nothing happens in console (you are able to write again..), you are using a wrong python alias (for example python3 run.py bla bla). Type `python -V` or `python3 -V` or `py -V` to find out the right one and then use it with the run.py
- if uiautomator2/minicab install stucks, try the following: 
```
adb shell pkill atx-agent
pip3 install uiautomator2 --upgrade
```
Wait until is finished and try to run the bot again.

### Subsequent Runs:
1. Connect Android device to your computer with a USB cable
2. (optionally) If you installed the script with **virtualenv**, be sure to activate your environment before running: `source .venv/bin/activate`/`.venv\Scripts\activate.bat` (on windows)
3. run the script: 
```
python3 run.py --config accounts/username/config.yml
```

> Note: If you have a screen lock pin or swipe, you will need to unlock the script before each use. Otherwise - the script will do it for you each run. Additionally, the script also handles opening Instagram for you and choosing the correct account among the ones logged into the app. Disable notifications will allow the bot to run smootly without interferences.
