    # Laravel-CheatSheet
Some additional features
# choose version

composer create-project laravel/laravel="5.1.*" myProject

# Breeze
composer require laravel/breeze --dev && php artisan breeze:install  && npm install && npm run build && php artisan migrate

<br>

# ShortCurt
<br>

sudo wget https://raw.githubusercontent.com/felipesms2/Laravel-CheatSheet/main/cli-shortcurt -P /usr/bin 
&& sudo mv /usr/bin/cli-shortcurt /usr/bin/lv
&& sudo chmod +x /usr/bin/lv

php artisan make:model table --all
<br>
#sqlite support
<br>
DB_CONNECTION=sqlite<br>

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
App\Models\User::factory()->count(1)->create()<br>
App\Models\Secret::factory()->create(['user_id' => 2]) /*Here is to override some hardcoded*/ <br>;
User::with('secrets')->get(); <br>



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
https://stackoverflow.com/questions/63807930/target-class-controller-does-not-exist-laravel-8

php artisan make:request StoreUserRequest  to create a new validate in a separated file

# Gate
        File >> app/Providers/AuthServiceProvider.php;

            $this->registerPolicies();  
        Gate::define('logged-in', function($user){
            return $user;
        });

        Index Method Controller >> 
          if (Gate::denies('logged-in')) {
             dd('Access Denied');
        }


# Must Veriy email

https://larainfo.com/blogs/laravel-8-email-verification-with-laravel-ui

# Route api prefix

Route::group(['prefix' =>"v1", 'namespace' => 'App\Http\Controllers\Api\V1'], function()
{
    Route::apiResource('customers', CustomerController::class);
    Route::apiResource('invoices', InvoiceController::class);
});


# Migrations and changes in schema


# storage without SSH

Artisan::call('storage:link');
$table->string('name', 100)->change(); // to change the column data 
php artisan make:migration add_name_field_table_name --table=users  #make migration change
$table->dropColumn('image'); // drop some column on function down
<br>
## Here the relationship
$table->foreign('user_id')
->references('id')
->on('users')
->onDelete('cascade');

# Function Controller from Tinker

$controller = app('App\Http\Controllers\MyController');

#changes to existing database

	#create migrations
		php artisan make:migration add_columns_to_users_table --table=users
	#add column
		$table->string('username', 50)->nullable()->after('email');
		$table->boolean('have_skill')->default(null)->after('username');

# Database Seeder


php artisan make:seeder UserSeeder

1 put model into seeder in user case for example

php artisan make:seeder UserSeeder

2 in run function call the factory
	#Option 1
	User::factory()->times(10)->create();
	
	#Option 2
	

3 In database seeder post the seeders which have to call during db--seed;
	#Call Seeder into database without run migrate
	php artisan db:seed

	#Migrate with seed

	php artisan migrate:refresh --seed

	
