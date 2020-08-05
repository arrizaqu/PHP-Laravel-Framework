# Create Login API

## Install Laravel APP

```
> laravel new app_api
```

## Install Laravel Passport

```
> composer require laravel/passport
> php artisan migrate
> php artisan passport:install
```

## Install HasApiToken

```
// app/User.php

<?php

namespace App;

...
use Laravel\Passport\HasApiTokens; // include this

class User extends Authenticatable
{
    use Notifiable, HasApiTokens; // update this line

    ...
}
```



