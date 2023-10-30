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

### Retrieving the Chirps
---
Let's update the `index` method on our `ChirpController` class to pass Chirps from every user to our index pages.
```php
# app/Http/Controllers/ChirpController.php

class ChirpController extends Controller
{
  public function index(): View
  {
    return view('chirps.index', [
      'chirps' => Chirp::with('user')->latest()->get(),
    ]
  }
}
```
We're using the `Elequent` `with` method to load every Chrip's associated User. We've also used the `latest` scope to return the records in reverse-chronological order.

### Connecting users to Chirps
---
We've instructed Laravel to return `user` relationship so that we can display the name of the Chirp's author. But, the Chirp's `user` relationship hasn't been defind yet. <br>
We need to add relationship `belongs to` `Chirp` model (the inverse relationship with the `user` model):
```php
# app/Models/Chirp.php

use Illuminate/Databse/Eloquent/Relations/BelongsTo;

class Chirp extends Model
{
  public function user(): BelongsTo
  {
    return $this->belongsto(User::class);
  }
}
```

### Updating our View
---
Update the `chirps.index` component by displaying the Chirps form:
```php
# resources/views/chirps/index.blade.php

<x-app-layout>
    <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
        <form method="POST" action="{{ route('chirps.store') }}">
            @csrf
            <textarea
                name="message"
                placeholder="{{ __('What\'s on your mind?') }}"
                class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
            >{{ old('message') }}</textarea>
            <x-input-error :messages="$errors->store->get('message')" class="mt-2" />
            <x-primary-button class="mt-4">{{ __('Chirp') }}</x-primary-button>
        </form>
 
        <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
            @foreach ($chirps as $chirp)
                <div class="p-6 flex space-x-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600 -scale-x-100" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                    </svg>
                    <div class="flex-1">
                        <div class="flex justify-between items-center">
                            <div>
                                <span class="text-gray-800">{{ $chirp->user->name }}</span>
                                <small class="ml-2 text-sm text-gray-600">{{ $chirp->created_at->format('j M Y, g:i a') }}</small>
                            </div>
                        </div>
                        <p class="mt-4 text-lg text-gray-900">{{ $chirp->message }}</p>
                    </div>
                </div>
            @endforeach
        </div>
    </div>
</x-app-layout>
```

### Routing Editing Chirps
---
First, we update our routes file to enable `chirps.edit` and `chirps.update`. The `chirps.edit` route will display the form or editing a Chirp. while the `chirps.update` route will accept the data from the form and update the model:
```php
# route/web.php

Route::resources('chirps', ChirpController::class)
  ->only(['index', 'store', 'edit', 'update'])
  ->middleware(['auth', 'verified')];
```

### Linking to the edit page
```php
# resources/views/chirps/index.blade.php

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
 
        <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
            @foreach ($chirps as $chirp)
                <div class="p-6 flex space-x-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600 -scale-x-100" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                    </svg>
                    <div class="flex-1">
                        <div class="flex justify-between items-center">
                            <div>
                                <span class="text-gray-800">{{ $chirp->user->name }}</span>
                                <small class="ml-2 text-sm text-gray-600">{{ $chirp->created_at->format('j M Y, g:i a') }}</small>
                                @unless ($chirp->created_at->eq($chirp->updated_at))
                                    <small class="text-sm text-gray-600"> &middot; {{ __('edited') }}</small>
                                @endunless
                            </div>
                            @if ($chirp->user->is(auth()->user()))
                                <x-dropdown>
                                    <x-slot name="trigger">
                                        <button>
                                            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                                                <path d="M6 10a2 2 0 11-4 0 2 2 0 014 0zM12 10a2 2 0 11-4 0 2 2 0 014 0zM16 12a2 2 0 100-4 2 2 0 000 4z" />
                                            </svg>
                                        </button>
                                    </x-slot>
                                    <x-slot name="content">
                                        <x-dropdown-link :href="route('chirps.edit', $chirp)">
                                            {{ __('Edit') }}
                                        </x-dropdown-link>
                                    </x-slot>
                                </x-dropdown>
                            @endif
                        </div>
                        <p class="mt-4 text-lg text-gray-900">{{ $chirp->message }}</p>
                    </div>
                </div>
            @endforeach
        </div>
    </div>
</x-app-layout>
```

