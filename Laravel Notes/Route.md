## get()
Look at the some example to create route
```php
Route::get('/url', [ControllerName::class, 'functionName']);
```
For the dynamic route you can follow this 
```php
Route::get('/url'/{id}, [ControllerName::class, 'functionName']);
```
For optional parameter you need to set **?** in route and a default value in Controller
```php
Route::get('/url/{id?}', [ControllerName::class, 'functionName']);

// Controlle function should be like this
fucntion functionName(Request $request, $id = 0) {
	if($id == 0) {
		return "Nothign is found";
	} else {
		return response("Your Id is $id");
	}
}
```
## post()
You get the form response by the post() function
```php
Route::post('/url', [ControllerName::class, 'functionName']);
```
Your controller function should be like this
```php
function functionName(Request $request) {
	return $request->input('form_name');
}
```
## match()
If you want to request the **get** and **post** both in the same url, you need to make route with the **match()** function
```php
Route::match(['get', 'post'], 'countries', [ControllerName, 'functionName']);
```
Now let's see how we can get the post method from controller function
```php
function functionName(Request $request){
	if ($request->isMethod('post')) {
		return "This is from post method";
	}
	return view("home");
}
```