# Hello World

Untuk menjalankan hello world pada laravel, mudahnya dibuatkan satu controller untuk men-create tampilan text hello world.

## Create Controller

Membuat controller secara mudah pada package "App/Http/Controller"

```php
<?php

namespace Http\Controllers;

use Illuminate\Routing\Controller;

class TestController extends Controller
{
    public function index(){
        echo "hello world";
    }
}
```

## Define Route

Untuk menjalankan Controller yang sudah definisikan sebelumnya perlu di tambahkan pada Route, lebih tepatnya pada directory "Route/web.php" seperti berikut :

```php
<?php
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/


use Illuminate\Support\Facades\Route;

Route::get('/hello', function(){
    return "hello world php laravel";    
});
```

## Access web URL 

```
http://localhost:8000/index.php/hello
```



