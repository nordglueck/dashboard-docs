# Send messages via WebSocket to clients

In this tutorial we are going to notify each of the clients connected to the WebSocket
about changes to the endpoint that was created in the last tutorial.

## Prerequisites

Everything covered in the [last Tutorial](00_tut_ws.md).

# Observer

To be able to track changes in any instance of the ``Patient`` model, it is necessary, to implement an
_observer_ in the ``PatientConsumer`` that was created in the previous tutorial. The first change is to add the
``ObserverModelInstanceMixin`` from the [Django Channels Rest Framework](https://github.com/hishnash/djangochannelsrestframework).

```python

class PatientConsumer(ListModelMixin, RetrieveModelMixin, PatchModelMixin, UpdateModelMixin,
                      CreateModelMixin,
                      DeleteModelMixin, GenericAsyncAPIConsumer, ObserverModelInstanceMixin):
    queryset = Patient.objects.all()
    serializer_class = PatientSerializer
    permission_classes = (permissions.IsAuthenticated,)


```

In a second step we are going to add our own custom Observer for this special model class that will be called ``PatientConsumerObserver`.

```python

class PatientConsumer(ListModelMixin, RetrieveModelMixin, PatchModelMixin, UpdateModelMixin,
                      CreateModelMixin,
                      DeleteModelMixin, GenericAsyncAPIConsumer, ObserverModelInstanceMixin,PatientConsumerObserver):
    queryset = Patient.objects.all()
    serializer_class = PatientSerializer
    permission_classes = (permissions.IsAuthenticated,)


```

### PatientConsumerObserver

A minimal setup for the ``PatientConsumerObserver`` may look something like this: 

```python


class PatientConsumerObserver(AsyncAPIConsumer):

    async def accept(self, **kwargs):
        await super().accept(**kwargs)
        await self.patient_change.subscribe()

    @model_observer(Patient)
    async def patient_change(self, message, **kwargs):
        """
        Observes changes of the patient model instances.
        :param message: The request/message from the consumer
        :param kwargs: Optional keyword arguments
        :return: Information about the change event via websocket messages in json format to the consumer
        """
        await self.send_json(message)

    @patient_change.serializer
    def patient_serializer(self, instance, action, **kwargs):
        """ Serializes the patient instance to be sent in json format to the consumer.
        :param instance: The patient instance
        :param action: Create, update, patch, list, delete
        :param kwargs: Optional keyword arguments
        :return: The serialized history instance
        """
        return PatientSerializer(instance).data


```


!!! info 
    
    All of the methods allow for the implementation of custom logic. However the ``accept`` method should
    somehow lead to the WebSocket accepting the request from a client to connect to the WebSocket stream.
    
    Sidenote: A customized disconnect method is also possible.