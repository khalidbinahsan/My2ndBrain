Interface is a code block like abstract class in php. You can't extends the interface but implements with class. It's more like you will declear some method on interface then when you implements, you must override that method on the new class.  Let's see the example below
```php
interface BaseAnimal {
    function isAlive();
    function canEat($param1, $param2);
    function bread();
}

class Animal implements BaseAnimal {
    function isAlive(){}
    function canEat($param1, $param2){}
    function bread(){}
}
```