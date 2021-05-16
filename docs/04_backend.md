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



???+ info "env files"
    ```console

        .envs
        ├── .local
        │   ├── .django
        │   └── .postgres
        └── .production
            ├── .django
            └── .postgres
    ```


???+ info "compose"
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

???+ info "dashboard"

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

???+ info "requirements"

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

### Test

=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```


!!! note
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    ``` python
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

    Nunc eu odio eleifend, blandit leo a, volutpat sapien. Phasellus posuere in
    sem ut cursus. Nullam sit amet tincidunt ipsum, sit amet elementum turpis.
    Etiam ipsum quam, mattis in purus vitae, lacinia fermentum enim.