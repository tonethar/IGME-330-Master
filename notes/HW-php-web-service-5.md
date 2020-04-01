# PHP Web Service Part V - adding authentication


[Overview](#overview)

[I. Get Started](#get-started)

<hr><hr>

<a id="overview" />

## Overview

<hr>

<a id="get-started" />

## I. Get Started


```php
<?php
// this web service returns a random number between 1 and max
 $max = 10; // default `$max` value is 10
 if(array_key_exists('max', $_GET)){
    $max = $_GET['max'];
    $max = (int)$max; // explicitly cast value to an integer
    $max = $max < 1 ? 1 : $max; // ternary operator
    $max = $max < getrandmax() ? $max : getrandmax(); // ditto
  }
	$num = rand(1,$max);
	header('content-type:application/json'); 
	echo "{\"message\": \"success\", \"value\": $num }";
?>
```


<hr><hr>

**[Previous Chapter <- PHP Web Service - Part IV](HW-php-web-service-4.md)**
