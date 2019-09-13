# Activating a Plugin

Every Vanguard plugins needs to be activated after the installation. 
All you need to do in order to enable the plugin is to reference it's 
service provider class inside the array that is being returned from 
the `plugins()` method in `app/Providers/VanguardServiceProvider.php`.

In our case, it will look something like following (pay attention to 
the `use` line at the top of the file):

```
use Vanguard\Foo\Foo;

//...

protected function plugins()
{
    return [
        Dashboard::class,
        Users::class,
        UserActivity::class,
        RolesAndPermissions::class,
        Settings::class,
        Foo::class, // or you can add it as a string, like '\Vanguard\Foo\Foo'
    ];
}
```

As soon as the plugin is activated it will automatically register a new route 
for you, which you can use to test if the plugin is installed properly. 
In our example from above, you should be able to navigate to "/foo" page 
and it will show something like following:

![Vanguard - Plugin Landing Page](assets/img/plugin-landing-page.png)