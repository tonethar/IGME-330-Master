# XML Web Services

- Here we will create an XML web service, and downlaod it via the XHR object.


I. XML Web Service (written in PHP)

- This service is online here: http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke-xml.php 

**get-a-joke-xml.php**

```php
<?php
/*
	Name: get-a-joke-xml.php
	Description: Returns a single random joke in XML format
	Author: Keyser Soze
	Last Modified: 11/12/2018
*/

// $jokes contains our data
// this is an indexed array of associative arrays
// the associative arrays are jokes -  they have an 'q' key and an 'a' key
$jokes = array(
	array("q"=>"What do you call a very small valentine?","a"=>"A valen-tiny!"),
	array("q"=>"What did the dog say when he rubbed his tail on the sandpaper?","a"=>"Ruff, Ruff!"),
	array("q"=>"Why don't sharks like to eat clowns?","a"=>"Because they taste funny!"),
	array("q"=>"What did the boy cat say to the girl cat?","a"=>"You're Purr-fect!"),
	array("q"=>"What is a frog's favorite outdoor sport?","a"=>"Fly Fishing!")
);

// get a random element of the $jokes array
// there are a bunch more PHP array functions at: http://php.net/manual/en/ref.array.php
$numJokes = count($jokes);
$randomJoke = $jokes[mt_rand(0, $numJokes - 1)];

$string = "<joke>\n";
$string .= "<q>{$randomJoke[q]}</q>\n";
$string .= "<a>{$randomJoke[a]}</a>";
$string .= "</joke>";

// Sends the correct HTTP header
header("Access-Control-Allow-Origin: *");
header('content-type:application/xml');
echo $string;

?>
```
