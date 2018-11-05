# Demo: PHP-driven Web Service

**get-a-joke.php**

```php
<?php
/*
	Name: get-a-joke.php
	Description: Returns a single random joke in JSON format
	Author: Keyser Soze
	Last Modified: 11/5/2018
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

// json_encode() turns an associative array into a string of well-formed JSON
$string = json_encode($randomJoke);

// Sends the correct HTTP header
header('content-type:application/json');
echo $string;


?>
```

**get-a-joke-2.php**

```php
<?php
/*
	Name: get-a-joke-2.php
	Description: Returns a single random joke in JSON format
	Author: Keyser Soze
	Last Modified: 11/5/2018
*/
if(array_key_exists('callback', $_GET)){
	$callback = $_GET['callback'];
}else{
	$callback = NULL;
}

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

// json_encode() turns an associative array into a string of well-formed JSON
$string = json_encode($randomJoke);

if ($callback){
	// Sends the correct HTTP header
	header('content-type:application/javascript');
	$string = $callback . "(" . $string . ")";
}else{
	// Sends the correct HTTP header
	header('content-type:application/json');
}

echo $string;


?>
```
