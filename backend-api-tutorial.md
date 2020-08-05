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

## Install 'app/Providers/AuthServiceProvider'

```
// app/Providers/AuthServiceProvider.php

<?php

namespace App\Providers;

use Illuminate\Foundation\Support\Providers\AuthServiceProvider as ServiceProvider;
use Illuminate\Support\Facades\Gate;
use Laravel\Passport\Passport; // add this 

class AuthServiceProvider extends ServiceProvider
{
    /**
     * The policy mappings for the application.
     *
     * @var array
     */
    protected $policies = [
         'App\Model' => 'App\Policies\ModelPolicy', // uncomment this line
    ];

    /**
     * Register any authentication / authorization services.
     *
     * @return void
     */
    public function boot()
    {
        $this->registerPolicies();

        Passport::routes(); // Add this
    }
}
```

## Setting Driver for Token Guard in 'config/auth'

```
// config/auth

<?php

return [
    ...

    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

        'api' => [
            'driver' => 'passport', // set this to passport
            'provider' => 'users',
            'hash' => false,
        ],
    ],

    ...
];
```



