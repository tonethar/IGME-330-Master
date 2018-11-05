# HW - Maps Part I

## I. Overview
- This exercise gives you a chance to work with the google maps API:
  - get an API key
  - set the zoom level and center of the map with buttons
  - add markers to the map
- The instructions are here: [Maps-1.pdf](./_files/Maps-1.pdf (6.7 MB))
- start files are below
- See mycourses.rit.edu dropbox for due date
  
## II. Start Files

**map-simple-start.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Simple Map</title>
    <meta name="viewport" content="initial-scale=1.0">
    <meta charset="utf-8">
    <style>
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
      #map {
        height: 100%;
      }
    </style>
  </head>
  <body>
    <div id="map"></div>
    <script>
      var map;
      function initMap() {
        map = new google.maps.Map(document.getElementById('map'), {
          center: {lat: -34.397, lng: 150.644},
          zoom: 8
        });
      }
    </script>
    <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=initMap"
    async defer></script>
  </body>
</html>
```

**coffee-data.js**

```js
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
```

**building-data.js** (for the *optional* portion of the HW)

```js
const buildings = [
{
	latitude:43.084156,
	longitude:-77.67514,
	title:"GOL - Golisano Hall",
	path: [
	{lat:43.084255, lng:-77.679697},{lat:43.083828, lng:-77.679683},{lat:43.083822, lng:-77.679643},
	{lat:43.083781, lng:-77.679643},{lat:43.083781, lng:-77.679686},{lat:43.083732, lng:-77.679689},
	{lat:43.083732, lng:-77.679753},{lat:43.083672, lng:-77.679764},{lat:43.083662, lng:-77.680016},
	{lat:43.083726, lng:-77.680016},{lat:43.083726, lng:-77.680078},{lat:43.083775, lng:-77.680078},
	{lat:43.083777, lng:-77.680134},{lat:43.083817, lng:-77.680134},{lat:43.083983, lng:-77.680091},
	{lat:43.084308, lng:-77.680102},{lat:43.084310, lng:-77.680142},{lat:43.084347, lng:-77.680142},
	{lat:43.084338, lng:-77.680789},{lat:43.084665, lng:-77.680791},{lat:43.084669, lng:-77.680695},
	{lat:43.084692, lng:-77.680695},{lat:43.084690, lng:-77.680021},{lat:43.084677, lng:-77.679997},
	{lat:43.084677, lng:-77.679920},{lat:43.084688, lng:-77.679898},{lat:43.084714, lng:-77.679882},
	{lat:43.084739, lng:-77.679871},{lat:43.084759, lng:-77.679844},{lat:43.084776, lng:-77.679812},
	{lat:43.084802, lng:-77.679772},{lat:43.084818, lng:-77.679718},{lat:43.084833, lng:-77.679681},
	{lat:43.084827, lng:-77.679662},{lat:43.084641, lng:-77.679662},{lat:43.084628, lng:-77.679635},
	{lat:43.084596, lng:-77.679635},{lat:43.084516, lng:-77.679726},{lat:43.084510, lng:-77.679611},
	{lat:43.084255, lng:-77.679611}
	]
},

{
	latitude:43.08363,
	longitude:-77.67881,
	title:"ORN- Orange Hall",
	path:[
	{lat:43.083745, lng:-77.678408},{lat:43.083561, lng:-77.678397},{lat:43.083524, lng:-77.678427},
	{lat:43.083522, lng:-77.678572},{lat:43.083553, lng:-77.678574},{lat:43.083551, lng:-77.678773},
	{lat:43.083522, lng:-77.678775},{lat:43.083516, lng:-77.678952},{lat:43.083549, lng:-77.678952},
	{lat:43.083545, lng:-77.679044},{lat:43.083514, lng:-77.679046},{lat:43.083512, lng:-77.679178},
	{lat:43.083551, lng:-77.679180},{lat:43.083549, lng:-77.679215},{lat:43.083737, lng:-77.679221}
	]
}
];
```
