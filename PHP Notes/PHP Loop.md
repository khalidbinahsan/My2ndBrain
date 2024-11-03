Here is get the short example of PHP loop
```php

// for loop
for( $i = 0; $i < 10; $i = $i + 1) {
    echo '<button>Learn More</button><br>';
}

// while loop
$i = 0;
while($i < 16){
    echo '<button>Load more</button><br>';
    $i++;
}

// Alternative template of while loop
$i = 1;
while ($i < 6):
  echo $i;
  $i++;
endwhile;

// do while loop
$i = 0;
do{
    echo '<button>Buy Now</button> <br>';
    $i++;
}
while($i < 16);

// goto loop
$i = 0;
a: $i++;
echo $i.PHP_EOL;
if($i < 10) goto a;

// foreach loop
$colors = array("red", "green", "blue", "yellow");

foreach ($colors as $x) {
  echo "$x <br>";
}

// foreach in assocciative array
$members = array("Peter"=>"35", "Ben"=>"37", "Joe"=>"43");

foreach ($members as $x => $y) {
  echo "$x : $y <br>";
}

// foreach loop in object
class Car {
  public $color;
  public $model;
  public function __construct($color, $model) {
    $this->color = $color;
    $this->model = $model;
  }
}

$myCar = new Car("red", "Volvo");

foreach ($myCar as $x => $y) {
  echo "$x: $y <br>";
}

// Alternative syntext of foreach
$colors = array("red", "green", "blue", "yellow");

foreach ($colors as $x) :
  echo "$x <br>";
endforeach;

```
