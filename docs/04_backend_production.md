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