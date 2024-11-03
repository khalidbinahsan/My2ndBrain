To crate a controller the command is 
```bash
php artisan make:controller MyController
```
Route
```php
Route::get('/about', [MyController::class, 'methodName']);
```
## Single Action Controller
This controller is for manage only one action with the ==--invoke==
```bash
php artisan make:controller MyController --invokable
```
Route
```php
Route::get('/invoke', SingleAction::class);
```
Note: No need to call any function here. the ==--invoke== constructor will run automatically.

## Resource Controller
With this controller the basic ==CRUD== operation methods will generate automatically in the controller class. 
```bash
php artisan make:controller ControllerName --resource
```
Route
```php
Route::resource('photos', PhotoController::class);
```
You don't need to declare the function name in the route. Let's see how the function are invoked
```php
GET()       index()         http://127.0.0.1:8000/photos
GET()       create()        http://127.0.0.1:8000/photos/create
POST()      store()         http://127.0.0.1:8000/photos
GET()       show()          http://127.0.0.1:8000/photos/{id}
GET()       edit()          http://127.0.0.1:8000/photos/{id}/edit
PUT/PATCH() update()        http://127.0.0.1:8000/photos/{id}
DELETE()    destroy()       http://127.0.0.1:8000/photos/{id}
```
Let's have a look how generated the resource controller
```php
class PhotoController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        return 'This is index method';
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        return 'This is create method';
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        return 'This is store method';
    }

    /**
     * Display the specified resource.
     */
    public function show(string $id)
    {
        return 'This is show method';
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(string $id)
    {
        return 'This is edit method';
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, string $id)
    {
        return 'This is update method';
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(string $id)
    {
        return 'This is destroy method';
    }
}
```
Note: You can't change the method name. You should keep the name as it is.
## Get Request Input
To get the request input here is a simple example
```php
function getData(Request $request){
	$fname = $request->input('fname');
	return $fname;
}
```
## Get Request Header
To get the request header here is a simple example
```php
function getHeader(Request $request){
	$host = $request->header('host');
	return $host;
}
```
## Get query string
To get the query string you can use the query() function. Suppose your query is https://khalidbinahsan.com?id=1 let's see the code
```php
function getQuery(Request $request) {
  $query = $request->query();
  return $query;
}
```

## Extra Function
### abort()
To showing error
```php
return abort("404", "Not Found");
```
### redirect()
To redirect any url
```php
return redirect("/contact");
```