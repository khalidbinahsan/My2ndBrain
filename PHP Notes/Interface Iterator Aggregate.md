Look at this real example about how the iterator aggregate work
```php
<?php
class DistrictCollection implements IteratorAggregate{
    private $district;
    public function __construct(){
        $this->district = array();
    }
    function addDistrict($district) {
        array_push($this->district, $district);
    }
    function getDistrict() {
        return $this->district;
    }
    function getIterator() {
        return new ArrayIterator($this-> district);
    }
}
$districts = new DistrictCollection();
$districts->addDistrict("Rajshahi");
$districts->addDistrict("Bogra");
$districts->addDistrict("Khulna");
$districts->addDistrict("Sylhet");
$districts->addDistrict("Jamalpur");
foreach($districts as $district) {
    echo $district."\n";
}
/* Output:
Rajshahi
Bogra
Khulna
Sylhet
Jamalpur
*/
```
## Interface Countable
You can add two interface or more in a single class. Look at the example below
```php
<?php
class DistrictCollection implements IteratorAggregate, Countable{
    private $district;
    public function __construct(){
        $this->district = array();
    }
    function addDistrict($district) {
        array_push($this->district, $district);
    }
    function getIterator() {
        return new ArrayIterator($this-> district);
    }
    function count() {
	    return count($this->district);
    }
}
$districts = new DistrictCollection();
$districts->addDistrict("Rajshahi");
$districts->addDistrict("Bogra");
$districts->addDistrict("Khulna");
$districts->addDistrict("Sylhet");
$districts->addDistrict("Jamalpur");
echo count($districts) //output: 5
```