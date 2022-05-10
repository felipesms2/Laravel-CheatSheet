# Laravel-CheatSheet
Some additional features
#choose version

composer create-project laravel/laravel="5.1.*" myProject


<br>

php artisan make:model table --all

#sqlite support

DB_CONNECTION=sqlite
DB_DATABASE=/absolute/path/to/database.sqlite


composer require doctrine/dbal

#user interface

https://github.com/laravel/ui
composer require laravel/ui
php artisan ui bootstrap



https://butlerraines.com/code-stuff/creating-laravel-project-scratch-my-local-machine

<br>
Factory
php artisan tinker <br>
User::factory()->count(3)->make() <br>
User::factory()->times(5)->create();
