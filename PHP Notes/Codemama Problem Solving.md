```php
// Example One
<?php
    function checkInt(int $int1, int $int2){
        if($int1 === 10 || $int2 === 10){
            echo "True";
        } elseif ($int1 + $int2 === 10) {
            echo "True";
        } else {
            echo "False";
        }
    }
  
    fscanf(STDIN, "%d %d", $int1, $int2); // SPACE BY SPACE
    checkInt($int1, $int2);

// Example Two
<?php
   function singleName($input){
       list($fname, $lname) = explode(" ", $input);
       $name1 = trim($lname);
       $name2 = trim($fname);
       echo $name1.", ".$name2;
   }
   $input = fgets(STDIN); // LINE BY LINE
   $input2 = fgets(STDIN); // LINE BY LINE 2
   singleName($input);
```