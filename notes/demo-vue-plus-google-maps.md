# Demo - Combining Vue.js and google maps

- How do you integrate google maps & its `callback`  parameter with Vue.js? See below!

## I. Full Working Version

ZIP file is here --> [vue-plus-google-maps-need-API-KEY.zip](_files/vue-plus-google-maps-need-API-KEY.zip)

## II. HTML & JS Source Code

**google-map-vue.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Vue and Google Maps</title>
	<script src="map_data/coffee-data.js"></script>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<style>
	 #map {
	 			width: 800px;
        height: 400px;
    }
	</style>
</head>
<body>
<div id="root">
	 <div id="map"></div>
		<p>
			<button @click="setZoom(1)">World Zoom (1)</button>
			<button @click="setZoom(16)">Default Zoom (16)</button>
			<button @click="setZoom(20)">Building Zoom (20)</button>
			<button @click="setZoom(18)">Isometric View (18)</button>
    </p>
</div>

<script>
"use strict";
/*
	Make `app` a global by using `var`, now we can ...&callback=app.initMap from the google map script near the bottom of this file
*/
var app = new Vue({
	el: "#root",
	methods:{
	
		initMap(){
			const mapOptions = {
				center: {lat:43.083848, lng:-77.6799},
				zoom: 16,
				mapTypeId: google.maps.MapTypeId.ROADMAP
			};

			this.map = new google.maps.Map(document.getElementById('map'), mapOptions);
			this.map.mapTypeId = 'satellite';
			this.map.setTilt(45);
			this.coffeeShops = coffeeShops;
			for(let obj of this.coffeeShops){
        this.addMarker(obj.latitude, obj.longitude, obj.title);
      }
		},
		
		addMarker(latitude,longitude,title) {
			let position = {lat:latitude,lng:longitude};
  		let marker = new google.maps.Marker({position: position, map:this.map});
  		marker.setTitle(title);
  		// Add a listener for the click event
			google.maps.event.addListener(marker, 'click', function(e){
				// `this` doesn't work here - because it refers to the marker that was clicked on - use `app` instead
				app.makeInfoWindow(this.position,this.title);
			});
		},
		
		makeInfoWindow(position,msg){
		 // Close old InfoWindow if it exists
      if(this.infowindow) this.infowindow.close();
      	 	
      // Make a new InfoWindow
      this.infowindow = new google.maps.InfoWindow({
            map: this.map,
            position: position,
            content: "<b>" + msg + "</b>"
      });
    },
		
		setZoom(zoomLevel){
      this.map.setZoom(zoomLevel);
		}
	}
});
  
</script>
<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=app.initMap" async defer></script>

</body>
</html>
```
