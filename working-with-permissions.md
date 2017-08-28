#Working with Vanguard Permissions

* [Working with Vanguard Permissions](#working-with-vanguard-permissions)
	* [Creating Permissions](#creating-permissions)
	* [Updating View Template](#updating-view-template)
	* [Applying the Permissions](#applying-the-permissions)

---
<a name="working-with-vanguard-permissions"></a>
##Working with Vanguard Permissions

Vanguard comes with some default permissions but, if some of them does not fit your needs, they can be easily modify them. Adding new permissions is a breeze too.

In this example we will add 3 more different permissions: **View User**, **Edit User** and **Remove User**. Those permissions will allow us to have some users be able to access the users section, but some of them won't be able to do anything else than to edit user or view their profiles.

<a name="creating-permissions"></a>
###Creating Permissions

All permissions can be created through the UI, like it is explained in [roles and permissions section](roles-and-permissions.html#permissions-manage).

Created permissions for this example have have following details:

|Display Name|Name|
|------------|----|
| View User | user.view |
| Edit User | user.edit |
| Remove User | user.remove |

<a name="updating-view-template"></a>
### Updating View Template

Now, since we have those permissions created, we need to update the view that is used for displaying users list. The HTML used for displaying the list of users is located inside `resources/views/user/list.blade.php` view file. 

Our goal is to display buttons for editing, viewing or removing some user only if currently logged in user has the appropriate permission. In order to display something based on user's permissions, we just have to surround that HTML with following [Blade](https://laravel.com/docs/5.4/blade) directives:

```php
@permission('user.view')
	// Anything here will be displayed only
	// if currently logged in user has "user.view" permission
@endpermission
```

So, to apply this to our use-case, we will surround those buttons like following:

```php
@permission('user.view')
	<a href="{{ route('user.show', $user->id) }}" 
	   class="btn btn-success btn-circle"
       title="View User" data-toggle="tooltip" data-placement="top">
       <i class="glyphicon glyphicon-eye-open"></i>
    </a>
@endpermission

// Do the same for all 3 buttons
```

Since view is now updated, if you access the `yourdomain.com/user` URL, you won't see those buttons for viewing, editing and removing users. But, as you probably already guessed, you are still able to edit some user by directly accessing the following URL `yourdomain.com/user/USER_ID/edit`. That's because the process is not completed yet, and you have to update your routes or controller.

<a name="applying-the-permissions"></a>
### Applying the Permissions

Removing the buttons from users list is not actually protecting the application. If users type specific URL directly in browser's address bar, they will be able to access the desired page. In order to protect this, we have to apply permission [middleware](https://laravel.com/docs/5.4/middleware). 

This can be done in two ways. We can update the controller and add middleware directly inside the controllers constructor, or we can update `routes/web.php` file and apply middleware to specific route.

####Updating UsersController

One way to protect our pages and make them available only for users with specific permissions, is to add middleware directly to controller's constructor. For our example, we have to edit `app/Http/Controllers/Web/UsersController.php` controller and add the following code inside its `__construct` method:

```php
$this->middleware('permission:user.view', ['only' => 'view']);

$editMethods = [
    'edit', 'updateDetails', 'updateAvatar', 'updateAvatarExternal',
    'updateSocialNetworks', 'updateLoginDetails', 'enableTwoFactorAuth',
    'disableTwoFactorAuth'
];

$this->middleware('permission:user.edit', ['only' => $editMethods]);

$this->middleware('permission:user.remove', ['only' => 'delete']);
```

After applying middleware to controller's methods (**only** option provided as second argument means that permission middleware should only be applied to specified methods inside the controller), Vanguard will throw `403 Forbidden` exceptions whenever someone try to access the protected URL, and it will make that part of the system available only for users with appropriate permissions.

####Updating Routes

Updating routes is another way to apply middleware to specific resource (resource <=> URL). Applying permission to specific routes is fortunately maybe even easier than applying them inside the controller. For example, if we want to apply a **user.view** permission to it's route, all we have to do is to update it as following:

```php
Route::get('user/{user}/show', [
    'as' => 'user.show',
    'uses' => 'UsersController@view',
    'middleware' => ['permission:user.view']
]);
```

And that's it, just by adding that `middleware` option to route options array, it will protect the route and make it unavailable to users without **user.view** permission. 

By following this example, you can now update all routes and set desired permissions.
