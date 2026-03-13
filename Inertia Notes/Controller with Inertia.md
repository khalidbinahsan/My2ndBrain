This is an example of Inertia Controller
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use Inertia\Inertia;
use Illuminate\Support\Facades\Http;

class HomeController extends Controller
{
    function hello(Request $request) {
        $name = "Khalid Batch 4";
        return Inertia::render('Home/Hello', [
            'name' => $name,
            'posts' => $this->getPost()
        ]);
    }
    function greet(Request $request) {
        return Inertia::render('Home/Great');
    }
    private function getPost() {
        $response = Http::get('https://jsonplaceholder.typicode.com/posts');
        return $response->json();
    }
}

```