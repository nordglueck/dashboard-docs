This section goes more into detail on how to develop the front end locally. 
While the installation is covered on the installation page, 
this section also provides details on which settings one might configure for their specific environment.

After the installation of all npm modules, the most important command to get things running in a local environment is:

```console

npm run serve

```

This will serve the Vue.js App locally. Keep in mind that you should have the Docker container with the backend running
locally as well to be able to exchange data. The terminal is going to give some output similar to this:

```console

 DONE  Compiled successfully in 6342ms                                                                                                                                                   11:57:49 AM


  App running at:
  - Local:   http://localhost:8080/ 
  - Network: http://localhost:8080/

  Note that the development build is not optimized.
  To create a production build, run npm run build.


```

However, due to the configurations, you should be able to reach the page at ``http://localhost:8000``, which is recommended,
as everything else (such as the Django Admin panel, the API Docs etc.) are also operating on this port.


### Hot reloading

Developing in Vue.js and serving the web app as shown before should enable you to see changes made to the app immediately
without restarting anything. This is called hot reloading and might be familiar when someone is experienced in flutter or something
like that. However, this system has it's flaws and might not work as expected from time to time. This may be due to several
reasons. A good idea in this case is to 1. try and quit the process and restart ``npm run serve`` or in a harder case 2. quit the process, 
delete all caches and restart ``npm run serve`` or as a last option 3. quit the process, delete all caches, run ``npm run build`` and then 
restart ``npm run serve``.


### Vue.js Plugin

Besides the Hot Reload functionality, that makes developing in Vue.js very comfortable, the Vue.js Plugin for Chromium-based browsers comes in very
handy as well. 

The Vue.js devtools provide functionality such as browsing through the different components and observing different states of data objects.
In addition to that it is possible to track the vuex flow, i.e. the triggering events, the mutations and the states before and after a mutation was made.

<img src="https://raw.githubusercontent.com/vuejs/devtools/main/media/screenshot-shadow.png" width=87%>
<br>
source: [https://raw.githubusercontent.com/vuejs/devtools/main/media/screenshot-shadow.png](https://raw.githubusercontent.com/vuejs/devtools/main/media/screenshot-shadow.png)


### Debug/track WebSocket messages

Via the devtools in every modern browser it is possible to track the websocket messages that are being exchanged between the back end and the front end.
However, one needs to pay respect to some peculiarities. The following shows, how debugging/tracking WebSocket messages in general works.

- Open the devtools of the browser
- Navigate to the **Network** tab
- Inside the Network tab choose **WS** (WebSockets) 
- **Navigate to the page you want to inspect the WebSocket communication on or reload the page you are on**
- Outgoing messages are marked with an arrow pointing upwards, whereas incoming messages are marked with an arrow pointing downwards



<img src="../assets/stream_out.png"><br>
Outgoing message from front end to back end. Request to list all patients.

<img src="../assets/stream_in.png">
Incoming message from back end to front end. Response with a list of all patients. It is possible to unfold single parts of the response such as single patients and retrieve more information. 

Please also refer to the [back end section](04_backend_local.md) on WebSockets, because it covers some general information.