# Installation

This page serves as an installation guide for local development of the **Dengue Dashboard**. The guide assumes, that the reader
already cloned a recent repository of the project and navigated to the project root. The shown commands are executed from the command line in the root
directory if not declared otherwise.

## 1. Back end: Django

#### Getting Up and Running Locally With Docker

!!! info

    The project is not required to run in a docker container. All of the processes involved could also be started manually. However, for simplicity and cross-platform development purposes, a docker environment is provided.

The steps below will get you up and running with a local development environment.
All of these commands assume you are in the root of your generated project.

See also: [https://github.com/pydanny/cookiecutter-django/](https://github.com/pydanny/cookiecutter-django/)


#### Prerequisites

* Docker; if you don't have it yet, follow the [installation instructions](https://docs.docker.com/install/#supported-platforms);
* Docker Compose; refer to the official documentation for the [installation guide](https://docs.docker.com/compose/install/).

---

#### Build the Stack

This can take a while, especially the first time you run this particular command on your development system:

```console
docker-compose -f local.yml build
```
    

Generally, if you want to emulate production environment use ``production.yml`` instead. And this is true for any other actions you might need to perform: whenever a switch is required, just do it!

---


#### Run the Stack

This brings up both Django and PostgreSQL. The first time it is run it might take a while to get started, but subsequent runs will occur quickly.

Open a terminal at the project root and run the following for local development:

```console
docker-compose -f local.yml up
```

You can also set the environment variable ``COMPOSE_FILE`` pointing to ``local.yml`` like this:

```console
export COMPOSE_FILE=local.yml
```

And then run:

```console
docker-compose up
```

To run in a detached (background) mode, just::

```console
docker-compose up -d
```

??? info "(Optionally) Designate your Docker Development Server IP"

    When ``DEBUG`` is set to ``True``, the host is validated against ``['localhost', '127.0.0.1', '[::1]']``. This is adequate when running a ``virtualenv``. For Docker, in the ``config.settings.local``, add your host development server IP to ``INTERNAL_IPS`` or ``ALLOWED_HOSTS`` if the variable exists.

---

??? info "Alternative: Virtual Environment for Python"

    **Prerequisites**: 
    - Installation of:
      - Python 3 
      - pip
      - nodejs 
      - npm/yarn
      - redis
      - postgres 
      - a Unix/MacOS or Windows Machine
    
    As an alternative to Docker, the project can be developed in a **virtual environment for python**.
    To create a virtual environment, decide on a name, e.g. `env_name` and create on like so in a folder above or aside the project folder:
    
    ```console    
    python3 -m venv env_name
    ```
    
    To activate the virtual environment on a level above the environment folder that was just created:
    
    === "Mac OS / Linux"
    
        ```console
        source env_name/bin/activate
        ```
    
    === "Windows"
    
        ``` console
        env_name\Scripts\activate.bat
        ```
    
    ### Back end
    
    With the virtual environment at hand (and activated), the requirements for the projects can now be installed manually only to this environment. To do so, 
    you need to go to the root directory of the project and execute the following command:
    
    ```console
    pip install requirements/local.txt
    ```

    After the installation is complete, the following command will start the server:

    ```console
    python manage.py runserver
    ```

    The following commands are the same as in docker but without the docker specific prefix:

    ```console
    python manage.py makemigrations
    python manage.py migrate
    python manage.py createsuperuser
    ```

    ### Front End
    
    Change to the **vue_frontend** directory. To initialize the frontend, from the ``vue_frontend`` directory, run:

        npm install

    To serve the Vue frontend in hot-reloading development mode **together with the back end**:

        npm run serve

    And to build for deployment:

        npm run build


    ### Additional Configurations

    When starting the server you may be prompted to provide right credentials for the database or redis.
    To find out, how to cofigure each of them for your OS, please refer to the specific documentations and provide
    the right credentials.

    **NOTE:** This approach is common when building django projects, however it is not tested for this specific project.
    Due to the scope of the project, it is highly reccomended to use the docker environment.

    For more information on virtual environments, please refer to the Python 3 tutorial: [https://docs.python.org/3/tutorial/venv.html](https://docs.python.org/3/tutorial/venv.html)


    
    



---

## 2. Front end: Vue.js


This app integrates with a Vue single page app (SPA) located in ``vue_frontend``.

To initialize the frontend, from the ``vue_frontend`` directory, run:

    npm install

To serve the Vue frontend in hot-reloading development mode **together with the back end**:

    npm run serve

And to build for deployment:

    npm run build


---

## Commands

### Execute Management Commands

As with any shell command that we wish to run in our container, this is done using the ``docker-compose -f local.yml run --rm`` command:

    docker-compose -f local.yml run --rm django python manage.py migrate
    docker-compose -f local.yml run --rm django python manage.py createsuperuser

Here, ``django`` is the target service we are executing the commands against. The ``run`` command is starting a new container that is
being deleted after run due to the ``--rm`` flag.

To achieve the same but in an already running container, you can use commands like:

    docker-compose -f local.yml exec django python manage.py migrate
    docker-compose -f local.yml exec --rm django python manage.py createsuperuser

``exec`` will use the existing container and run the given command in it.


More on Docker and local development can be found in ```LOCAL_DEV.rst```.
