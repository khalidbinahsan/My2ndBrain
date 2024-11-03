To keep your application history, Laravel Log is a important feature. Let's see how to save the log history
You must import the class
use Illuminate\Support\Facades\Log;
## Log::info()
```php
public function sum(Request $request) : int
    {
        $num1 = $request->num1;
        $num2 = $request->num2;
        $sum = $num1 + $num2;
        Log::info($sum);
	    return $sum;
    }
```
## Log type
Log has some different type. Let's have look
```php
Log::info();
Log::emergency();
Log::alert();
Log::critical();
Log::error();
Log::warning();
Log::notice();
Log::debug();
```

## Package
[Laravel Pail](https://laravel-news.com/laravel-pail)
You can use this package to tail your log file more effectively.