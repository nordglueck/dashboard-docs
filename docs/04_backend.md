# Back end

This page shall provide more in-depth information on the structure of the back end and it's most important files.

## Structure

The back end is structured in a way, that distinguishes between a local development environment and a production environment.
Therefore some files such as the Dockerfile (see [**Installation**](/dashboard-docs/02_Installation)) are available twice. Depending on the environment, the respective files should either be used or are used automatically.
Files marked with the word **base** such as ``config/settings/base.py`` - as the name suggests - serve as a base for both,
the local and the production environment. 

### Local

...

### Production

The most important difference between the local and the production environment are the **environment variables**.
Not only, but mostly sensitive information is stored in environment variables and will not be exported from a local environment
to a production environment. Therefore these environment variables have to be set in the production environment.
It is suggested not to hardcode values for such variables into the code for production, but to really set and use environment variables.

...

