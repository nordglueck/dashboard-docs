Once the system should be run in production, the source files have to be bundled. The command to do so is:

```console 
npm run build
```

It might take a while to build the files, but eventually they will be placed in the ``dashboard/static/vue`` folder in the back end
where these static files can then be served and interpreted from browsers, as they now contain only HTML, CSS and JS.

Configurations for this process can be made in the ```vue.config.js``` file at the root of the ``vue_frontend`` folder.
It is necessary to keep the static files in VCS for production.

