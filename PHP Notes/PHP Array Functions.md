## array_values()
You can get the values of an array with this function 
```php
<?php
$bilGates = [
    "firstName" => "Bill",
    "lastName" => "Gates",
    "age" => 45,
    "gender" => "Male",
    "email" => "gates@gmail.com",
    "phone" => "08801756747"
];
$values = array_values($bilGates);
print_r($values);
```

## array_keys()
you can get the array key with this function
```php
<?php
$bilGates = [
    "firstName" => "Bill",
    "lastName" => "Gates",
    "age" => 45,
    "gender" => "Male",
    "email" => "gates@gmail.com",
    "phone" => "08801756747"
];
$keys = array_keys($bilGates);
print_r($keys);
```

## array_key_exists()
You can find your array item with it's key
```php
<?php
$bilGates = [
  "firstName" => "Bill",
  "lastName" => "Gates",
  "age" => 45,
  "gender" => "Male",
  "email" => "gates@gmail.com",
  "phone" => "08801756747"
];
$isExist = array_key_exists("firstName", $bilGates);
print_r($isExist);
```

## array_search
You can search your array with it's value from here
```php
<?php
$bilGates = [
  "firstName" => "Bill",
  "lastName" => "Gates",
  "age" => 45,
  "gender" => "Male",
  "email" => "gates@gmail.com",
  "phone" => "08801756747"
];
$findArray = array_search("Male", $bilGates);
print_r($findArray); // Output: gender
```

## array_flip()
You can flip your array with this function
```php
<?php
$bilGates = [
  "firstName" => "Bill",
  "lastName" => "Gates",
  "age" => 45,
  "gender" => "Male",
  "email" => "gates@gmail.com",
  "phone" => "08801756747"
];
$flipArray = array_flip($bilGates);
print_r($flipArray);
```

## count(), sizeof()
You can count the array how much elements there is 
```php
<?php
$fruites = ["Mango", "Lychee", "Banana"];
$count = count($fruites);
$count2 = sizeof($fruites);
echo $count;
echo $count2;
```

## array_sum()
You can sum your array with this function
```php
<?php
$number = [1,2,3,4,5,6];
$sum = array_sum($number);
echo $sum;
```

## array_product()
You can multiply your array with this function
```php
<?php
$number = [1,2,3,4,5,6];
$multiply = array_product($number);
echo $multiply;
```

## array_merge()
You can merge your array with this function
```php
<?php
$number1 = [1,2,3,4,5,6];
$number2 = [5,6,7,8,9,10];
$merge_me = array_merge($number1, $number2);
print_r($merge_me);
```

## array_replace()
You can replace one with another array
```php
<?php
$city1 = ["Dhaka", "Khulna", "Barisal", "Comilla"];
$city2 = ["Mirpur", "Noakhali", "Gulshan", "Chittagong"];
$replace = array_replace($city1, $city2);
print_r($replace);
```

## sort()
You can sort your array with ascending order
```php
<?php
$city1 = ["Dhaka", "Khulna", "Barisal", "Comilla"];
$sort = sort($city1);
print_r($sort);
```

## array_unique()
To remove the duplicate character from array
```php
<?php
$arr = ["a", "b", "c", "b"];
$newArr = array_unique($arr);
print_r($newArr)  // output ["a", "b", "c"]
```