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
User::factory()->times(5)->create(); <br>


php artisan make:seeder RoleUserSeeder

user seeder bring model to class: <br>

 1 use App\Models\User;
 2 put method create factory on run method <br>
 
        //Inside databaseseeder to run individually
        $this->call(UserSeeder::class);
        $this->call(RoleSeeder::class);
        php artisan db:seed --class=RoleSeeder /*Call individually* / 
        php artisan migrate:refresh --seed /*Reset and migrate*/
        //run php artisan db:seed
        

