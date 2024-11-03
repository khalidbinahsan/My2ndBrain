## @foreach in Laravel blade template
```php
@foreach($learnerKey as $learner)  
    <li>First name: {{$learner['fname']}} Last name: {{$learner['lname']}}</li>  
@endforeach
```
## @for loop in Laravel blade template
```php
@for($i = 0; $i < 100; $i++)  
    <span>Item Number is: {{$i}}</span><br>  
@endfor
```
## @php code in Laravel blade template
```php
@php  
$num1 = 20;  
$num2 = 30;  
echo $num1 + $num2;  
@endphp
```
## Add Subview through @include()
```php
@include('component.testimonial')  
@include('component.contact')  
@include('component.hero')
```
## @if @else in Laravel blade
```php
@php  
$marks = 60;  
@endphp  
@if($marks <= 100 && $marks >= 80)  
    <h3>You got A+</h3>  
    @elseif($marks <= 80 && $marks >= 60)  
    <h3>You got A-</h3>  
@endif
```
##  @switch @case @break @default and @endswitch
```php
@php 
	$value = 75000; // Example value 
@endphp
@switch($value)
    @case(100)
        <h1>The result is hundred</h1>
        @break
    @case(1000)
        <h1>The result is Thousand</h1>
        @break
    @case(100000)
         <h1>The result is lack</h1>
        @break
    @default
        <h1>The result is not in our range</h1>
@endswitch
```
## Add static url with **asset()**
```php
<img src="{{asset('https://your-file-url')}}">
```
## Add Url in anchore tag with **route()**
```php
<a href="{{route('home')}}">Home</a>
```
Add the **name()** end of your route
```php
Route::get('/', function(){  
    return view('site.home');  
})->name('home');
```
## Laravel Dynamic layout with @yield() @section() @extends
We used the **@yield()** to get the content from other page
```php
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>@yield('title')</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
	@yield('content')
</body>
</html>
```
 You must **@extends()** the master layout first.
```php
@extends('layout')
@section('title')
Home
@endsection

@section('content')
<h1>This is Home Page</h1>
@endsection
```
## @parent()
If you want to keep the master layout content and want to add the additional content over there, you can use the @parent() blade function

## @push() @stack()
With the @push() function, you can add the js script in your layout body. 
First of all you need to use the @stack() function in master layout
```php
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>@yield('title')</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
	@yield('content')
</body>
@stack('scripts')
</html>
```
Then add the @push function in the page content
```php
@extends('layout')
@section('title')
Home
@endsection

@section('content')
<h1>This is Home Page</h1>
@endsection
@push('scripts')
<script>
	alert ('Hello world');
</script>
@endpush
```
## @error('name')
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