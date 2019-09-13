# Creating a Plugin

When you are building a new plugin, you can either do everything from 
scratch or you can use the following command which will scaffold the 
base files for the plugin for you:

```
php artisan vanguard:make-plugin Foo
```

The command from above will generate a new folder called `Foo` inside the 
Vanguard's `/plugins` directory, which is the default location for all 
Vanguard plugins and it will update your main `composer.json` file to 
reference the newly installed plugin.
The root namespace for all plugin classes created in this case will 
be `Vanguard\Foo`.

Each plugin has one main class which basically serves 
as a [service provider](https://laravel.com/docs/6.0/providers) for the plugin. 
In our case, the main plugin service provider is defined inside 
the `plugins/Foo/src/Foo.php` file (it will always have the same name as the 
plugin itself if you scaffold the plugin using `vanguard:make-plugin` command).

The generated plugins' top-level structure will look like following:

```
plugins
-- Foo
---- config
---- database
---- resources
---- routes
---- src
---- tests
---- .gitignore
---- composer.json
---- package.json
---- webpack.mix.js
```

Since not all plugins will have all all the above, you are free to customize 
the directory structure however you want.
