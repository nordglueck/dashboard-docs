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

After the docker container is up and running, additional commands (like ``makemigrations`` e.g.), inside the container can be execuded using the ``exec``
command:

```console

docker-compose -f local.yml exec django python manage.py makemigrations

```


!!! attention "More content coming soon"

    - test websockets