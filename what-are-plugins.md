# What are Plugins?

Vanguard can be easily extended with a different kinds of plugins. 
Each plugin is basically a Laravel package that extends some Vanguard 
classes and integrates into the application.

Each plugin can have it's own API or Web routes, migrations and it's 
own views and controllers, just like any other Laravel package. 
This is why it is **highly recommended** to check the documentation 
for [creating Laravel packages](https://laravel.com/docs/6.0/packages) before 
you proceed with creating a Vanguard plugin.

**NOTE!** Using plugins to extend the Vanguard application is highly 
recommended but it is completely optional. If you don't want to use 
plugins, you can modify the original Vanguard source files and implement 
any features you want.