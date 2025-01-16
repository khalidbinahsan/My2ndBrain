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
### Unions
The **union** method takes two arguments, the first argument is the first query and the second arguments is the second query. Then that return the result together.

```php
 function demoAction() {
        $query1 = DB::table('products')->where('price', '=', 580);
        $query2 = DB::table('products')->where('category_id', '=', 35)->union($query1)->get();
        return $query2;
    }
```
Note: You must make the query from same table.
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

## Uses ->where
```php
function demoAction() {
        $products = DB::table('products')
        ->where('price', '<', 200)
        ->get();
        return $products;
    }
```
The where operator
=, !=, <, <=, >, >=, LIKE(contains), NOT LIKE(does not contain), IN(is in the list), NOT IN(is not in the list)
You can use the `whereIN` directly
```php
function demoAction() {
        $products = DB::table('products')
        ->whereIn('price', [20, 5000])
        ->get();
        return $products;
    }
```
You can see the all where clauses from here [Laravel where clauses](https://laravel.com/docs/11.x/queries#basic-where-clauses)
## orderBy - asc desc
```php
function demoAction() {
        $products = DB::table('products')
        ->orderBy('id', 'desc')
        ->get();
        return $products;
   }
```
## orderBy -  inRandomOrder()
```php
function demoAction() {
        $products = DB::table('products')
        ->inRandomOrder()
        ->get();
        return $products;
    }
```
## first()
To get the only the first row
```php
 function demoAction() {
        $products = DB::table('products')->first();
        return $products;
    }
```
Note: No need to call `->get()` function here.
## latest()
To get the last inserted data 
```php
function demoAction() {
        $products = DB::table('products')->latest()->first();
        return $products;
    }
```
## oldest()
To get the first inserted data
```php
function demoAction() {
        $products = DB::table('products')->oldest()->first();
        return $products;
    }
```
## skip() take()
We can define how many row we want to skip and how many row we want to take. Let's see
```php
function demoAction() {
        $products = DB::table('products')
        ->skip(2)
        ->take(4)
        ->get();
        return $products;
    }
```
## groupBy()
We can make a group by the table name
```php
function demoAction() {
        $products = DB::table('products')
        ->groupBy('price')
        ->get();
        return $products;
    }
```
Note: You must make false the strict mode from `config->database.php` to avoid the error

You can give condition here with **having()** function
```php
function demoAction() {
        $products = DB::table('products')
        ->groupBy('price')
        ->having('price', '>', 200)
        ->get();
        return $products;
    }
```
## insert()
To insert data to Database
```php
function demoAction(Request $request) {
        $products = DB::table('brands')
        ->insert($request->input());
        return $products;
    }
```
Or you can insert by a associative array
```php
function demoAction(Request $request) {
        $name = $request->input('brand_name');
        $img = $request->input('brand_img');
        $brand = DB::table('brands')->insert([
            'brand_name'=>$name,
            'brand_img'=>$img
        ]);
        return $brand;
    }
```
### update()
```php
function dataInsert(Request $request){
        $products = DB::table('products')
        ->where('id', '=', $request->id)
        ->update(['price' => 2500]);
        return $products;
    }
```
### updateOrInsert()
If the criteria match then it will update otherwise insert
```php
function dataInsert(Request $request){
        $products = DB::table('brands')
        ->updateOrInsert(
            ['brand_name'=> $request->brandName],
	        $request->input());
        return $products;
    }
```
### Increment & Decrement
```php
function dataInsert(Request $request){
        $products = DB::table('products')
        ->where('id', '=', $request->id)
        ->increment('price');
        // ->increment('price', 20);
        // ->decrement('price');
        // ->decrement('price', 10);
        return $products;
    }
```
### Delete a row
```php
function dataInsert(Request $request){
        $products = DB::table('brands')
        ->where('id', '=', $request->id)
        ->delete();
        return $products;
    }
```
### Delete a table
```php
function dataInsert(Request $request){
        $deleted = DB::table('users')->truncate();
        return $deleted;
    }
```