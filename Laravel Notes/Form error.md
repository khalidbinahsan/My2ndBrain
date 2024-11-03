You can use the @error() function to handle the form error 
```php
<input type="text" name="name">
@error('name')  
<div class="text-red-500">{{ $message }}</div>  
@enderror
```
## old()
If you want to keep the old value and don't want to be empty your field, while submit the form and getting error.
```php
<input type="text" name="name" value="{{ old('name') }}">
@error('name')  
<div class="text-red-500">{{ $message }}</div>  
@enderror
```