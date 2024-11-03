### json_encode()
To convert PHP associative array to json object
```php
<?php
$assArray = ["name" => "Jhon", "age" => 30];
echo json_encode($assArray); // output {"name":"Jhon","age":30}
```

### json_decode()
To convert json array to the PHP associative array. It will accept two parameter. true value is fixed.
```php
<?php
$demoStr = '[{"name":"Jhon","age":30},{"name":"Ahme","age":60}]';
print_r(json_decode($demoStr, true)); // output Array ( [0] => Array ( [name] => Jhon [age] => 30 ) [1] => Array ( [name] => Ahme [age] => 60 ) )
```