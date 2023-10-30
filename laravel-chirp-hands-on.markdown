## Models, Migration and Controller
There are some concept between these three:
* [Model](https://laravel.com/docs/eloquent) provide a powerful and enjoyable interface for you to interact with the tables in your database.
* [Migration](https://laravel.com/docs/migrations) allows you to easily create and modify the tables in your database. They ensure that the same database structure exist everywhere that your application runs.
* [Controllers](https://laravel.com/docs/controllers) are responsible for processing request made to your apps and returning a response.

The method 
```php
php artisan make:model -mrc Chrip
```
will create a model, migration, and resource controller for Chrip projec.
1. `app/Models/Chirp.php` - The Eloquent model.
2. `database/migrations/<timestamp>_create_chirps_table.php` - The database migration that will create your database table.
3. `app/Http/Controller/ChirpController.php` - The HTTP controller that will take incoming requests and return responses.

### Routing
---
```markdown
Common Resource Routes:
// index - Show all listings
// show - Show single listing
// create - Show form to create new listing
// store - Store new listing
// edit - Show form to edit listing
// update - Update listing
// destroy - Delete listing  
```

We will also create an URLs to our controller. To start with, we are going to enable to routes
* The `index` route will display our form and a listing of Chirps
* The `store` route to used for saving ne Chrips listing.

### Middleware
---
Middleware provide a mechanism for inspecting and filtering HTTP request entering your apps. For this context, we need to place these route behind two `middleware`:
* The `auth` middleware ensures that only logged-in users can access the route.
* The `verified` middleware will be used if you decide to enable `email verification.`
```php
# routes/web.php

use App\Http\Controllers\ChirpController

route::resouces('chrips', ChirpsController::class)
  ->only(['index', 'store']) # Only index and store inside chirps
  ->middleware(['auth', 'verified']) # Must get an authentication

require __DIR__.'/auth.php'
```
This will create the following routes:
| **Verb** | **URI** | **Action** | **Route Name** |
|----------|---------|------------|----------------|
| GET      | /chirps | index      | chirps.index   |
| POST     | /chirps | store      | chirps.store   |

### Blade
---
Render a `Blade` view in the `ChirpController` class.
```php
# App/Http/Controllers/ChirpController.php

use Illuminate\View\View;

class ChirpController extends Controller
{
  public function index(): View
  {
    return view('chirps.index')
  }
}
```
Then you can make a Blade view inside the view directory
```php
# resources/view/chirp/index.blade.php

<x-app-layout>
    <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
        <form method="POST" action="{{ route('chirps.store') }}">
            @csrf
            <textarea
                name="message"
                placeholder="{{ __('What\'s on your mind?') }}"
                class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
            >{{ old('message') }}</textarea>
            <x-input-error :messages="$errors->get('message')" class="mt-2" />
            <x-primary-button class="mt-4">{{ __('Chirp') }}</x-primary-button>
        </form>
    </div>
</x-app-layout>
```

### Navigation Menu
---
Configure the navigation menu provided by `Breeze`
Update the `navigation.blade.php` component provided by Breeze to add a menu item for desktop screen.
```php
# resources/views/layouts/navigation.blade.php

<div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
  <x-nav-link :href="route('dashboard')" :active="request()->routeIs('dashboard')">
{{ __('Dashboard') }}
 </x-nav-link>

  # Adding the new Nav for Chirps
  <x-nav-link :href="route('chirps.index')" :active="request()->routeIs('chirps.index')">
{{ __('Chirps') }}
 </x-nav-link>
</div>
```

### Saving the Chirp
---
Our form has been configured to post messages to the `chirps.store` route that we created earlier (in `Route::resourece`). <br>
Now we can update the `store` method inside the `ChirpController` class to validate the data and create a new Chirp:
```php
# app/Http/Controllers/ChirpController.php

use Illuminate\Http\RedirectResponse;

class ChirpController extends Controller
{
  public function store(Request $request) # Store takes argument from the method post
  {
    $validated = $request->validate([
      'message' => 'required|string|max:255',
    ]);

    $request->user()->chirps()->create($validated);

    return redirect(route('chirps.index'));
  }
}
```
We're using the Laravel's powerful validation feature to ensure that the user provides a message and that it won't be exceed the 255 character limit of the database column. <br>
Then creating a new record that will belong to the **logged user** by Leverging a `chirp` relationship. <br>
Finally, return a redirect response to send users back to the `chirps.index` route.


### Creating a Relationship
---
>[Ref.](https://laravel.com/docs/10.x/eloquent-relationships)

We've been called a `chirps` method on the `$request->user()` object. We need to create this method on our `User` model to define a `has many` relaionship:
```php
# app/Models/User.php

use Illuminate\Database\Eloquent\Relations\HasMany;

class User extends Authenticatable
{
  public function chirps(): HasMany
  {
    return $this->hasMany(Chirp::class);
  }
}
```

### Mass Assignment Protection
---
> [Ref.](https://laravel.com/docs/eloquent#mass-assignment)

Passing all of the data from a request to your model can be risky. Imagine you have a page where users can edit their profiles. If you were to pass the entire request to the model, then a user could edit any column they like, such as an `is_admin` column (this is called [Mass Assignment Vulnerability](https://en.wikipedia.org/wiki/Mass_assignment_vulnerability). <br>
Laravel protects you from accidentally doing this by blocking mass assignment by default. We still can enable mass assignment for safe attribute by marking them as `fillable`.
```php
# app/Models/Chirp.php

class Chirp extends Model
{
  protected $fillable = [
    'message',
  ]
}
```

### Updating the Migration
The only thing missing is extra columns in our database to store the relationship between a `Chirp` and it's `User` and the message itself. <br>
```php
# databse/migrations/<timestamp>_create_chirps_table.php

return new class extends Migration
{
   ...
  public function up(): void
  {
    Schema::create('chirps', function (Blueprint $table) {
      $table->id();
      $table->foreignId('user_id')->constrained()->cascaseOnDelete();
      $table->string('message');
      $table->timestamps();
    });
  }
  ...
};
```
Migrate the databse since we added this `migration`. <br>
Each database migration will only be run once. To make additional changes to a table, you will need to create another migration. During development, you may wish to update an undeployed migration and rebuild your database from scratch using the `php artisan migrate:fresh` command.

