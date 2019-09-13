# Plugin Service Provider

As mentioned in [creating a plugin section](creating-a-plugin.html), each plugin 
has one main class which basically serves 
as a [service provider](https://laravel.com/docs/6.0/providers) for the plugin. 
Like any other service provider it has two default methods that you can use 
for registering plugin related stuff:  **register** and **boot**.

Vanguard plugins have one more default method called **sidebar**, and it's 
purpose is to allow you to easily put the navigation items to Vanguard's 
sidebar navigation.

### The Register Method

As per [Laravel docs](https://laravel.com/docs/6.0/providers#the-register-method), 
within the `register` method, you should only bind things into 
the [service container](https://laravel.com/docs/6.0/container). For example, 
this is a perfect place to bind some concrete repository classes to a specific 
interface.

### The Boot Method

This method is called after all other service providers have been registered, 
meaning you have access to all other services that have been registered by 
the framework. Inside this method you will bind your plugin routes, register 
views, etc. 

### The Sidebar Method

If your plugin needs to add an item to the sidebar, this is the method where 
you will define how this sidebar item will look like and who should be able 
to see it.

The method returns an instance of the `Vanguard\Support\Sidebar\Item` class 
and it's recommended to open the class definition itself and go through all 
the documented methods to see everything that this class can do. Here is an 
example on how to define a sidebar item for our "Foo" plugin created above:

```php
public function sidebar()
{
    return Item::create('Foo')
        ->icon('fas fa-bullhorn')
        ->route('foo.index')
        ->permissions('foo.manage')
        ->active('foo*');
}
```

The `create` factory method from above accepts a string which is basically 
the title of the navigation item printed inside the sidebar.

The `icon` method is actually FontAwesome icon class that should be used for 
the item.

The `route` method is a named route to which this navigation item should
 point to. If you don't have a named route for this navigation item, or you 
 simply want to point to some external URL, you can use the `href` method 
 that accepts any string that will be used for a `href` attribute for a navigation link.

The `permissions` method is where you define permissions required for viewing 
the sidebar item. It accepts either a single permission as a string, array of 
permissions or even a callback that you can use if you have some complex 
authorization logic. 

If a callback provided here returns `true` then currently authenticated user 
will be able to see the navigation item. Otherwise it won't be rendered. Here is an 
example:

```php
Item::create('Foo')
    ->permissions(function ($user) {
        return $user->status === 'Foo';
    })
//...
```

The `active` method is where you define when this navigation item should be 
active according to the current URL path. In our case from above, this item 
will be active whenever there is an URL that **starts with** `foo`.