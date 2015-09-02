# Brief notes on Mobile JSON wire protocol

## WebDriver and Selenium
The way selinum used to work to automate web applications is by injecting javascript code into the browsers, the subsequent actions like entering keywords, clicking a button, etc will be driven by javascript.

On the other hand WebDriver works by invoking the browser’s native commands directly at the OS level.
Web driver is an interface, the implementations of web driver are:
Firefox driver, Chrome driver, InternetExplorerDriver, etc

https://selenium.googlecode.com/git-history/master/docs/api/java/org/openqa/selenium/WebDriver.html

Unlike Selenium-RC, if there comes a new browser into existences a new webdriver has to be implemented for supporting that browser.

The advantage of using WebDriver is that you can write scripts is any programming language. All the web drivers will understand one common protocol i.e JSON wire protocol. The conversion of objects to JSON objects is done by the language specific library you include in your classpath.

In addition to the drivers mentioned above there is also Android Driver/Selendroid for mobile devices, these drivers are used only for automating any web application in the mobile browsers.

Mobile JSON wire protocol is an extension of JSON wire protocol which is used automate apps apart from the browsers. This protocol extends JSON protocol and also includes additional actions like swipe, pinch, etc.

https://code.google.com/p/selenium/wiki/JsonWireProtocol

## Testing Appium API

I tried invoking the REST API exposed by Appium server by using a chrome REST client and a sample JSON object (Desired Capabilities Object).

This needs appium server running with at least one device or emulator connected.

I’m doing a POST on http://127.0.0.1:4723/wd/hub/session (url of appium server) with POST body containing a desired capabilities JSON.

{"desiredCapabilities": {"newCommandTimeout":120,"app":"/home/prakashg/Appium/AppiumDemo-master/src/app-debug.apk","platformName":"Android","deviceName":"Android Emulator"}}

Appium gives a response with a sessionId:

{
status: 0
value: 
{
platform: "LINUX"
browserName: "Android"
platformVersion: "5.1"
webStorageEnabled: false
takesScreenshot: true
javascriptEnabled: true
databaseEnabled: false
networkConnectionEnabled: true
locationContextEnabled: false
warnings: 
{
}
desired: 
{
newCommandTimeout: 120
app: "/home/prakashg/Appium/AppiumDemo-master/src/app-debug.apk"
platformName: "Android"
deviceName: "Android Emulator"
}
-
newCommandTimeout: 120
app: "/home/prakashg/Appium/AppiumDemo-master/src/app-debug.apk"
platformName: "Android"
deviceName: "emulator-5554"
}
-
sessionId: "dca80aa5-41dc-435e-8a12-c37477e09b72"
}

This sessionId will be used in all subsequent requests like selecting an element or scrolling a screen.
ex: /session/:sessionId/element , session/:sessionId/touch/scroll


Corrections or edits are welcome.



