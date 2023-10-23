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
