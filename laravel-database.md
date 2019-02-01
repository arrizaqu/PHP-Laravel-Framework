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



