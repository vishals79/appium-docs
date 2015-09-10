	 	 	
#Selendroid Architecture:

Selendroid has two major parts:

Selendroid Standalone server: a netty server that runs on the machine.

Selendroid Server:  another netty server that runs on the device.

From http://selendroid.io/architecture.html

![alt tag](https://docs.google.com/drawings/d/1Mo1YWUBgDNzcIBSq8EuyBjNhgpQk-3F91lEt9_43ueQ/pub?w=772&h=298)

* Selendroid-Client  - 	the java client library (based on the selenium java client).
* Selendroid-Server  - 	that is running beside your app on the Android device.	
* AndroidDriver-App  - 	a built in Android driver webview app to test the mobile web.	
* Selendroid-Standalone  - manages different Android devices by installing the 	selendroid-server and the app under test.

##Source code flow: (Selendroid Standalone)

The three main module of the project I debugged through are
* Selendroid-Standalone
* Selendroid-Server
* Selendroid-server-common

Selendroid-server-common has code that is responsible for routing the requests from the client to either Standalone server or Selendroid server.

The class responsible for Standalone Server start up is `SelendroidLauncher.java`

The `launchServer()` method of this class creates an instance of SelendroidStandaloneServer (`SelendroidStandaloneServer.java`) which is actually a netty server. While this instantiation happens this server registers two handlers named StatusServlet and SelendroidServlet.

`StatusServlet` - used only for the status request of the server. [http://localhost:4444/wd/hub/status](http://localhost:4444/wd/hub/status).
`SelendroidServlet` - registers all the required handler for the incoming requests (**POST,GET**)

There are three other servlets that are registered with selendroid server that runs on the device. All these servlets implement `HttpServlet` which declares the method `handleHttpRequest`.

While starting up SelendroidStandaloneServer insantiates `SelendroidStandaloneDriver` where initialization of the connected devices, Server port and of other configurations happen. These properties will be used while processing any request that is received by Standalone server.

`BaseServlet.handleHttpRequest()` method finds an handler that can process any particular request based on the url (or JSON body). 

All the handlers of SelendroidStandaloneServer are present under the package `io.selendroid.standalone.server.handler`. 

One of the handlers is `CreateSessionHandler`. This handler is invoked at the very first invocation of any action on the device for example, `findElement (someId)`. 
SelendroidStandaloneDriver has a method `createNewTestSession` method which gerenarates a seesionId and also pushes the **selendorid-server apk** on to the connected devices and starts the server (walk through the code for better understanding)

##Source code flow: (Selendroid server)

`ServerHandler` from Selendroid-server-common is the common class for both standalone and selendroid server which redirects the incoming requests to appropriate handler based on the request type.

Like `SelendroidServlet.java` for standalone server, `AndroidServlet.java` registers all the required handlers for selendroid server. Again for selendroid server as well `BaseServlet` finds the right handler based on the request type.

All the handlers for selendroid server are present under the package `io.selendroid.server.handler`.




