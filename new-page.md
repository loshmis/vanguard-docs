#Creating New Page

* [Creating New Page](#creating-new-page)
	* [Page Route](#page-route)
	* [Creating The Controller](#controller)
	* [Actual Page View](#view)
	* [Sidebar Menu](#sidebar)
	
---

<a name="creating-new-page"></a>
##Creating New Page

Chances are high that you would like to create your own pages inside the Vanguard application. 
This section will explain in details everything you need to do to add your own page into the system.

The page we are going to add will be simple page that will display the list of all users with active sessions.


<a name="page-route"></a>
###Page Route

First thing we will have to do is to create new route for your page. We can do that by simply editing `/routes/web.php` file and adding the following code 
anywhere inside the file. I've added it on top.

```php
Route::get('active-users', function () {
    return "Active users will be displayed here.";
});
```

To verify that this code is actually working, you should go to `yourwebsite.com/active-users` and you should see following text on your screen: 

```html
Active users will be displayed here.
```

This means that your route is now working properly, so we can proceed and create new controller that will handle the actual request, instead of 
using this [closure](http://php.net/manual/en/class.closure.php), as we did in our example above.

<a name="controller"></a>
###Creating The Controller

Creating new controller in Laravel is pretty easy. If you are familiar with the terminal, you can navigate to Vanguard's root folder and type the following command

```cli
php artisan make:controller ActiveUsersController
```

After you execute this command, new controller will be automatically created for you and placed inside `app/Http/Controllers` folder. The file will be named `ActiveUsersController.php`.

