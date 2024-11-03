Look at the example how to set cookie, read cookie and delete cookie
```php
<?php
// To set cookie
setcookie("token1", "abc1234xyz");
setcookie("token2", "abc1234xyz");
setcookie("token3", "abc1234xyz");

// To read cookie
echo $_COOKIE['token1'];

// To delete cookie
setcookie("token3", "");
```