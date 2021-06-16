# Create a new report via WebSocket

In this tutorial we are going to create a report using WebSockets.


## Prerequisites

- Established WebSocket connection
- State-management is set-up


## Retrieve a list of reports

To interact with the data the WebSocket endpoints provide, the dcrf-client is used. It provides methods to e.g. delete a report. All we have to do is to connect to the WebSocket and pass the
endpoint, in this case _reports_, together with a JSON Object that contains the data for the report as parameters to the ``delete`` method. For an overview of available methods refer to the repository or the source code directly: [https://github.com/theY4Kman/dcrf-client](https://github.com/theY4Kman/dcrf-client) 

In the ``actions`` of a store module of the application, we will have the following code:

```javascript

    deleteReport(context, payload) {
        let client = context.rootState.socket.client;

        client.delete("history", payload.id).then(() => {
        }).catch((e) => {
            context.commit('NEW_NOTIFICATION', e.errors, {root: true});
        });
        
    },

```

