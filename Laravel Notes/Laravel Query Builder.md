Need to import the BD class first
```php
use Illuminate\Support\Facades\DB;
```
### Get all data
To get all data use **get()** method
```php
function demoAction() {
        $products = DB::table('products')->get();
        return $products;
    }
```
### Get the first row
To get only the first row use **first()** method
```php
function demoAction() {
        $products = DB::table('products')->first();
        return $products;
    }
```
### Get a single row
To get a single row use **find()** method
```php
function demoAction() {
        $products = DB::table('products')->find(1);
        return $products;
    }
```
### Get the single column data
To get all data from single column use **pluck()** method
```php
function demoAction() {
        $price = DB::table('products')->pluck('price');
        return $price;
    }
```
You can set  the key also here
```php
function demoAction() {
        $products = DB::table('products')->pluck('price', 'id');
        return $products;
    }
```
### Get the specific column
You can get the specific column with the **select()** method
```php
 function demoAction() {
        $products = DB::table('products')->select('name', 'price')->get();
        return $products;
    }
```
## Get unique data from column
To get the unique data you can use 
```php
function demoAction() {
        $products = DB::table('products')->select('name')->distinct()->get();
        return $products;
    }
```
## Join Table
### Inner Join
```php
function demoAction() {
        $products = DB::table('products')
        ->join('users', 'products.user_id', '=', 'users.id')
        ->join('categories', 'products.category_id', '=', 'categories.id')
        ->get();
        return $products;
    }
```
### Left Join
```php
function demoAction() {
        $products = DB::table('products')
        ->leftJoin('users', 'products.user_id', '=', 'users.id')
        ->leftJoin('categories', 'products.category_id', '=', 'categories.id')
        ->get();
        return $products;
    }
```
### Right Join
```php
function demoAction() {
        $products = DB::table('products')
        ->rightJoin('users', 'products.user_id', '=', 'users.id')
        ->rightJoin('categories', 'products.category_id', '=', 'categories.id')
        ->get();
        return $products;
    }
```
### Cross Join
Cross Join is make the possible combination of it's table
```php
 function demoAction() {
        $products = DB::table('products')
        ->crossJoin('categories')
        ->get();
        return $products;
    }
```
### Advanced Join Clauses
You can make the join by applying some condition
```php
function demoAction() {
        $products = DB::table('products')
        ->join('categories', function(JoinClause $join){
            $join->on('products.category_id', '=', 'categories.id')
            ->where('products.price', '>', 200);
        })
        ->join('brands', function(JoinClause $join){
            $join->on('products.brand_id', '=', 'brand_id')
            ->where('brands.brand_name', '=', 'Hatil');
        })
        ->get();
        return $products;
    }
```

## Query Math
### count()
You can count the row of the table
```php
function demoAction() {
        $total = DB::table('products')->count();
        return $total;
    }
```
### max()
You can get max value with this method
```php
function demoAction() {
        $price = DB::table('products')->max('price');
        return $price;
    }
```
### min()
You can get min value with this method
```php
function demoAction() {
        $price = DB::table('products')->min('price');
        return $price;
    }
```
### avg()
You can get the average value with this method
```php
function demoAction() {
        $price = DB::table('products')->avg('price');
        return $price;
    }
```
### sum()
You can get the sum value of a column
```php
function demoAction() {
        $price = DB::table('products')->sum('price');
        return $price;
    }
```