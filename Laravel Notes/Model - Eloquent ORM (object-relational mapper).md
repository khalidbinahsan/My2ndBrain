This is simple overview of a model
```php
class Brand extends Model
{
    protected $fillable =['brandName', 'brandImg'];
}
```
### create()
Now you can make a operation from your controller like this
```php
function createBrand(Request $request){
      return  Brand::create($request->input());
    }
```
Note: To get the full advantage of Eloquent ORM, you must keep the Model name Singular while the Database table name is plural
### update()
```php
function updateBrand(Request $request){
        return Brand::where('id', $request->id)->update($request->input());
    }
```
### updateOrCreate()
If the data can find it will update. If not, it will create a new data
```php
function updateBrand(Request $request){
        return Brand::updateOrCreate(
            ['brandName' => $request->name],
            $request->input()
        );
    }
```
Route is like this
```php
Route::post('/update-brand/{name}', [TestController::class, 'createBrand']);
```
### delete()
Delete is very simple
```php
function createBrand(Request $request){
        return Brand::where('id', $request->id)->delete();
    }
```
### select()
To get the specific column
```php
function getProducts(Request $request){
        return Product::select('title', 'price', 'star')->get();
    }
```
Note: You must call the get() function here.
### distinct()
To get the unique value of column
```php
function getProducts(Request $request){
        return Product::select('title')->distinct()->get(); 
    }
```
### where()
To set the condition
```php
function getProducts(Request $request){
        return Product::where('price', '=', 573)->get();
    }
```
You can also use the operator like =, <, >, LIKE, NOT LIKE, IN, NOT IN
## Advance where clauses
### whereBetween
```php
function getProducts(Request $request){
        return Product::whereBetween('price', [1, 400])->get();
    }
```
In the example above the whereBetween clauses take the data from 1-400 of price.
### whereNotBetween
It will do the reverse things of whereBetween
```php
function getProducts(Request $request){
        return Product::whereNotBetween('price', [1, 400])->get();
    }
```
To see more advance where clauses go to [Laravel where clauses](https://laravel.com/docs/11.x/queries#basic-where-clauses)
### increment()
```php
function createBrand(Request $request){
        return Product::where('id', $request->id)->increment('price');
    }
```
You can put the increment number here
```php
function createBrand(Request $request){
        return Product::where('id', $request->id)->increment('price', 10);
    }
```
### decrement()
You can do the same things for decrement as well
```php
function createBrand(Request $request){
        return Product::where('id', $request->id)->decrement('price');
    }
```
### get()
You can retrieve all date with get()
```php
function getProduct(Request $request){
        return Product::get();
    }
```
Note: The route must should be get here.
### all()
You can do the same things as like as get()
```php
function getProduct(Request $request){
        return Product::all();
    }
```
### first()
To get the first row of database
```php
 function createBrand(Request $request){
        return Product::first();
    }
```
### find()
To get the specific row of database
```php
function createBrand(Request $request){
        return Product::find(8);
    }
```
### pluck()
To get the specific column data
```php
function getProducts(Request $request){
        return Product::pluck('title', 'price');
    }
```
### orderBy()
To get data asc or desc order
```php
 function getProducts(Request $request){
        return Product::orderBy('price', 'desc')->get();
    }
```
### inRandomOrder()
To get the data by random order
```php
function getProducts(Request $request){
        return Product::inRandomOrder()->get();
    }
```
### latest()
To get the last inserted data
```php
function getProducts(Request $request){
        return Product::latest()->first();
    }
```
### oldest()
To get the first inserted data
```php
function getProducts(Request $request){
        return Product::oldest()->first();
    }
```
### groupBy
To get the data by it's group
```php
 function getProducts(Request $request){
        return Product::groupBy('price')->get();
    }
```
Note: You must make false the strict mode from config/database.php
### having()
You can add extra layer of condition in the groupBy you need to use having()
```php
 function getProducts(Request $request){
        return Product::groupBy('price')
        ->having('price', '>', 2000)->get();
    }
```
### skip() take()
To how many row you want to skip and take
```php
function getProducts(Request $request){
        return Product::skip(5)->take(1)->get();
    }
```
### simplePaginate()
To paginate the data
```php
function getProducts(Request $request){
        return Product::simplePaginate(5);
    }
```
Note: Your 2nd page url should be like this http://127.0.0.1:8000/api/products?page=2
You can also use just **paginate()**
## Aggregates
### count()
To count the row number
```php
function getProducts(Request $request){
        return Product::count();
    }
```
### sum()
To the sum column value
```php
function getProducts(Request $request){
        return Product::sum('price');
    }
```
### avg()
To calculate the average of the total number
```php
function getProducts(Request $request){
        return Product::avg('price');
    }
```
### max()
To get the maximum number
```php
function getProducts(Request $request){
        return Product::max('price');
    }
```
### min
To get the minimum number
```php
function getProducts(Request $request){
        return Product::min('price');
    }
```
## Eloquent Relationship
There are two relationship method on Eloquent ORM
1. Has Relationship - To create the relation from parent to child table
2. Belongs Relationship - To create the relation from child to parent table
### One to One relation
In this case you need to create a function with **hasOne()** in you parent Model. Suppose we are working for User Model and it has a Profile Model. The function should be like this
User model:
```php
function profile(){
       return $this->hasOne(Profile::class);
    }
```
Now in you controller the query should be like this
```php
function getUser(Request $request){
        return User::with('profile')->get();
    }
```
Here is **User** is the parent Model and Called the **profile** function using **with()** function. 
Now Let's see how it should be from **profile** end
Profile model:
```php
function user(){
        return $this->belongsTo(User::class);
    }
```
Controller:
```php
function getUser(Request $request){
        return Profile::with('user')->get();
    }
```
Note: Need to use **belongsTo()** function when we get data from child table
### One to Many relation
We need to use the **hasMany()** function instead of **hasOne()** to build a One to Many ralationship
Parent Model:
```php
function review(){
        return $this->hasMany(ProductReview::class);
    }
```
Controller:
```php
function getReviews(Request $request){
        return User::with('profile')->with(relations: 'review')->get();
    }
```
Let's see how should be from the child model
child Model:
```php
function user(){
	       return $this->belongsTo(User::class);
    }
```
Controller:
```php
function getProducts(Request $request){
        return ProductReview::with('user')->get();
    }
```
## Many to Many
Suppose we have the **Product** table and want to make the relation with **tags** table. The mysql dosen't allow the Many to Many relation directly. We need a helper table in this case that's name is pivot table. 
Go to the **Product** model and and make the relation with **Tag** model
```php
function tag(){
        return $this->belongsToMany(Tag::class, 'product_tags');
    }
```
Now go to the **Tag** model and make the relationship with **Product** model
```php
function product(){
        return $this->belongsToMany(Product::class, 'product_tags');
    }
```
let's return with controller
```php
function getProducts(Request $request){
        return Tag::with('product')->get();
    }
```