Sessions is a important part to save data temporary. Let's see how to store session data and get the data or delete in Laravel
## session()->put()
To set the session data
```php
function sessionPut(Request $request):bool
    {
        $email = $request->email;
        $request->session()->put('userEmail', $email);
        return response("Session data has been set");
    }
```
## session()->get()
To get the session data multiple times
```php
function sessionGet(Request $request):string
    {
        return $request->session()->get('userEmail', 'default');
    }
```
## session()->flash()
This session only exist until next request. Than it will be deleted. The request could be in any route, the session will be deleted on next request.
```php
function sessionFlash(Request $request) {
	$request->session()->flash('msg', 'This is a flash message');
	return response("The flash session has been set");
}
```
You can set the flash session by **with()** function also and redirect to a route
```php
function setAndRedirect(Request $request) {
	return redirect('/flash')->with('message', 'Something wrong');
}
```
## session()->pull()
To get the session data only one time
```php
function sessionPull(Request $request):string
    {
        return $request->session()->pull('userEmail', 'default');
    }
```
## session()->forget()
To remove a single key of session data
```php
function sessionForget(Request $request):bool
    {
        $request->session()->forget('userEmail');
        return true;
    }
```
## session()->flush()
To remove all session data()
```php
 function sessionFlush(Request $request):bool
    {
        $request->session()->flush();
        return true;
    }
```