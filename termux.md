# Use GramAddict without pc


## Step 1: Download and Install Termux

https://f-droid.org/repo/com.termux_113.apk

## Step 2: Install required packages

    pkg upgrade -y
	curl -LO https://its-pointless.github.io/setup-pointless-repo.sh
	bash setup-pointless-repo.sh
    pkg install android-tools python build-essential cmake libjpeg-turbo libpng python libxml2 libxslt freetype git numpy -y

## Step 2: Install gramAddict
	

    git clone https://github.com/patbengr/bot.git gramaddict
    cd gramaddict
    pip install -r requirements.txt
    
## Step 3: Run
	

    python -m uiautomator2 init
    python run.py
    
    

