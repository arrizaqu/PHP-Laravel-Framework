# Laravel Database

Laravel membuat interaksi dengan database menjadi sangat sederhana diberbagai jenis basis data menggunakan raw sql, baik menggunakan query builder dan ORM Eloquent, kemudia untuk ini maka laravel secara default support terhadap 4 database, diantaranya :

1. Mysql
2. PostgresSQL
3. SQLite
4. SQLServer

## Configurasi

File database konfigurasi dalam laravel terletak pada "config/database.php", bisa saja pada file config ini, akan mendefinisikan semua database connection, serta dapat menentukan koneksi database manakah yang akan dijadikan sebagai default.

## Read & Write Connections

Mungkin saja kita menginginkan menggunakan 1 koneksi database untuk keperluan menampilkan data, namun seperti INSERT, UPDATE, DELETE untuk kerperluan yang berbeda, untuk menangani hal ini maka laravel dapat memisahkan konfigurasi untuk READ and WRITE sebagai berikut:

```php
'mysql' => [
    'read' => [
        'host' => ['192.168.1.1'],
    ],
    'write' => [
        'host' => ['196.168.1.2'],
    ],
    'sticky'    => true,
    'driver'    => 'mysql',
    'database'  => 'database',
    'username'  => 'root',
    'password'  => '',
    'charset'   => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix'    => '',
],
```

## Multiple Database Connections

Saat menggunakan beberapa koneksi, Anda dapat mengakses setiap koneksi melalui metode koneksi, Nama database akan menjadi salah satu koneksi yang terdaftar di file konfigurasi "config / database.php" :

```php
$users = DB::connection('foo')->select(...);
```

bisa juga menggunakan PDO sebagai database koneksi sebagai berikut :

```php
$pdo = DB::connection()->getPdo();
```

## Raw SQL Query

Setelah mengonfigurasi koneksi database kita, maka kita dapat menjalankan query menggunakan DB. DB menyediakan metode untuk setiap jenis query seperti: SELECT, UPDATE, INSERT, DELETE, dan STATEMENT.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Support\Facades\DB;
use App\Http\Controllers\Controller;

class UserController extends Controller
{
    /**
     * Show a list of all of the application's users.
     *
     * @return Response
     */
    public function index()
    {
        $users = DB::select('select * from users where active = ?', [1]);

        return view('user.index', ['users' => $users]);
    }
}
```

## Using Named Bindings

Tanda dari ? akan mewakili proses binding parameter, seperti contoh berikut :

```php
$results = DB::select('select * from users where id = :id', ['id' => 1]);
```

### Insert

```php
DB::insert('insert into users (id, name) values (?, ?)', [1, 'Dayle']);
```

### Update

```php
$affected = DB::update('update users set votes = 100 where name = ?', ['John']);
```

### Delete

```php
$deleted = DB::delete('delete from users');
```

## Running A General Statement

Untuk menggunakan Query secara general, maka bisa dilakukan sebagai berikut :

```php
DB::statement('drop table users');
```

### Listening For Query Events

Terkadang kita menginginkan sebuah event listener pada saat menjalankan query berlangsung hal ini mungkin saja atau  beberapa script untuk keperluan testing, atau melihat proses binding dan checking pada saat laravel menggunakan aktivitas query, untuk hal itu kita bisa melakukan pada "boot" di Service Provider, sebagai berikut :

```php
<?php

namespace App\Providers;

use Illuminate\Support\Facades\DB;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        DB::listen(function ($query) {
            // $query->sql
            // $query->bindings
            // $query->time
        });
    }

    /**
     * Register the service provider.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}
```

## Database Transaction

Dalam menggunakan metode transaksi perlu menjalankan serangkaian operasi tertentu sehingga secara otomatis akan dibatalkan jika salah satu proses tidak berkerja atau terjadi kegagalan, berikut ini adalah contoh potongan script laravel melakukan tugas tersebut :

```php
DB::transaction(function () {
    DB::table('users')->update(['votes' => 1]);

    DB::table('posts')->delete();
});
```

### Handling Deadlocks

_Deadlock \_adalah jalan buntu yang dapat terjadi ketika dua atau lebih transaksi masing-masing menunggu lock yang sedang dipegang oleh transaksi lainnya untuk dilepas. Hanya ada satu cara untuk menghancurkan  \_deadlock_, yaitu _abort_

```php
DB::transaction(function () {
    DB::table('users')->update(['votes' => 1]);

    DB::table('posts')->delete();
}, 5);
```

### Manually Using Transactions

Pada aplikasi nya laravel men-support jika memungkinkan untuk mode transaksi dibuatkan sebagai manual, seperti code berikut ini : 

```php
DB::beginTransaction();
```

code rollback 

```php
DB::beginTransaction();
```

code commit transaction jika dianggap proses sempurna dilakukan

```php
DB::beginTransaction();
```



