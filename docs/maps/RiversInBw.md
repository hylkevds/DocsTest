---
title: Rivers in BW
layout: default
category: maps
order: 2
---

# Rivers in Baden-Württemberg

Data from the [LUBW](https://www.lubw.baden-wuerttemberg.de).


<div id="mapid" style="height: 850px;"></div>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css" integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ==" crossorigin=""/>
<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js" integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew==" crossorigin=""></script>
<script src='https://api.mapbox.com/mapbox.js/plugins/leaflet-fullscreen/v1.0.1/Leaflet.fullscreen.min.js'></script>
<link href='https://api.mapbox.com/mapbox.js/plugins/leaflet-fullscreen/v1.0.1/leaflet.fullscreen.css' rel='stylesheet' />
<script  src="https://unpkg.com/sta-map@1.2.2/dist/stam.min.js"></script>
<script type="text/javascript">
	var mymap = L.map('mapid').setView([48.5, 9.00], 8);
	mymap.addControl(new L.Control.Fullscreen());
	L.tileLayer('https://{s}.tile.iosb.fraunhofer.de/tiles/osmde/{z}/{x}/{y}.png', {
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
		maxZoom: 18
	}).addTo(mymap);
	L.stam({
		baseUrl: "https://lubw.k8s.ilt-dmz.iosb.fraunhofer.de/v1.1",
		MarkerStyle: "yellow",
		clusterMin: 20,
		queryObject: {
			count: true,
			skip: 0,
			entityType: 'Things',
			filter: "properties/type eq 'waterBody'",
			select: null,
			expand: null,
			top: 0
		}
	}).addTo(mymap);
</script>


