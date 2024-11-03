You can manage the Laravel default Middleware and can stop the CSRF validation in the development phase.  To stop the CSRF and this code in `bootstrap/app.php` file.
```php
->withMiddleware(function (Middleware $middleware) {
		$middleware->validateCsrfTokens(except: ['*']);
    })
```