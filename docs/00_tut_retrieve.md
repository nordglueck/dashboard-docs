# Retrieving Report data from the back end via WebSocket

In this tutorial we are going to retrieve a list of reports from the back end using WebSocket.


## Prerequisites

- Established WebSocket connection
- State-management is set-up


## Retrieve a list of reports

To interact with the data the WebSocket endpoints provide, the dcrf-client is used. It provides methods to e.g. retrieve a list of reports. All we have to do is to connect to the WebSocket and pass the
endpoint, in this case _reports_ as a parameter to the ``list`` method. For an overview of available methods refer to the repository or the source code directly: [https://github.com/theY4Kman/dcrf-client](https://github.com/theY4Kman/dcrf-client) 

In the ``actions`` of a store module of the application, we will have the following code:

```javascript

    //load all reports
    loadReports(context) {
        let client = context.rootState.socket.client;
        client.list("reports").then((response) => {
            context.commit("UPDATE_REPORT_DATA", response);
        }).catch((e) => {
            context.commit('NEW_NOTIFICATION', e.errors, {root: true});
        })
        ;
    },

```

``client`` is a variable containing the established WebSocket connection. The list method returns a response
or an error, which may be handled as needed. In this case, the response triggers a mutation that alters the state
containing the current report data. In case of an error, the error triggers a mutation that updates the global notifications.
