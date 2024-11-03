## Enable PHP strict mode
To enable php strict mode write this function to the top on your code
```php
<?php
declare(strict_types=1)
```

## number_format(_number,decimals,decimalpoint,separator_)
You can convert you number with the decimal point with this function.
```php
<?php
    function totalPrice($price, $discount) {
        $percentage = $discount / 100;
        $sellPrice = $price - ($price * $percentage);
        echo "Price: ".number_format($sellPrice, 2);
    };

    totalPrice(50, 20); // Output: Price: 40.00

?>
```
## round()
To round the number `10.44` to the nearest integer in PHP, you can use the `round()` function.
```php
$number = 10.44; 
$nearestInteger = round($number); 

echo $nearestInteger; // output: 10
```
## floor()
To round the number 10.75 always down to the nearest integer in PHP, you can use the floor() function.
```php
$number = 10.75; 
$nearestInteger = floor($number); 

echo $nearestInteger; // output: 10
```
## ceil()
To round the number `10.44` up to the nearest integer in PHP, you can use the `ceil()` function.
```php
$number = 10.44;
$upperInteger = ceil($number);

echo $upperInteger; // outpur: 11
```
## min()
You can find the lowest (or minimum) number in an array in PHP using the `min()` function.
```php
$numbers = [5, 3, 9, 1, 7, 4];
$lowestNumber = min($numbers);

echo $lowestNumber; // output: 1
```
## max()
To find the highest (or maximum) number in an array in PHP, you can use the `max()` function.
```php
$numbers = [5, 3, 9, 1, 7, 4];
$highestNumber = max($numbers);

echo $highestNumber; // output: 9
```
## array_sum()
To sum all array number
```php
$array = [10, 20, 30];
echo array_sum($array); // output: 70
```
## count()
Count the array index
```php
$array = [10, 20, 30];
echo count($array); // output: 3
```