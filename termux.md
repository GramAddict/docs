
# Use GramAddict without pc


## Step 1: Download and Install Termux

https://f-droid.org/repo/com.termux_113.apk

## Step 2: Install required packages

    pkg upgrade -y
	curl -LO https://its-pointless.github.io/setup-pointless-repo.sh
	bash setup-pointless-repo.sh
    pkg install android-tools python build-essential cmake libjpeg-turbo libpng python libxml2 libxslt freetype git numpy -y
    pip install wheel

## Step 2: Install gramAddict

This procedure is slow use -vvv in pip if you want to see if everything installing alright
	

    git clone https://github.com/patbengr/bot.git gramaddict
    cd gramaddict
    pip install -r requirements.txt
    
## Step 3: Run
	

    python -m uiautomator2 init
    python run.py
    
## How can I access termux files?
Read that article
https://wiki.termux.com/wiki/Internal_and_external_storage

The easiest solution is to download an storage access framework compatible file manager like
FX File Explorer: https://play.google.com/store/apps/details?id=nextapp.fx
Then you can follow that instructions
https://wiki.termux.com/images/e/e5/FX_Termux_Home.jpg

Then you can edit and view gramaddict files.
    


