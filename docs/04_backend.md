# Back end

This page shall provide more in-depth information on the structure of the back end and it's most important files.

## Structure

The back end is structured in a way, that distinguishes between a local development environment and a production environment.
Therefore some files such as the Dockerfile (see [**Installation**](/dashboard-docs/02_Installation)) are available twice. Depending on the environment, the respective files should either be used or are used automatically.
Files marked with the word **base** such as ``config/settings/base.py`` - as the name suggests - serve as a base for both,
the local and the production environment. 

```console
.
├── .envs
├── compose
│   ├── local
│   └── production
├── config
│   └── settings
├── dashboard
│   ├── contrib
│   ├── patients
│   ├── static
│   ├── templates
│   ├── users
│   ├── utils
│   └── webpack_bundle
├── docs
│   ├── _build
│   └── _source
├── locale
├── requirements

```



??? info "env files"
    
    Environment files are mainly used to store sensitive data such as passwords or secret keys that may cause vulnerabilities if exposed in the code.
    In local environments some things may be hardcoded, when they are depending on environment variables in production. This is an intended behaviour and should not be changed.
    See the ``config`` section and information about the settings. Most of the settings that require environment variables are defined there.

    ```console

        .envs
        ├── .local
        │   ├── .django
        │   └── .postgres
        └── .production
            ├── .django
            └── .postgres
    ```


??? info "compose"

    Except for the ``.yml`` files, all of the docker configuration is to be found in this directory. As usual, the configurations are separated by environments.

    ```console

    .
    ├── local
    │   ├── django
    │   │   ├── Dockerfile
    │   │   └── start
    │   └── docs
    │       └── Dockerfile
    └── production
        ├── django
        │   ├── Dockerfile
        │   ├── entrypoint
        │   └── start
        ├── postgres
        │   ├── Dockerfile
        │   └── maintenance
        │       ├── _sourced
        │       ├── backup
        │       ├── backups
        │       └── restore
        └── traefik
            ├── Dockerfile
            └── traefik.yml

    ```

???+ info "config"

    The main settings of the software are to be found in the config folder. Whats normally the ``settings.py`` file, lives in the ``settings`` folder and is separated by environment.
    Because there are settings, that local and production environments have in common, there is also a ``base.py``, that serves as the base. In a local environment, the settings of both the ``base.py`` and the ``local.py`` will be considered.


    ```console

    ├── __init__.py
    ├── api_router.py
    ├── asgi.py
    ├── middleware.py
    ├── settings
    │   ├── __init__.py
    │   ├── base.py
    │   ├── local.py
    │   ├── production.py
    │   └── test.py
    ├── urls.py
    └── wsgi.py

    ```

??? info "dashboard"

    ```console
    .
    ├── contrib
    │   └── sites
    │       └── migrations
    ├── patients
    │   ├── api
    │   └── migrations
    ├── static
    │   ├── css
    │   ├── fonts
    │   ├── images
    │   │   └── favicons
    │   ├── js
    │   ├── sass
    │   └── vue
    │       ├── css
    │       ├── fonts
    │       ├── img
    │       └── js
    ├── templates
    │   ├── account
    │   ├── pages
    │   ├── users
    │   └── webpack_bundle
    ├── users
    │   ├── api
    │   ├── migrations
    │   └── tests
    ├── utils
    └── webpack_bundle
        └── templatetags

    ```

??? info "requirements"

    The requirements follow the logic that was presented in the settings. ``base.txt`` is serving as a base for both local and production environments. Depending on the environment, the respective requirements will be installed additionally.
    The ``base.txt`` should only include what's needed in both environments. 

    ```console
    .
    ├── base.txt
    ├── local.txt
    └── production.txt

    ```

### Local


...

### Production

The most important difference between the local and the production environment are the **environment variables**.
Not only, but mostly sensitive information is stored in environment variables and will not be exported from a local environment
to a production environment. Therefore these environment variables have to be set in the production environment.
It is suggested not to hardcode values for such variables into the code for production, but to really set and use environment variables.

#### Configuring the environment

!!! info "environment variables"

    The environment files can be found in the ``.envs`` directory like shown before.
    The most important thing for us here now is ``env_file`` section enlisting ``./.envs/.local/.postgres``. Generally, the stack's behavior is governed by a number of environment variables (`env(s)`, for short) residing in ``envs/``.
    
    ```console
    # PostgreSQL
    # ------------------------------------------------------------------------------
    POSTGRES_HOST=postgres
    POSTGRES_DB=<your project slug>
    POSTGRES_USER=<your postgres user>
    POSTGRES_PASSWORD=<your password>
    ```

...