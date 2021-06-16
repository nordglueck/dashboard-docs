# Create a new report via WebSocket

In this tutorial we are going to create a report using WebSockets.


## Prerequisites

- Established WebSocket connection
- State-management is set-up


## Retrieve a list of reports

To interact with the data the WebSocket endpoints provide, the dcrf-client is used. It provides methods to e.g. patch a report. All we have to do is to connect to the WebSocket and pass the
endpoint, in this case _reports_, together with a JSON Object that contains the data for the report as parameters to the ``patch`` method. In addition to that, a primary key is needed to identify the right report. For an overview of available methods refer to the repository or the source code directly: [https://github.com/theY4Kman/dcrf-client](https://github.com/theY4Kman/dcrf-client) 

In the ``actions`` of a store module of the application, we will have the following code:


```javascript

    updateReport(context, payload) {

        let client = context.rootState.socket.client;

        context.dispatch('formatJson', payload).then((jsonObj) => {

            client.patch("reports", payload.id, jsonObj).then((report) => {
                context.commit("UPDATE_REPORT_DATA", [report]);
            }).catch((e) => {
                context.commit('NEW_NOTIFICATION', e.errors, {root: true});
            })
            ;
        });
    },

```

``client`` is a variable containing the established WebSocket connection. The patch method returns a response
or an error, which may be handled as needed. In this case, the response triggers a mutation that alters the state
containing the current report data. In case of an error, the error triggers a mutation that updates the global notifications.

!!! info

    The ``context.dispatch('formatJson', payload)`` part in the listing above will call a function that formats the parameter called ``payload``
    that is given to the ``createReport`` function into a JSON Object. It then returns this Object. The response is then passed into the
    next function that is ``client.patch("reports", payload.id, jsonObj)``. 

    You may also just pass a JSON Object as a payload and leave the ``formatJson`` out. 