In this tutorial we will handle data that is provided by the back end via WebSockets.  
We are going to use the endpoint created in the respective [back end tutorial](00_tut_ws.md)

## Prerequisites

- A general understanding of how vuex works. States, actions and mutations should be familiar.
- A working WebSocket stream to import data from and send data to.
- A set-up store with submodules like described [here](05_frontend.md#the-store).

## Establish a connection to the WebSocket

At first it is necessary to establish a connection to the WebSocket. In contrast to HTTP REST communication this connection remains
established until one of the communication partners closes it. Therefore each side can send data via the WebSocket at any time. 

To establish the connection, we use a package called ``dcrf-client``, which is the client-side implementation of the Django Channels Rest Framework, which
is used in the back end implementation to provide the WebSocket itself. The ``connect`` method takes one parameter of the address of the WebSocket.
In our case it will be a WebSocket on localhost and therefore ``"ws://localhost:8000/ws/"``. The information about the socket and the established connection is then saved
to a variable called ``client``. As this information is important, because the connection remains open and therefore important, we save it to the global
state via a _commit_, which triggers a mutation, that does exactly that.

Some additional sugar, to have easily accessible information about whether the system is connected to the WebSocket or not is implemented in the following lines.
Every WebSocket has EventListeners like ``onopen``. If the WebSocket is open, i.e. the system is connected, a mutation is triggered and sets a respective variable to true.

```js

import dcrf from "dcrf-client";

...

const state = {
    connected: false,
    error: "",
    client: null,

    ...
};

...

setup(context) {
        if (!state.is_online) {
            var client = dcrf.connect("ws://localhost:8000/ws/");
            context.commit("SET_CLIENT", client);
            state.client.transport.socket.onopen = function () {
                context.commit("CONNECTED", true);
            };
        }
},

```

## Create a patient module

In ``src/store/modules/patients/patients.js`` there should be the following structure. If the folder and file doesn't exist, feel
free to generate them. 

```js

const state = {

};

const mutations = {

};

const actions = {

};

const patientModule = {
    state,
    mutations,
    actions,
    getters,
};

export default patientModule;


```

To register the module to the global vuex state, we have to import it in ``src/store/vuex_usage_utils.js`` like in the following snippet.

```js

...

import patients from "./modules/patients/patient.js";

...

let store = new Vuex.Store({
    modules: {
        auth,
        patients,
    },
    // persist the state, excluding the socket (important!)
    plugins: [createPersistedState({
        paths: ['auth','patients'],
        key: 'vuex',
        reducer: function (state) {
            //clear the state that is persisted in the local storage when the user is logged out
            if (state.auth.logged_in === false) {
                return {}
            }
            return {patients: state.patients}
        },
    })],

});

export default store;


```

## List all available patients

Back in ``src/store/modules/patients/patients.js`` we can now define actions to handle our data. In this example we want to list
all available patients. An action to do so might be called _loadPatients_. 

First, we get hold of the client object we created in the first step. As this object is not part of the state of this file, we have
to access it by using the rootState like in the snippet below. On the ``client`` (open socket) we can now use methods provided by the ``dcrf-client``.
To list all patients we use the _list_ function and pass the stream of which we want to list the objects off as an argument. 
The response of this is handled directly and commited to the state. Error-handling is also important here and should lead to another commit, like
shown below.

```js

    loadPatients(context) {
        let client = context.rootState.socket.client;
        client.list("patients").then((response) => {
            context.commit("UPDATE_PATIENT_DATA", response);
        }).catch((e) => {
            context.commit('NEW_NOTIFICATION', e.errors, {root: true});
        });
    },

```

## Update patient data

The data retrieved in the previous step leads to a commit to ``UPDATE_PATIENT_DATA``, which itself is a mutation. Mutations are able
changing the state and this principle should be taken care of to provide nice and clean state-management. In our case the response of our
``list`` request is being passed to the ``UPDATE_PATIENT_DATA`` mutation. Inside the mutation, the patientData object of the state is
simply completely replaced with the new input.

```js

const state = {
    patientData: [],
};

const mutations = {
    UPDATE_PATIENT_DATA(state, payload) {
        state.patientData = payload;
    },
};

```


## Make the patient data accessible

In order to access the data from within components in Vue, we have to provide getters for our state variables. In our case we can just
name the getter as the variable and map the variable to it. But it is also possible to write more complex getter functions that provide filters, for example to filter patients by name or ID.
An example for a filter by ID is shown in the lines below.

```js

const getters = {
    patientData: (state) => state.patientData,
    
    getPatientById: (state) => (id) =>
        state.patientData.find((patient) => patient.id === id),
};


```


## Final result

```js


const state = {
    patientData: [],
};

const mutations = {
    UPDATE_PATIENT_DATA(state, payload) {
        state.patientData = payload;
    },
};

const actions = {
    // loads all available patient data
    loadPatients(context) {
        let client = context.rootState.socket.client;
        client.list("patients").then((response) => {
            context.commit("UPDATE_PATIENT_DATA", response);
        }).catch((e) => {
            context.commit('NEW_NOTIFICATION', e.errors, {root: true});
        });
    },

};

const getters = {
    patientData: (state) => state.patientData,
    getPatientById: (state) => (id) =>
        state.patientData.find((patient) => patient.id === id),
};

const patientModule = {
    state,
    mutations,
    actions,
    getters,
};

export default patientModule;


```