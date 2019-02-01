# Eloquent ORM

# Introduction

Eloquent ORM disertakan oleh Laravel untuk menyediakan implementasi ActiveRecord yang indah dan sederhana untuk bekerja dengan Database. Setiap tabel database memiliki "Model" yang sesuai yang digunakan untuk berinteraksi dengan tabel tersebut. Model akan menyediakan query data dalam tabel, serta INSERT data baru ke dalam tabel.

untuk melakukan Eloquent ini pastikan bahwa konfigurasi database sudah benar dan tidak terjadi kesalahan pada "config/database.php"

## Defining Models

Model biasanya dilakukan pada "app" diretory, tapi bisa saja kita memberikan templat yang lain dan memberikan konfigurasi untuk menload otomatis directory tersebut di dalam "compose.json" file, semua Eloquent models adalah extends _Illuminate\Database\Eloquent\Model _

```
php artisan make:model Flight
```

## Eloquent Model Conventions

Setelah selesai mengerjakan script diatas kurang lebihnya akan terbentuk class Flight seperti berikut : 

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Flight extends Model
{
    //
}
```



