# Use GramAddict without pc


## Step 1: Download and Install Termux

https://f-droid.org/repo/com.termux_113.apk

## Step 2: Install required packages

    pkg upgrade -y
	curl -LO https://its-pointless.github.io/setup-pointless-repo.sh
	bash setup-pointless-repo.sh
    pkg install android-tools python build-essential cmake libjpeg-turbo libpng python libxml2 libxslt freetype numpy -y

