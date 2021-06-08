# New WebSocket Endpoint

In this tutorial we create a new websocket endpoint.

## Model

First we have to create a model. In this example a simple patient model.

```python
from django.db import models

class Patient(models.Model):
    """
    Patient instance.
    """
    first_name = models.CharField(max_length=240)
    last_name = models.CharField(max_length=240)
    admission_date = models.DateTimeField()
    dismissal_date = models.DateTimeField(blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
```
**file:** ``dashboard/patients/models.py``


## Serializer
The second step is to serialize the model. To do so, we import the serializer from the [Django Rest Framework](https://www.django-rest-framework.org/)
and create a new Serializer Class, that inherits from the ModelSerializer. The base model for this serializer is the just created patient model.
In the ``fields`` argument we may list all the fields we want to serialize. It is also possible to define ``__all__`` or exclude certain fields.


```python

from rest_framework import serializers
from dashboard.patients.models import Patient

class PatientSerializer(serializers.ModelSerializer):
    class Meta:
        model = Patient
        fields = ["id", "first_name", "last_name", "admission_date",
                  "dismissal_date", "updated_at", "created_at"]

```

**file:** ``dashboard/patients/api/serializers.py``

## Consumer
To be able to make the serialized data available to connected clients, a consumer needs to be set up. Clients that are connected
to the WebSocket are called _consumers_.
A fairly minimalistic setup looks something like this. Notice that a couple of ``Mixins`` are imported from the [Django Channels Rest Framework](https://github.com/hishnash/djangochannelsrestframework), which provide the basic functionality.
The serializer is the one we just created and the queryset is the one from the model above. To allow only authenticated users to connect, 
the ``permission_classes`` are set to ``ìsAuthenticated``.


````python

from djangochannelsrestframework import permissions
from djangochannelsrestframework.generics import GenericAsyncAPIConsumer
from djangochannelsrestframework.mixins import (
    ListModelMixin,
    RetrieveModelMixin,
    UpdateModelMixin,
    PatchModelMixin,
    DeleteModelMixin,
    CreateModelMixin,
)

from dashboard.patients.api.serializers import PatientSerializer
from dashboard.patients.models import Patient


class PatientConsumer(ListModelMixin, RetrieveModelMixin, PatchModelMixin, UpdateModelMixin,
                      CreateModelMixin,
                      DeleteModelMixin, GenericAsyncAPIConsumer):
    queryset = Patient.objects.all()
    serializer_class = PatientSerializer
    permission_classes = (permissions.IsAuthenticated,)

````

**file:** ``dashboard/patients/consumers.py``

!!! info

    The Mixins that the consumer inherits from, are the actions that the WebSocket will provide. In the listing above you 
    can e.g. see a ``ListModelMixin`` which will provide the list action for the consumer.


## URLs
Finally, we have to define a route for the WebSocket, just like with the REST API. The routes for the WebSockets are called _streams_ and are defined in ``asgi.py``. 
In this file you will find the ``ProtocolTypeRouter``, that routes HTTP and WebSocket requests accordingly. Here, the starting point for the WebSocket is defined as ``/ws``, 
whereas we defined the starting point for REST API endpoints as ``/api`` (not here). The stream we define here will be the string that follows the ``/ws/``. 
So in this case, our new route, that is connected to the PatientConsumer that we created in the previous step will be called _patients_. Notice, that within this definition,
the _patients_ is not declared with quotation marks. However, the resulting route/URL is ``www.example.com/ws/patients/``.
But with an important change to the REST API endpoints, because instead of:

**http://**``www.example.com/api/patients/`` or **https://**``www.example.com/api/patients/``

we now have a change in protocols and must use:

**ws://**``ww.example.com/ws/patients/`` or **wss://**``ww.example.com/ws/patients/``


```python

from channels.routing import ProtocolTypeRouter, URLRouter
from django.core.asgi import get_asgi_application
from django.urls import re_path

from dashboard.patients.consumers import PatientConsumer
from channelsmultiplexer import AsyncJsonWebsocketDemultiplexer
from config.middleware import TokenAuthMiddlewareStack


application = ProtocolTypeRouter({
    "http": get_asgi_application(),
    "websocket": TokenAuthMiddlewareStack(
        URLRouter(
            [re_path(r"^ws/$", AsyncJsonWebsocketDemultiplexer(
                patients=PatientConsumer().as_asgi(),
            ).as_asgi()), ]
        )
    ),
})

```

**file:** ``config/asgi.py``