### Creating the Edit Form
---
This is similar to the form for creating Chirps, except we'll post to the `chirps.update` route and use the` @method` directive to specify that we're making a "PATCH" request. We'll also pre-populate the field with the existing Chirp message:
```php
<x-app-layout>
    <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
        <form method="POST" action="{{ route('chirps.update', $chirp) }}">
            @csrf
            @method('patch')
            <textarea
                name="message"
                class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
            >{{ old('message', $chirp->message) }}</textarea>
            <x-input-error :messages="$errors->get('message')" class="mt-2" />
            <div class="mt-4 space-x-2">
                <x-primary-button>{{ __('Save') }}</x-primary-button>
                <a href="{{ route('chirps.index') }}">{{ __('Cancel') }}</a>
            </div>
        </form>
    </div>
</x-app-layout>
```

### Updating the Controller
---
Let's update the `edit` method on our `ChirpController` to display our form. Laravel will automatically load the Chirp model from the database using [route model binding](https://laravel.com/docs/9.x/routing#route-model-binding) so we can pass it straight to the view. <br>
We'll then update the `update` method to validate the request and update the database.
```php
# app/Http/Controllers/ChirpController.php

    public function edit(Chirp $chirp): View
    {
        $this->authorize('update', $chirp);
 
        return view('chirps.edit', [
            'chirp' => $chirp,
        ]);
    }

  
  public function update(Request $request, Chirp $chirp): RedirectResponse
    {
        $this->authorize('update', $chirp);
 
        $validated = $request->validate([
            'message' => 'required|string|max:255',
        ]);
 
        $chirp->update($validated);
 
        return redirect(route('chirps.index'));
    }

```
You may have noticed the validation rules are duplicated with the `store` method. You might consider extracting them using Laravel's [Form Request Validation](https://laravel.com/docs/validation#form-request-validation), which makes it easy to re-use validation rules and to keep your controllers light.

### Authorization
---
By default, the `authorize` method will prevent *everyone* from being able to update the Chrip. So we can specify who is allowed to update it by creating a [Model Policy](https://laravel.com/docs/authorization#creating-policies) with the following command:
```php
php artisan make:policy ChirpPolicy --model=Chirp
```
This will create a policy class at `app/Policies/ChirpPolicy.php` which we can update to specify that only the author is authorized to update a Chirp:
```php
# app/Policies/ChirpPolicy.php

class ChirpPolicy
{
  public function update(User $user, Chirp $chirp): bool
  {
    return $chirp->user()->is($user);
  }
}
```

### Routing to Delete Chirps
---
First, we can setup the route for deleting
```php
# routes/web.php
Route::resource('chirps', ChirpController::class)
    ->only(['index', 'store', 'edit', 'update', 'destroy'])
    ->middleware(['auth', 'verified']);
```

### Updating the Controller
---
```php
# app/Http/Controllers/ChirpController.php

public function destroy(Chrip $chirp): RedirectResponse
{
  $this->authorize('delete', $chirp);

  $chirp->delete();

  return redirect(route('chirp.index'));
}
```

### Setup the Authorization
---
Rather than repeating the same logic with the `update` method, we can reuse the same logic by calling the `update` method.
```php
# app/Policies/ChirpPolicy.php

  /**
   * Determine whether the user can update the model.
   */
  public function update(User $user, Chirp $chirp): bool
  {
      return $chirp->user()->is($user);
  }

  /**
   * Determine whether the user can delete the model.
   */
  public function delete(User $user, Chirp $chirp): bool
  {
      return $this->update($user, $chirp);
  }
```

### Updating View
---
```php
<x-slot name="content">
    <x-dropdown-link :href="route('chirps.edit', $chirp)">
        {{ __('Edit') }}
    </x-dropdown-link>
    <form method="POST" action="{{ route('chirps.destroy', $chirp)}}">
        @csrf
        @method('delete')
        <x-dropdown-link :href="route('chirps.destroy', $chirp)" onclick="event.preventDefault(); this.closest('form').submit();">
            {{ __('Delete')}}
        </x-dropdown-link>
    </form>
</x-slot>
```




