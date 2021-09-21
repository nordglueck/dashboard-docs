This section goes more into detail on how to develop the backend locally. While the installation is covered on the installation page, this 
section also provides details on which settings one might configure for their specific environment.

#### Local development

As explained on the installation page, there are two different ``docker-compose`` files for each of the environment. For local development, the docker container is built
and started by executing the following two commands in the root directory of the project.

```console

docker-compose local.yml -f build

```

This first command builds the docker container and installs all of the necessary requirements for the back end. Because we are building the
container for the local environment here, the requirements ``base.txt`` and ``local.txt`` will be installed. 

The following command starts the docker container.

```console

docker-compose local.yml -f up

```

Together with **django** some other processes, including **redis** (cache) and **postgres** (database) will be started.

After starting the docker container, the console output would look something like the following:


<div id="termynal" data-termynal data-termynal data-ty-typeDelay="40" data-ty-lineDelay="700">
    <span data-ty="input">redis       | 1:M 19 May 2021 13:09:00.119 * Ready to accept connections</span>
    <span data-ty="input">postgres    | 2021-05-19 13:09:01.875 UTC [26] LOG:  database system was shut down at 2021-05-11 19:27:08 UTC</span>
    <span data-ty="input">postgres    | 2021-05-19 13:09:01.895 UTC [1] LOG:  database system is ready to accept connections</span>
    <span data-ty="input">django      | PostgreSQL is available</span>
    <span data-ty="input">django      | Operations to perform:</span>
    <span data-ty="input">django      |   Apply all migrations: admin, auth, authtoken, background_task, contenttypes, patients, sessions, sites, users</span>
    <span data-ty="input">django      | Running migrations:</span>
    <span data-ty="input">django      |   No migrations to apply.</span>
    <span data-ty="input">django      | INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)</span>
</div>

The last line of the output shows the URL of the application. However, to fully be able to develop locally, pay attention to
the [**Front End**](/05_frontend) page. 

After the docker container is up and running, additional commands (like ``makemigrations`` e.g.), inside the container can be executed using the ``exec``
command:

```console

docker-compose -f local.yml exec django python manage.py makemigrations

```

### Modelling

As the back end is the place for modeling the data structure of the system, it is important to know two commands, that will be
needed quite frequently. After adding new fields to a model, updating any field, adding a new model or changing about anything regarding the models
of the system, the database needs to know about the changes. The commands (in this particular order) are:

```console

python manage.py makemigrations
python manage.py migrate

```

The first command will show the changes that can be written to the database with the second command.
Every execution of the commands generates a migration file, which will be stored in a ``migrations`` folder near the models itself.
The migrations contain the history of the models and are kind of like a _git_ for models in Django. It is important to keep them and not exclude them
in VCS (git), so that other developer's histories are complete when making migrations and so that everyone is able to work on the same layout of the database.


### WebSockets

The back end is providing the WebSocket communication and can handle incoming request, send responses, accept or quit connections and so on.
Once the system is running, the terminal output will show the state of the system, which will state, if it is accepting WebSockets (already) and if
there are Consumers connected to the WebSocket. As soon as some Consumer (client at the front end) connects to the WebSocket, the terminal will output this.

Hence, debugging the states of a WebSocket communication (request, accept, close etc.) can be easily done via ``print`` statements to the console in the respective functions.
Other ways include WebSocket testing with programs like the newer versions of postman or using the devtools in a browser, which is described in [the front end section.](05_frontend_local.md).

The easiest way to fake a consumer however would be to just use the in-built console inside a browser:

1. Make sure you are on a HTTPS page (HTTP might not work for some browsers)
2. Open the devtools
3. Navigate to the Console tab
4. Establish a new WebSocket connection to your desired WebSocket like so: ``let ws = new WebSocket("ws://yourdomain.com/streamname");``

This sends a regular pure JavaScript WebSocket request to your server which should lead to an output on your terminal. 
Note, that this simple request should just get you started and might not lead to an established connection, as there may be restrictions in place.
