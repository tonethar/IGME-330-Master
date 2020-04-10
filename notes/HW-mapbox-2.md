# Mapbox-2 RIT Coffee Finder


***For all of the steps going forward, keep the debugger console open to be sure that you don’t have any errors***

## I. Get Started

1) Duplicate the **custom-marker** folder and name it **rit-coffee-finder**

2) Download ![**coffee-icon.png**](./_images/_map-images/coffee-icon.png | width=50) and put it into the **images** folder

3) Modify your CSS to use the new icon, and change the width and height to 30px

4) Delete the contents of the `features` array (inside the `GeoJSON` object) - it should look like this:

```js
let geojson = {
  type: 'FeatureCollection',
  features: []
};
```
- now move the `let geojson = {…};` code OUTSIDE of the `init()` method
- Reload the page - the markers should be gone.

5) Change the `center` and `zoom` properties of the map to zoom in on RIT - `[-77.6799,43.083848]` and `14`

    - Reload the page - the map should be zoomed in on RIT

6) Now create a function named `initMap()` and move the `mapboxgl.accessToken = …` and `const map = new mapboxgl.Map({…});` code into it

    - But you’ll need to declare `map` at the top of **main.js** now, with a `let` declaration

7) Now call `initMap()` from the top of `init()`

    - Test your code in the browser, it should work the same

8) Now create a new function named `addMarkersToMap()` and move the marker creation code into it

9) In `init()`,  call `addMarkersToMap()` right after you call `initMap()`

Test your code in the browser, it should work the same

10) This is what main.js should look like (I’ve folded some code, obviously):

![screenshot](./_images/_map-images/maps-5.jpg)


## II. Add some markers

1) let’s create a new function named `loadMarkers()` - it will look like this:

```js
function loadMarkers(){
	const coffeeShops = [
		{
			latitude:43.084156,
			longitude:-77.67514,
			title:"Artesano Bakery & Cafe"
		},

		{
			latitude:43.083866,
			longitude:-77.66901,
			title:"Beanz"
		},

		{
			latitude:43.082520,
			longitude:-77.67980,
			title:"Midnight Oil"
		},

		{
			latitude:43.086678,
			longitude:-77.669014,
			title:"The College Grind"
		},

		{
			latitude:43.082634,
			longitude:-77.68004,
			title:"The Cafe & Market at Crossroads"
		},

		{
			latitude:43.08382,
			longitude:-77.674805,
			title:"RITZ Sports Zone"
		},

		{
			latitude:43.086502,
			longitude:-77.66912,
			title:"The Commons"
		},

		{
			latitude:43.08324,
			longitude:-77.68105,
			title:"The Market at Global Village"
		},

		{
			latitude:43.08384,
			longitude:-77.67457,
			title:"Brick City Cafe"
		},

		{
			latitude:43.084904,
			longitude:-77.6676,
			title:"Corner Store"
		},

		{
			latitude:43.08464,
			longitude:-77.680145,
			title:"CTRL ALT DELi"
		},

		{
			latitude:43.08359,
			longitude:-77.66921,
			title:"Gracie's"
		}
	];
	
	// now convert this data to GeoJSON

}
```


2) Here’s the rest of the code - you can type this:

![screenshot](./_images/_map-images/maps-6.jpg)

3) Now put a call to `loadMarkers()` in the `init()` function, right between `initMap();` and `addMarkersToMap()`

4) Reload the page, you should see the markers. Check the console, you should see the `geojson` logged out

![screenshot](./_images/_map-images/maps-7.jpg)

![screenshot](./_images/_map-images/maps-8.jpg)

5) XXX


