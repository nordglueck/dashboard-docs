In order to manage and especially store the data, we use a postgres database in our system. Postgres integrates well with Django and
Django provides special features that can be used best with postgres which then again provides great extensibility for the future.

However, postgres has some particular commands, one needs to know in order to interact with the databases.

An overview over the most common and useful commands as well as explanations can be found at:
[https://tomcam.github.io/postgres/](https://tomcam.github.io/postgres/)

As an alternative to the interaction via the command line, it is possible to use a programm such as DBeaver to manage
the database(s).

DBeaver is free of charge and can be used with macOS, Linux and Windows:

[https://dbeaver.io/](https://dbeaver.io/)

The credentials to connect to your database from inside DBeaver can be found (or set) in the _postgres environment variables_ in the project folder. 