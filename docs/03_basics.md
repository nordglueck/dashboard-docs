# Basics

## Django

### Model-View-Template (MVT)

Django is following the Model-View-Template structure, where the Model is for structuring and manipulating the data of the application, the view implements
the business logic and the templates serves the views to the clients. In this project, the templates are rendering the static files
provided by the webpack bundling, that are moved into the ``static`` folder after executing ``npm run build`` inside the ``vue_frontend`` directory.

#### Model

The model of the application is to be found in the respective ``models.py`` file. See [https://docs.djangoproject.com/en/3.2/topics/db/models](https://docs.djangoproject.com/en/3.2/topics/db/models) for documentation on how to create Models and available Fields.
All of the data of the model instances are saved to a **PostgreSQL** Database. Postgres integrates well with Django and Django even supports some fields exclusively for Postgres. See [https://docs.djangoproject.com/en/3.2/ref/contrib/postgres/](https://docs.djangoproject.com/en/3.2/ref/contrib/postgres/)

#### View

The view implements the business logic of the application. In the ``patients/views.py``, the REST API endpoints are defined. The most important endpoints that are exposed
as of the end of the thesis are:

| Endpoint           | Actions (REST)                 | Description                      |
|--------------------|-------------------------|----------------------------------|
| ``/api/patients/``     | GET, POST               | List view of all patients        |
| ``/api/patients/id/``  | GET, PUT, PATCH, DELETE | Detail view of a single patient  |
| ``/api/reports/``      | GET, POST               | List view of all reports         |
| ``/api/reports/id/``   | GET, PUT, PATCH, DELETE | Detail view of a single report   |
| ``/rest-auth/login/``  | POST                    | Login with username and password |
| ``/rest-auth/logout/`` | POST                    | Logout and delete token          |
| ``/rest-auth/user/``   | GET                     | Retrieve user information        |


A full documentation of all available endpoints as well as an **interactive demo** of the endpoints can be obtained from the 
endpoint ``/swagger``. Curl commands can be interactively executed on the page and requests and responses can be analysed.

The fields, that are to be included (or excluded) in the respective JSON responses are defined in the ``patients/serializers.py`` file.

With the WebSocket integration, the endpoints for WebSocket requests are defined like so:


| Stream   | Consumer        | Model            | Actions (REST-like)                                      |
|----------|-----------------|------------------|-----------------------------------------------|
| ``patients`` | PatientConsumer | Patient          | List, Retrieve, Create, Patch, Update, Delete |
| ``reports``  | ReportConsumer  | Report           | List, Retrieve, Create, Patch, Update, Delete |
| ``history``  | HistoryConsumer | HistoricalReport | List, Retrieve, Patch, Update, Delete         |



#### Template

### Routing

### REST API

### Consumer

### Background Tasks

---

## Vue.js

### Routing

### State-management

### Components

---

## WebSockets

---

