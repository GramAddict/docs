# Use GramAddict without pc


## Step 1: Download and Install Termux

https://f-droid.org/repo/com.termux_113.apk

## Step 2: Install required packages

    pkg upgrade -y
    apt update > /dev/null 2>&1 && apt --assume-yes install wget > /dev/null 2>&1 && wget https://github.com/MasterDevX/Termux-ADB/raw/master/InstallTools.sh -q && bash InstallTools.sh
    pkg install android-tools python build-essential cmake libjpeg-turbo libpng python libxml2 libxslt freetype numpy -y
