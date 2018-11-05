# HW - Maps Part I

## I. Overview
- This exercise gives you a chance to practice and review:
  - the canvas code needed to create circles, squares, and polygons
- The instructions are here: [Maps-1.pdf](./_files/Maps-1.pdf (6.7 MB))
- See mycourses.rit.edu dropbox for due date
  
## II. Start File

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
