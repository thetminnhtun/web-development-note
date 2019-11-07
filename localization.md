# Localization

### Step 1

Create 2 files for languages — English and Myanmar
```
resources/lang/en/lang.php
resources/lang/my/lang.php
```
Write down below code in `resources/lang/en/lang.php`

```php
<?php

return [
    'message' => 'Hello World',
    'greeting' => 'How are you?',
];
```
Write down below code in `resources/lang/my/lang.php`

```php
<?php

return [
    'message' => 'မင်္ဂလာပါ',
    'greeting' => 'နေကောင်းလား',
];
```

### Step 2

Create a new controller `LocalizationController` by using the following command
```
 php artisan make:controller LocalizationController
```

### Step 3

Add index method of `LocalizationController` class as below code in `app/Http/LocalizationController.php`
```php
public function index($lang)
{
    Session::put('locale', $lang);
    return back();
}
```

### Step 4

Create Route to switch lanaguage
```php
Route::get('localization/{locale}','LocalizationController@index');
```

### Step 5

Create `LangWare` by using the following command

```
php artisan make:middleware LangWare
```

And write down below code to change Session get language to every route

```php
public function handle($request, Closure $next)
{
    if( App::setLocale( Session::get('locale') );
    } else {
    App::setLocale( Config::get('app.fallback_locale') );
    }
    return $next($request);
}
```

Add middleware to Kernel Middleware Group

```php
protected $middlewareGroups = [
'web' => [
    ...
    \App\Http\Middleware\LangWare::class,
],
```
### Step 5

Create Language Dropdown

```html
<li class="nav-item dropdown">
    <a class="nav-link dropdown-toggle" href="#" role="button" data-toggle="dropdown"> 
        language
    </a>
    <div class="dropdown-menu">
        <a class="dropdown-item" href="{{ url('localization/en') }}"> English </a>
        <a class="dropdown-item" href="{{ url('localization/my') }}"> Myanmar </a>
    </div>
</li>
```

### Step 6

Retrieving Translation Strings

```php
echo __('lang.message');
echo __('lang.greeting');
```
or
```php
{{ __('lang.message') }}
@lang('lang.message')
```
