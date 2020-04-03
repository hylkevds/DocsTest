---
layout: default
title: OGC SensorThings API
category: SensorThings API
order: 0
---

# Welcome to the API4INSPIRE wiki!
Here we will build a collection of resources essential for implementation, deployment and usage of the emerging INSPIRE APIs

## OGC API
[Development Specifications](https://github.com/DataCoveEU/API4INSPIRE/wiki/OGC-API-Specifications)

[Simple API Implementation](https://github.com/DataCoveEU/API4INSPIRE/wiki/Simple-OGC-API)

## SensorThings API

> The OGC SensorThings API is an OGC standard specification for providing an open and unified way to interconnect IoT devices, data, and applications over the Web. The SensorThings API is an open standard, builds on Web protocols and the OGC Sensor Web Enablement standards, and applies an easy-to-use REST-like style.

SensorThings API provides access to up-to-date measurement information that is:

* RESTful
* (Geo)JSON encoded
* Available via OASIS Odata URL patterns and query options
* Capable of directly including sensor data via the ISO MQTT protocol

This means that data from the API can be easily viewed using a normal Web Browser. One can simply navigate from one object to the next by clicking the URLs provided within the data.

For more information, please see the following sections:
* [Data Model](https://github.com/DataCoveEU/API4INSPIRE/wiki/STA-Data-Model)
* [Basic Requests](https://github.com/DataCoveEU/API4INSPIRE/wiki/STA-Basic-Requests)
* [Tailoring Requests](https://github.com/DataCoveEU/API4INSPIRE/wiki/STA-Tailoring-Requests)

If you're more for a hands-on approach, you can also just start playing with some of our services. Here's the link for near-real-time air quality data:
* https://airquality-frost.docker01.ilt-dmz.iosb.fraunhofer.de/v1.1

For context, a viewer operating on this endpoint:
* https://wg-brgm.docker01.ilt-dmz.iosb.fraunhofer.de/servlet/is/121/
