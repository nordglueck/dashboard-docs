# Front end

This page shall provide more in-depth information on the structure of the front end and it's most important files.


## Structure

The main directory of the front end is the **vue_frontend** folder. It's structure presents as follows on the first level:

```
.
├── .env
├── .browserslistrc
├── .eslintrc.js
├── .gitignore
├── README.md
├── babel.config.js
├── node_modules
├── package-lock.json
├── package.json
├── src
├── vue.config.js
└── webpack-stats.json

```

!!! info "Important files in the root directory"

    - **.env** : Environment variables for the front end
    - **README.md** : Quickstart with commands for development
    - **node_modules** : Auto-generated folder by running ``npm install`` that inherits all dependencies
    - **package.json** : Metadata and dependencies
    - **src** : Source code of the project
    - **vue.config.js** : Webpack configuration

### Source Code

As mentioned in the previous section, the source code of the front end is to be found in the **src** directory. 
It is a Vue App consisting of multiple **.vue** files that are divided into components or more complex layouts. 
For the state-management of the app, a _store_ is set up. Everything related to the state-management is to be found inside
the **store** directory.

```
.
├── App.vue
├── dashboard
│   ├── assets
│   ├── components
│   ├── directives
│   ├── entry
│   │   ├── main.js
│   │   ├── registerServiceWorker.js
│   │   └── router.js
│   ├── layout
│   ├── plugins
│   └── views
└── store
    ├── modules
    └── vuex_usage_utils.js

```

!!! info "Getting started with the front end"

    - **main.js** : Entrypoint for the app. Connects the store, the router, the App and everything that is needed.
    - **router.js** : Defines the routes for the app and connects components/layouts and names to them.
    - **App.vue** : The main structure of the app that is rendered at first.
    - **vuex_usage_utils.js** : The store/state-management configurations.

