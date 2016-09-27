#Development Mode

* [Development Mode](#development-mode)
    * [Debug Bar](#debug-bar)
	
---

<a name="development-mode"></a>
##Development Mode

While you are developing new Vanguard features, or you are customizing the existing features, you should definitely 
enable development mode so you can clearly see all errors on the screen, without constantly having to check you log file.

To enable development mode, all you need to do is to modify your `.env` file and set `APP_ENV` and `APP_DEBUG` to following values:
 
```php
APP_ENV=local
APP_DEBUG=true
```

<a name="debug-bar"></a>
###Debug Bar

Vanguard comes with awesome [Laravel Debugbar](https://github.com/barryvdh/laravel-debugbar) package that is automatically 
enabled for you if you enable development mode like it is described above. The package itself is very helpful during the development
process, and you can use it to see which queries are executed during page load, to check the session data etc.

 ![Vanguard Development Mode - Debug Bar](assets/img/debug-bar.png)