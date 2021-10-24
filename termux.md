
# Use GramAddict without pc


## Step 1: Download and Install Termux

[Apk from f-droid](https://f-droid.org/repo/com.termux_113.apk)
or
[Official PlayStore](https://play.google.com/store/apps/details?id=com.termux)

## Step 2: Install required packages

    pkg upgrade -y
	curl -LO https://its-pointless.github.io/setup-pointless-repo.sh
	bash setup-pointless-repo.sh
    pkg install android-tools python build-essential cmake libjpeg-turbo libpng libxml2 libxslt freetype git -y
    pip install wheel

## Step 3: Install GramAddict

This procedure is slow, use -vvv in pip if you want to see if everything installing alright
	
    git clone https://github.com/gramaddict/bot.git gramaddict
    cd gramaddict
    pip install -r requirements.txt

You can also install GramAddict using pip, but in that case you won't have the config-example folder ready to go.
    
## Step 4: Run
	
    python -m uiautomator2 init
    python run.py
    
## How can I access termux files?
Read that article
https://wiki.termux.com/wiki/Internal_and_external_storage

The easiest solution is to download an storage access framework compatible file manager like
[FX File Explorer](https://play.google.com/store/apps/details?id=nextapp.fx)
Then you can follow that instructions
https://wiki.termux.com/images/e/e5/FX_Termux_Home.jpg
Then you can edit and view GramAddict files.

## Troubleshooting
* if you type on termux `adb devices` and you get a blank list try the following:
	* connect the phone to a PC and get sure you get your device ID in `adb devices` (from pc console)
	* `adb tcpip 5555`
	* `adb kill-server` and disconnect the cable
	* get back on termux and write: `adb connect localhost:5555`
	* now you should be able to see your device ID in `adb devices`
* when I start the bot it looks like it freezes after opening IG and termux shell has been closed
	* edit your `accounts/yourusername/config.yml` file and set `close-apps: false`
	



**All credits to [patbengr](https://github.com/patbengr)**

