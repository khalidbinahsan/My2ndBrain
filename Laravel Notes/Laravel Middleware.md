Middleware is like a security level of Laravel application. It's execute after request but before response. When the server get a request, that actually go through the middleware and can manipulate the request or verify the authentication of it. Let's see some practical example
```php
public function handle(Request $request, Closure $next): Response
    {
        $key = $request->header('API-KEY');
        if($key == "1234XYZ") {
            return $next($request);
        } else {
            return response()->json("Unauthorized", 401);
        }
    }
```
This is the Middleware function. You should send the "API_KEY" key with your header. Your Router should be like the following Route
```php
Route::get('/hello', [DemoController::class, 'index'])->middleware([DemoMiddleware::class]);
```
Note: if the request pass the middleware, than it will go to the controller. Otherwise that will return a 401 unauthorized response.

You can also redirect from the Middleware
```php
public function handle(Request $request, Closure $next): Response
    {
        $api = $request->api;
        if($api == "123") {
            return $next($request);
        } else {
            return redirect('/hello2');
        }

    }
```
## Apply Middleware in a Route Group
```php
Route::middleware([DemoMiddleware::class])->group(function() {
    Route::get('/hello1/{api}', [DemoController::class, 'index1']);
    Route::get('/hello2/{api}', [DemoController::class, 'index2']);
    Route::get('/hello3/{api}', [DemoController::class, 'index3']);
    Route::get('/hello4/{api}', [DemoController::class, 'index4']);
});
```
## Apply Middleware in Whole Application
In Laravel 10, there was a way to use middleware to in ==Kernel.php== but in Laravel 11, the ==Kernel.php== is no longer available.
No we need to write the middle in the ==bootstrap/app.php== file. Let's see the example how to use middleware for whole application
```php
->withMiddleware(function (Middleware $middleware) {
     $middleware->web(append: [
	     DemoMiddleware::class,
     ]);
     
     $middleware->api(prepend: [
		EnsureTokenIsValid::class,
	]);
})
```
## Manipulate Headers
You can Manipulate the request header from the Middleware
```php
 public function handle(Request $request, Closure $next): Response
    {
        $request->headers->add(['email'=>'khalidbinahsan.com']);
        return $next($request);
    }
```
You can also change the Header value from the Middleware
```php
public function handle(Request $request, Closure $next): Response
    {
        $request->headers->replace(['email'=>'me@gmail.com']);
        return $next($request);
    }
```
## Request Rate Limiting
To prevent the unlimited request from user we can use the Request Rate Limiting Middleware in our Route
```php
Route::get('/request', [DemoController::class, 'requestLimit'])->middleware('throttle:5,1');
```
Here the ==throttle== is the Middleware name, ==5== is how many request you can send, ==1== is how per minutes.

You can set that for all the request in your application from ==bootstrap/app.php==
```php
 ->withMiddleware(function (Middleware $middleware) {
        $middleware->web(append: [
            'throttle:60,1'
        ]);
        $middleware->api(prepend: [
            'throttle:60,1'
        ]);
    })
```