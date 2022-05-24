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


https://stackoverflow.com/questions/63807930/target-class-controller-does-not-exist-laravel-8
To call a view inside index class controller

https://butlerraines.com/code-stuff/creating-laravel-project-scratch-my-local-machine

<br>
Factory

    public function definition()
    {
        return [
            "name" => $this->faker->jobTitle
        ];
        
        // in <Model>factory.php to chose field data from faker
    }
    
    


static values for faker in table roles 

/*

use Illuminate\Support\Facades\DB;
        DB::table('roles')->insert(
            [
                "name" =>  "Admin"
            ]
            );
           
           next value only change name
           or use //Role::factory()->times(10)->create(); to create random values

*/

php artisan tinker <br>
User::factory()->count(3)->make() <br>
User::factory()->times(5)->create(); <br>


php artisan make:seeder RoleUserSeeder //Creating a new seeder

user seeder bring model to class: <br>

 1 use App\Models\User;
 2 put method create factory on run method <br>
 
        //Inside databaseseeder to run individually
        $this->call(UserSeeder::class);
        $this->call(RoleSeeder::class);
        php artisan db:seed --class=RoleSeeder /*Call individually* / 
        php artisan migrate:refresh --seed /*Reset and migrate*/
   
        //run php artisan db:seed
        
 https://www.youtube.com/watch?v=vbgcpuEErhY&list=PLxFwlLOncxFLxT3ZxYPw7-hCrXhdZHg1W&index=5

# to make controller subfolder 

 php artisan make:controller Admin\\UserController -r
index function
     public function index()
    {
        dd('test');
    }

After put namespace on web.php routes 
    use App\Http\Controllers\Admin\UserController;
Then call the route

    Route::resource('/admin/users', UserController::class); 

# Grouping and prefixing a route name

Route::prefix('admin')->name('admin.')->group(function(){
    Route::resource('/users', UserController::class);
});

# Pagination 

Change return view('admin.users.index', ["users"=> User::all()]); to 

return view('admin.users.index', ["users"=> User::paginate(10)]);

on table view, above </table> (end tag)
{{$users->links()}}

AppServiceProvider.php to styling

add namespace 
    use Illuminate\Pagination\Paginator;

    public function boot()
    {
        Paginator::useBootstrap();
    }


