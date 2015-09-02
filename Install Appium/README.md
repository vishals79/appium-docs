# Install Appium

## Steps For Linux

### Prerequisites
1. Node.js
2. NPM

### Install Appium

npm install -g appium

### Andoid SDK

1. Download - https://developer.android.com/sdk/installing/index.html and extract to a folder

2. set $ANDROID_HOME to be your Android SDK path. If you unzipped the Android SDK to /usr/local/adt/, for example, you should add this to your shell startup:
export ANDROID_HOME=“/usr/local/adt/android-sdk-linux”
3. Include %ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\platforms; in PATH variable.

### Create AVD
Go to tools folder inside your android-sdk-linux.

	android avd

* Create a device using proper configuration.

### Start Device
Go to tools folder inside your android-sdk-linux.

	emulator -avd <device-name>

### Start Appium
 appium &

### Sample test cases
Sample Code - https://github.com/appium/sample-code

e.g Clone the code and go to sample-code/examples/java/junit

Run a test : mvn -Dtest=com.saucelabs.appium.SimpleTest test


## Steps For Windows

Link : http://qaautomationworld.blogspot.in/

## References:
1. http://appium.io
2. http://appium.io/slate/en/tutorial/android.html?java#introduction
3. http://qaautomationworld.blogspot.in/
4. https://github.com/appium/appium




