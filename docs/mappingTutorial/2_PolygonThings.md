---
title: Polygon Things
layout: default
category: mappingTutorial
order: 1
---

# Polygon things

Locations and FeaturesOfInterest in a SensorThings service are not always points.
In our Demograph use case we have the statistical NUTS regions as things, with the polygon of the region as Location, in various differnent resolutions.

__Lets put those on a map!__

First, lets see what the data looks like in the service.

- NUTS Regions exist in four levels, level 0 to 3:
  - Level 0: Countries
  - Level 3: Counties

Each Thing in the service has various properties useful for filtering.
The top-level NUTS region for Germany:

```
https://demography.k8s.ilt-dmz.iosb.fraunhofer.de/v1.1/Things?
  $filter=properties/countryCode eq 'DE' and properties/level eq 0&
  $count=true
```

