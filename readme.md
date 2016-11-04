<p align="center"><a href="https://laravel.com" target="_blank"><img width="150"src="https://laravel.com/laravel.png"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

## License

The Laravel framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

## How use
```
git clone https://github.com/IvanBohonosiuk/start.dev.git
```

Next use this command

```
composer install
```
Rename `.env.example` to `.env` and next make sure to create a new database and add your database credentials to your `.env` file:

```
DB_HOST=localhost
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```
and nex step
```
npm install
npm install hammerjs vue-async-data materialize-css
gulp
php artisan voyager:install
```
and change you file `resources/views/layouts/app.blade.php` on 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- CSRF Token -->
    <meta name="csrf-token" content="{{ csrf_token() }}">

    <title>{{ config('app.name', 'Laravel') }}</title>

    <!--Import Google Icon Font-->
    <link href="http://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <!-- Styles -->
    {{--<link href="/css/app.css" rel="stylesheet">--}}
    <link href="{{ elixir('css/app.css') }}" rel="stylesheet">
    @yield('styles')

    <!-- Scripts -->
    <script>
        window.Laravel = <?php echo json_encode([
            'csrfToken' => csrf_token(),
        ]); ?>
    </script>
</head>
<body>
    <div id="app">
        <nav>
            <div class="nav-wrapper">
                <div class="container">
                    <a href="{{ url('/') }}" class="brand-logo center">@if (Voyager::setting('logo') != '') <img src="/storage/{{ Voyager::setting('logo') }}"> @endif <span>{{ Voyager::setting('title') }}</span></a>
                    <ul id="nav-mobile" class="right hide-on-med-and-down">
                        @if (Auth::guest())
                            <li><a href="{{ url('/login') }}">Login</a></li>
                            <li><a href="{{ url('/register') }}">Register</a></li>
                        @else
                            <li>
                                <a class="dropdown-button" href="#" data-activates="dropdown1">
                                    <img src="/storage/{{ Auth::user()->avatar }}" class="responsive-img circle" style="width: 35px; position: relative; top: 12px;"> <span>{{ Auth::user()->name }}</span>
                                    <i class="material-icons right">arrow_drop_down</i>
                                </a>
                            </li>
                            <!-- Dropdown Structure -->
                            <ul id="dropdown1" class="dropdown-content">
                                <?php $user = TCG\Voyager\Models\User::find(Auth::user()->id); ?>
                                
                                @if($user->hasRole('admin'))
                                    <li>
                                        <a href="{{ url('/admin') }}">
                                            Admin
                                        </a>
                                    </li>
                                @endif
                                <li>
                                    <a href="{{ url('/logout') }}"
                                       onclick="event.preventDefault();
                                           document.getElementById('logout-form').submit();">
                                        Logout
                                    </a>
                                </li>
                                <form id="logout-form" action="{{ url('/logout') }}" method="POST" style="display: none;">
                                    {{ csrf_field() }}
                                </form>
                            </ul>
                        @endif
                    </ul>
                    <ul class="left hide-on-med-and-down">{!! Menu::display('main') !!}</ul>
                </div>
            </div>
        </nav>
        <div class="container">
            @yield('content')
        </div>
    </div>

    <!-- Scripts -->
    {{--<script src="/js/app.js"></script>--}}
    <script src="{{ elixir('js/app.js') }}"></script>
    @yield('scripts')
</body>
</html>
```

And we're all good to go!

Login in admin
```
**email:** admin@admin.com
**password:** password
```
