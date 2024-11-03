```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Cookie;

class ProfileController extends Controller
{
    public function index($id)
    {
        // Declare the variables
        $name = "Donald Trump";
        $age = "75";

        // Store data in an associative array
        $data = [
            'id' => $id,
            'name' => $name,
            'age' => $age
        ];

        // Create a cookie
        $cookie = cookie(
            'access_token',    // cookie name
            '123-XYZ',         // value
            1,                 // minutes
            '/',               // path
            $_SERVER['SERVER_NAME'], // domain
            false,             // secure
            true               // httpOnly
        );

        // Return the response with status code 200 and the cookie
        return response()->json($data, 200)->cookie($cookie);
    }
}

```