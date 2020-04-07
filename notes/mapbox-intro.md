# Mapbox Intro


- An alternative to google maps is Mapbox - let's check it out.


## I. Get Started

1. Sign up for an account here: https://account.mapbox.com/auth/signup/
2. On the account page - https://account.mapbox.com
3. Click the "Start by designing a map" button:
    - Choose "JS Web"
    - Choose "Use the Mapbox CDN"
    - Create an empty HTML page named **mapbox-start.html**
    - Follow the instructions and add the `<link>`and `<script>` tags, as well as the JS and HTML, to the page
    - Note that you will be given your Mapbox access token - keep a copy of it somewhere


**Here's what the HTML page will look like - you'll need to add your *access token* to it:**

**mapbox-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Map Start</title>
	<script src='https://api.mapbox.com/mapbox-gl-js/v1.8.1/mapbox-gl.js'></script>
	<link href='https://api.mapbox.com/mapbox-gl-js/v1.8.1/mapbox-gl.css' rel='stylesheet' />
</head>
<body>
<div id='map' style='width: 400px; height: 300px;'></div>
<script>
	mapboxgl.accessToken = 'ACCESS-TOKEN-GOES-HERE-GO-GET-YOUR-OWN!';
	var map = new mapboxgl.Map({
	container: 'map',
	style: 'mapbox://styles/mapbox/streets-v11'
	});
</script>

</body>
</html>
```

<hr>

## I-A. Test it

Screenshot of **mapbox-start.html**:

![screenshot](./_images/_map-images/maps-1.jpg)


<hr>

## I-B. Some things to try

1) Change the `center` and `zoom` of the map to the Rochester area:

```js
map.setZoom(9);
map.setCenter([-77.6799,43.083848]); // note the order - it's longitude,latitude - which is opposite of Google Maps
```

2) Go to this landing page --> https://www.mapbox.com/install/js/cdn-complete/
    - Now navigate to the [Add controls](https://docs.mapbox.com/mapbox-gl-js/example/navigation/) page to add a visible controller to your map (it's one line of code)

3) Head back to the landing page
    - Now navigate to [Style Animation](https://docs.mapbox.com/mapbox-gl-js/example/setstyle/) page:
    - You don't need to set up the radio buttons, but go ahead and change you map's style from  `streets-v11` to: 
      - `light-v10` OR
      - `dark-v10` OR
      - `outdoors-v11` OR
      - `satellite-v9`
    - You can also write code to change the style like this: `map.setStyle('mapbox://styles/mapbox/satellite-v9');`

4) Head back to the landing page
    - Now navigate to [Display a popup on click](https://docs.mapbox.com/mapbox-gl-js/example/popup-on-click/)
    - Try out the completed version of this map by clicking on the various symbols and viewing the popups
    - Look at the code starting at:
    
    ```js
    map.addSource('places', {
      'type': 'geojson',
      'data': {
        ...
      }
    ```
    
    - the `data` property here points at a GeoJSON object, which is the primary format that Mapbox expects location i.e. "Point of Interest" data to be encoded in:
      - https://geojson.org
      - http://geojson.io/ - a GeoJSON "builder" - one thing you can do is to drop markers on the map and this will write the GeoJSON for you 
    - 
    
<hr>

## II. Add Clickable Markers

- Create a new empty HTML page named **mapbox-markers.html**
- Follow this tutorial here - https://docs.mapbox.com/help/tutorials/custom-markers-gl-js/ - which give you something that looks like this:

![screenshot](./_images/mapbox-2.png)

<hr>

## III. RIT Coffee Map

- Here is a marker icon you will need (right-click to download) --> <img src="_images/coffee-icon.png" height="50" width="50" >
- To get started on the RIT coffee map, we just have to slightly modify the above tutorial - here's a screenshot of the code, and the final result (with 3 coffee shops showing)

**rit-coffee-mapbox.html**

![screenshot](./_images/mapbox-3.png)

![screenshot](./_images/mapbox-4.png)

![screenshot](./_images/mapbox-5.png)

Screenshot of **rit-coffee-mapbox.html**:

![screenshot](./_images/mapbox-6.png)






