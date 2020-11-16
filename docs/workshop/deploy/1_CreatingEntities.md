---
layout: default
title: Creating Entities
category: deploymentTutorial
topCategory: workshop
order: 1
---

# Creating New Entities

The OGC SensorThings API does not just allow you to read data, it is possible to create, update and delete all data too.

## Creating basic entities

Creating is done by making a http POST to a collection.
For instance, to create a new Thing, the JSON description of the Thing is posted to `v1.1/Things`:

```
POST https://example.org/FROST-Server/v1.1/Things
```
```javascript
{
  "name" : "lantern",
  "description" : "camping lantern",
  "properties" : {
    "property1" : "it’s waterproof",
    "property2" : "it glows in the dark"
  }
}
```

## POSTing to FROST-Server

How do you make a POST request? With your web browser!
You can use a browser plugin, like RESTClient (for Firefox) or Postman (Google Chrome), but since recently, the FROST-Server
landing page has a handy little form that can used to POST entities to your server.

If you run a server on your own machine, with Docker, you can find it at: 

> [http://localhost:8080/FROST-Server/](http://localhost:8080/FROST-Server/)


If you do not have your own server you can use our public demo instance at:

> [https://ogc-demo.k8s.ilt-dmz.iosb.fraunhofer.de/](https://ogc-demo.k8s.ilt-dmz.iosb.fraunhofer.de/)

Lets create a Thing. If you use our shared server, make sure you put your (nick)name in the name or
definition of the Thing you create, so you can find it back later!

After succesfully creating an entity the server responds with a header containing the URL of the newly created entity:
```
Location: https://ogc-demo.k8s.ilt-dmz.iosb.fraunhofer.de/v1.1/Things(19)
```


## What entities to create, in which order

All entities can link to other entities. In some cases, these relations are mandatory.
For instance, a Datastream must link to a Thing, a Sensor and an ObservedProperty.
The Datamodel shows all these relations:

![SensorThings API Data Model](../../images/SensorThingsAPI_DatenModel_v1.1-900.png)

This means there is a certain order in which the entities must be created.
It's impossible to create an Observation without a Datastream.
The usual order is:

1. Thing
1. Location
1. _ObservedProperty_
1. _Sensor_
1. Datastream
1. Observation (+FeatureOfInterest)

ObservedProperties and Sensors are often shared across many Datastreams.
You only need one definition of `Temperature` in your server.
Sensors are also often shared among all Datastreams the hold data for the same _type_ of sensor, though in some
use cases there is a separate Sensor entity for each actual sensor.

Now we need to create a Location, but how do we link it to our Thing?


## Creating entities with (required) relations

When creating an entity that needs to link to an already existing entity, the ID of that related entity can be specified in the JSON of the Entitiy we want to create.

```javascript
{
  "name": "Location of the kitchen",
  "description": "This is where the kitchen is",
  "properties": {},
  "encodingType": "application/geo+json",
  "location": {
    "type": "Point",
    "coordinates": [8.10, 50.00]
  },
  "Things": [
    { "@iot.id": 999}
  ]
}
```


The following example crates a Datastream, and links to an existing Thing (with id 2), Sensor (with id 5) and ObservedProperty (with id 3):

```
POST https://example.org/FROST-Server/v1.1/Datastreams
```
```javascript
{
  "name" : "Temperature in the Kitchen",
  "description" : "The temperature in the kitchen, measured by the sensor next to the window",
  "observationType": "http://www.opengis.net/def/observationType/OGC-OM/2.0/OM_Measurement",
  "unitOfMeasurement": {
    "name": "Degree Celsius",
    "symbol": "°C",
    "definition": "ucum:Cel"
  },
  "Thing": {"@iot.id": 2},
  "Sensor": {"@iot.id": 5},
  "ObservedProperty": {"@iot.id": 3}
}
```

It is also possible to specify one relation in the URL of the POST instead of in the JSON.
The following two POSTs both create a new Observation in Datastream 14:

```
POST https://example.org/FROST-Server/v1.1/Observations
```
```javascript
{
  "result" : 21,
  "Datastream": {"@iot.id": 14}
}
```

In the following example, the post is made to `v1.1/Datastreams(14)/Observations`, i.e. to the collection of Observations belonging to Datastream 14.
This automatically links the new Observation to Datastream 14.
```
POST https://example.org/FROST-Server/v1.1/Datastreams(14)/Observations
```
```javascript
{
  "result" : 21
}
```




