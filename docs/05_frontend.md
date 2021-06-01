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

???+ info "Important files in the root directory"

    - **.env** : Environment variables for the front end
    - **README.md** : Quickstart with commands for development
    - **node_modules** : Auto-generated folder by running ``npm install`` that inherits all dependencies
    - **package.json** : Metadata and dependencies
    - **src** : Source code of the project
    - **vue.config.js** : Webpack configuration