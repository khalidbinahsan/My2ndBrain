## strlen()
You can the length of a string with this function
```php
<?php
$str = "Hello world";
echo strlen($str); // output 11
```
## strrev()
You can reverse your string with this function
```php
<?php
$str = "Hello world";
echo strrev($str); // output dlrow olleH
```

## str_repeat()
You can repeat your number in certain period of time
```php
<?php
$str = "***-";
echo str_repeat($str, 10); // output ***-***-***-***-***-***-***-***-***-***-
```

## strtolower()
To create the lower case of a string
```php
<?php
$str = "Hello world";
echo strtolower($str); // output hello world
```

## strtoupper()
To create the upper case of a string
```php
<?php
$str = "Hello world";
echo strtoupper($str); // output HELLO WORLD
```

## ucwords()
To make every words capitalize
```php
<?php
$str = "hello world";
echo ucwords($str); // output Hello World
```

## ucfirst()
To make the first word capitalize
```php
<?php
$str = "hello world";
echo ucfirst($str); // output Hello world
```

## explode()
To convert string in a array.
```php
$str = "hello world. I'm khalid bin ahsan";
$arr = explode(".", $str);
print_r($arr); // output array([0] => hello world [1] =>  I'm khalid bin ahsan)
```

## implode()
To convert a array to a string
```php
$arr = ["a", "b", "c"];
$str = implode("", $arr);
echo $str // output abc
```
## join()
To join string from array
```php
<?php
$arr = array("Hello", "World");
$str = join(" ", $arr);
echo $str; // output Hello World
```

## implode()
implode() doing the same things as like join()
```php
<?php
$arr = array("Hello", "World");
$str = implode(" ", $arr);
echo $str; // output Hello World
```
## trim()
To remove the whitespace from first and last of a string
```php
<?php
$str = "     Hello World     ";
$arr = trim($str);
echo $arr; // output Hello World
```

## ltrim()
To remove all whitespace form lest side of a string
```php
<?php
$str = "     Hello World     ";
$arr = ltrim($str);
echo $arr; // output Hello World.....
```

## rtrim()
To remove all whitespace form lest side of a string
```php
<?php
$str = "     Hello World     ";
$arr = rtrim($str);
echo $arr; // output ......Hello World
```

## str_split()
To convert a string to array
```php
$str = "Hello World";
$arr = str_split($str);
print_r($arr);  // output array
```
