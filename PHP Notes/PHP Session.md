Always your should write the session_start() when you work with the session. Here is the example
```php
<?php
// This is for store the session data
session_start();
$_SESSION["userEmail"] = "khalidbinahsan";

// This is for read the session data
session_start();
echo $_SESSION["userEmail"];

// This is for delete the all the session variable
session_start();
session_destroy();

// This is for delete the specific variable
session_start();
unset($_SESSION["userEmail"]);
```