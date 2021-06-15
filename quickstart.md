# Quick Start

Getting started is easy. Follow the directions below to get GramAddict installed and check out the [example configs](examples.md) to get rolling.

## Requirements

- Python 3.6+
- PIP
- ADB
- Only devices with Android 4.4+ (SDK 19) are supported.
  There are a few emulators you can use instead: google for them. e.g. Memu, LDPlayer, Android Studio and so on.
- Your Instagram app must be in English https://help.instagram.com/111923612310997

<br /><br />

## Step 1: Install Python (if not installed)

### Windows

#### 1. Download the [latest Python 3 release.](https://www.python.org/downloads/windows/)
  
   * As of the time of this writing, the latest version is [3.9.4.](https://www.python.org/downloads/release/python-394/)

#### 2. Run downloaded setup and make sure to __check these boxes__:
   * [x] Install launcher for all users
   * [x] Add Python 3.9 to PATH
   * [x] (*If prompted*) Disable path length limit

#### 3. Verify that `python3` is now installed -> in CMD (or PowerShell):

   ```
   python –V
   ``` 
   or
   ```
   python3 –V
   ```
   Your machine may have multiple versions of Python installed, depending on which is selected by default you would have to use `python` *OR* `python3` later on, based on the results of version check commands from the above. Remember that the version must be 3.6+

#### 4. Verify that `pip3` is now installed - in CMD (PowerShell):
    
   ``` 
   pip3 -V
   ```
   If it is not installed, download [get-pip.py](https://bootstrap.pypa.io/get-pip.py) (right click on the link -> save as) and run `python get-pip.py` from the same folder where you just downloaded the file.
   
<br />

### Mac

#### 1. Install `brew`:
   ```
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
#### 2. Install Python 3:
  ```
  brew install python
  ```
#### 3. Verify that `python3` and `pip3` are now installed:
  ```
  python3 –V && pip3 -V
  ```

<br />

### Linux

On Linux Python is pre-installed. 
For Raspberry the pre-installed version should be 3.6. Check this out by running this command: `python3 -V`
If you have a over version of python, google for how to upgrade.

<br /><br />

## Step 2: Install GramAddict

There are two ways to install GramAddict. Via `git` or via `pip`. If you plan on **modifying code**, **contributing**, **being a beta tester**, or otherwise **inspecting** the code. You should install GramAddict with `git`. Otherwise you should install it with `pip`. We recommend installing with `pip` for the average user. 

Regardless of which method you use, if you are familiar with `virtualenv` or if you plan on using/developing other python scripts, we recommend that you set up a **virtual environment**.

### Using `pip`

1. Create a new folder in the directory of your choice. A recommendation would be in your user folder or documents folder.
2. Go into that folder: `cd gramaddict`
3. (Optionally) Use virtualenv or similar to make a virtual environment `virtualenv -p python3 .venv` and enter the virtual environment `source .venv/bin/activate`/`.venv\Scripts\activate.bat` (on windows)
4. Install GramAddict with **pip**: `pip3 install gramaddict`
5. Create a file named `run.py` with the following content in it (or [download it here](https://raw.githubusercontent.com/GramAddict/bot/master/run.py) (right click on the link -> save as)): 

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

Using Shell (expert mode) 
```
mkdir -p ~/Library/Android/sdk
mv <path-to-downloads>/platform-tools/ ~/Library/Android/sdk
```
Using Mouse (noob mode)
```
Create a new folder somewhere, Unzip it inside that and remember this PATH! You will need it for the next step.
```
2. Add platform-tools path to the PATH environment variable

```
Linux/macOS

    1. Open ~/.bash_profile with any text editor you like.
    2. Add the following line with the full path to the platform-tools directory: export PATH=~/Library/Android/sdk/platform-tools/:$PATH. This path may be different depending on the way you installed platform-tools.
    3. Save file and restart Terminal.

Windows

    1. Open Windows Explorer and right-click "My Computer" on left side.
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

If you have not already, you should make sure you have [Developer options](https://developer.android.com/studio/debug/dev-options#enable) turned on, **USB debugging** enabled, as well as **Install apps via USB** (if available) on your phone.

If you want to use an emulator and you're on Windows you can try with [Memu](https://www.memuplay.com/).
After installing it and opening it, type that in console to open the connection: `adb connect localhost:21503`


### First Run
0. Make sure that your Instagram is in English https://help.instagram.com/111923612310997
1. Connect Android device to your computer with a USB cable
2. Device will ask you to allow computer connection. Press "Connect"
3. Type `adb devices` in terminal. It will display attached devices. There should be exactly one device unless you have multiple attached:
```
List of devices attached
A0B1CD2345678901	device
```
This is the ID of your device, you should copy/paste it in your config file with the device paramether
e.g: device: A0B1CD2345678901
4. Initialize the uiautomator2 with this command: (It's also important when uiautomator2 gets updates) 
```
python3 -m uiautomator2 init
```
6. Proceed to set up your [configuration](configuration.md) (important).
7. Finally, you can run the script from the location where run.py file is located.
   For doing that open the console and move to the gramaddict location and type the following: 
```
python3 run.py --config accounts/yourusername/config.yml
```
**ATTENTION: run.py must be inside that folder because at start it moves almost all folders near it inside `accounts`!**

For avoid problems, compare your situatation with that before starting:

Tree of correct configuration for GIT:
```                                    
gramaddict/
    GramAddict/
        core/
            __init__.py
            ...
        plugins/
            __init__.py
            ...
        __init__.py
        version.py
    config-examples/
        ...
    res/
        ...
    setup.py
    ...
    accounts/
        youraccountname/
            config.yml
            telegram.yml
            filters.yml
            whitelist.txt
            blacklist.txt
            comments_list.txt
            pm_list.txt
    run.py
```
Tree of correct configuration for PIP:
```  
gramaddict/
    run.py
    accounts/
        youraccountname/
            config.yml
            telegram.yml
            filters.yml
            whitelist.txt
            blacklist.txt
            comments_list.txt
            pm_list.txt
```

#### Troubleshooting:
- if you run the bot but nothing happens in console (you are able to write again..), you are using a wrong python alias (for example python3 run.py bla bla). Type `python -V` or `python3 -V` or `py -V` to find out the right one and then use it with the run.py
- if uiautomator2/minicab install gets stuck, try the following: 
```
adb shell pkill atx-agent
pip3 install uiautomator2 --upgrade
python3 -m uiautomator2 init
```
Wait until it is finished and try to run the bot again.

### Subsequent Runs:
1. Connect Android device to your computer with a USB cable
2. (Optionally) If you installed the script with **virtualenv**, be sure to activate your environment before running: `source .venv/bin/activate`/`.venv\Scripts\activate.bat` (on windows)
3. Run the script: 
```
python3 run.py --config accounts/yourusername/config.yml
```

> Note: If you have a screen lock pin or swipe, you will need to unlock the script before each use. Otherwise - the script will do it for you each run. Additionally, the script also handles opening Instagram for you and choosing the correct account among the ones logged into the app. Disable notifications will allow the bot to run smootly without interferences.
