# Frequently Asked Questions


## How to approach the project?

The general structure of the project is divided into two parts: back end and front end. The back end is made with [Django, a web framework based on python](https://www.djangoproject.com/).
The front end is made with Vue.js. Vue.js consists of JavaScript, HTML and CSS. Both, Django and Vue.js are fairly easy to learn.

#### Back end / Django 

First of all, the **Django project** itself is providing useful resources to get started with Django: [Django Project](https://www.djangoproject.com/start/) 

For this project, for django a good start would also be the documentation of the **Django REST Framework**, as the back end
provides an API for different applications. See [Django REST Framework](https://www.django-rest-framework.org/)

The Dengue Dashboard in particular is based on being a real-time web-application and therefore uses a full-duplex communication
between the server and the client. That means that both, client and server, may always send each other messages after an initial
connection is established. That couldn't be provided with normal HTTP REST communication as previous mentioned.

For this purpose, the WebSocket protocol was implemented into the project, which made it necessary to implement **Django Channels**,
that enables channeling the different protocols (HTTP/WebSockets). 

An **incredibly useful article**, to understand the structure of this project and the overview of handling different protocols in a
real-time environment is to be found here: [https://blog.heroku.com/in_deep_with_django_channels_the_future_of_real_time_apps_in_django](https://blog.heroku.com/in_deep_with_django_channels_the_future_of_real_time_apps_in_django).
It is written by one of the core developers of Django and not only helps to understand the structure of this project, but also visualizes
the concepts of Django Channels.

To serve the API via **WebSockets**, the [Django Channels REST Framework](https://github.com/hishnash/djangochannelsrestframework) was used.


In general, it is possible and common to serve ``.html`` files from the Django Templates folder. You can write html and specific Django syntax to render pages
that will be served to the client. For this project however, Vue.js is used to create the files for the front end and display information to the client. The reason for this
is, that Vue.js is a **reactive** JavaScript framework. It enables automatic updating of the page/DOM in case of updates to the data that is being displayed.
Furthermore, with a JavaScript framework like this, it is possible to separate the data from it's representation.

The front end is solely developed in the ``vue_frontend`` directory, whilst all of the other folders are connected to the back end. 

Besides Django, the back end also includes other frameworks/technologies that are e.g. used for deployment.

To fully understand the files of the back end, one could look at the following technologies, that are used:

* Python
* Django (as a web framework based on python)
* Docker/Dockerfiles
* Shell Scripts
* Markdown (for Documentation purposes mostly)
* pip (package manager to install python packages)
* JSON
* Knowledge of the terminal



#### Front end / Vue.js

The front end of the application is developed with Vue.js. The main reason besides the separation of content and representation is the reactivity.
Through state-management it is possible, that the DOM automatically refreshes whenever changes to the represented data is made. This enhances the
real-time feature of the web-application. Vue has got several other advantages such as that it is light-weighted and incrementally adoptable, thus scalable.

A good starting point for Vue.js is the project website itself. Vue.js is open-source and well-documented. [https://vuejs.org/v2/guide/](https://vuejs.org/v2/guide/)

To connect with the aforementioned WebSocket provided by the Django Channels REST Framework, a [client side implementation](ttps://github.com/theY4Kman/dcrf-client) is used.

The maybe most important part in the front end implementation is the state-management. Vuex is a state-management pattern and library for Vue.js. 
The documentation for vuex delivers a good explanation of what vuex is and how it works. [https://vuex.vuejs.org/](https://vuex.vuejs.org/)
The following diagram gives a brief overview over the vuex state-management pattern from the aforementioned website.

![Overview of the vuex state-management pattern from https://vuex.vuejs.org/vuex.png](https://vuex.vuejs.org/vuex.png)

To fully understand the files of the front end, one could look at the following technologies:

* JavaScript
* HTML
* CSS
* Bootstrap (as a CSS framework that is used in the front end template)
* npm (package manager to install javascript packages)
* Vue.js 
* Vuex (state-management)
* Single Page Applications
* WebPack (Bundling files into static assets)
* JSON
* Developer Tools of your Browser of Choice (Chrome or Firefox are recommended)

---

## Which IDE is recommended?

_Front end_  
I would recommend **PyCharm Professional** together with the Vue.js PlugIn. It is a powerful IDE for Python development but with support for Vue.js
and comes with rich features regarding project navigation, highlighting, code completion, TODO management, integrated terminal or python console etc.

It is developed by JetBrains and free of charge for students.

Great and useful features for a project this size, are:

* Structure view: ``Cmd+7`` (Mac) / ``Alt+7`` (Win)
* Find file by name: ``Shift+Cmd+O`` (Mac) / ``Ctrl+F12`` (Win)
* Find in files: ``Shift+Cmd+F`` (Mac) / ``Ctrl+Shift+F`` (Win)

All Shortcuts for Win/Linux: [https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard.pdf](https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard.pdf)
All Shortcuts for MacOS: [https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard_mac.pdf](https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard_mac.pdf)

As an Alternative to PyCharm I would recommend **Virtual Studio Code** with Plugins for Vue.js.

_Back end_  

I would recommend **PyCharm Professional**. It is a powerful IDE for Python development but with support for Vue.js
and comes with rich features regarding project navigation, highlighting, code completion, TODO management, integrated terminal or python console etc.

It is developed by JetBrains and free of charge for students.

Great and useful features for a project this size, are:

* Structure view: ``Cmd+7`` (Mac) / ``Alt+7`` (Win)
* Find file by name: ``Shift+Cmd+O`` (Mac) / ``Ctrl+F12`` (Win)
* Find in files: ``Shift+Cmd+F`` (Mac) / ``Ctrl+Shift+F`` (Win)

All Shortcuts for Win/Linux: [https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard.pdf](https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard.pdf)
All Shortcuts for MacOS: [https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard_mac.pdf](https://resources.jetbrains.com/storage/products/pycharm/docs/PyCharm_ReferenceCard_mac.pdf)

As an alternative, **Virtual Studio Code** will work, but needs Plugins to feel like an IDE.

--- 

### Which programs are recommended?

_Front end_

- **Operating Systems:**
    - macOs, Linux, Windows (mind the problems)
- **IDEs**:
    - PyCharm Professional, Visual Studio Code
- **Browser**:
    - Brave, Chrome, Firefox (Chromium-based Browsers with Vue.js Plugin)
- **Misc:**
    - Docker, npm
    

_Back end_

- **Operating Systems:**
    - macOs, Linux, Windows (mind the problems)
- **IDEs**:
    - PyCharm Professional, Visual Studio Code
- **Programs:**
    - DBeaver
- **Browser**:
    - Brave, Chrome, Firefox (Chromium-based Browsers with Vue.js Plugin)
- **Misc:**
    - Docker

---

## What are the programming languages/technologies that are used?

_Front end_

- HTML, CSS, JS
- Vue.js
- Bootstrap
- JSON


_Back end_

- Python
- Django
- PostgreSQL
- Shell
- Docker
- JSON

## localhost:8000 is not showing the app.

You started Docker but localhost:8000 is not showing the App? There is a couple of things that could be wrong here. 


* **Front end is not up and running**

First of all, make sure, that the front end is being served. You can achieve
this by running

    npm install

once and then

    npm run serve

inside the ``vue_frontend`` directory of the project. ``npm run serve`` will serve the front end and enable hot reloading, which
means that all changes made to the code will automatically refresh the page in the browser after saving the file.

* **Cache is _broken_**

The app is made to make as little requests as necessary. That means, if some JavaScript or CSS file that is needed for the
page was already loaded into the cache once, the page will most likely not request the same file again unless the file is marked as modified.
This is one reason, why the webpack configuration, that bundles the front end ``.vue`` files to static ``.js`` and ``.css`` files
generates a unique hash that is appended to every file. The files will be renewed in the browser after every build process.

In local development however, the development cycle might lead to a broken cache, i.e. a cache, where files are mistaken to be
the newest when they aren't. The easiest way to verify if that is the problem you are encountering is to delete the cached files
or to see if the problem persists in a private window. 

Personal experience showed, that these caching problems in local development rarely occur, when building the project with ``npm run build`` after a developing session.

* **Serving in the wrong location**

The standard port of local development for Vue.js is ``:8080`` whereas the Docker will serve on port ``:8000``.
Both will work, but ``localhost:8000`` is preferable and used throughout the application.

Depending on your system/machine it is possible, that ``localhost`` or ``0.0.0.0`` or ``127.0.0.1`` is not the IP that your Docker instance is serving the app on.
Another possibility is, that the ports are not available to your host system or blocked by the firewall. Vue.js will usually automatically turn to another port then
but in cases might not. 

So for debugging, you might follow these steps:

* [https://stackoverflow.com/questions/46176584/docker-bind-for-0-0-0-04000-failed-port-is-already-allocated](https://stackoverflow.com/questions/46176584/docker-bind-for-0-0-0-04000-failed-port-is-already-allocated)
* Check your firewall settings for the ports
* Check the IP/Port of your docker process(es)

When you encounter another IP than any of the localhost IPs, it is important to whitelist them in the django app (``ALLOWED_HOSTS``) and also to **exchange all strings containing the localhost URL to your new IP.**

The ``ALLOWED_HOSTS`` can e.g. be altered in ```config/settings/local.py```. More information on ALLOWED_HOSTS: [https://docs.djangoproject.com/en/dev/ref/settings/#allowed-hosts](https://docs.djangoproject.com/en/dev/ref/settings/#allowed-hosts)

---

## I've got problems with Docker on Windows...

Windows is the least recommended Operation System. It seems to be well known, that there are problems when Hyper-V and VirtualBox coexist in a Windows installation.
This could lead to problems if you e.g. use something like VirtualBox on your Windows machine and want to install/use Docker (using Hyper-V) as well. 

Further information on this: 
[https://www.mt-ag.com/blog/ki-werkstatt/koexistenz-von-hyper-v-und-virtualbox-fur-den-einsatz-von-docker/](https://www.mt-ag.com/blog/ki-werkstatt/koexistenz-von-hyper-v-und-virtualbox-fur-den-einsatz-von-docker/)


---

