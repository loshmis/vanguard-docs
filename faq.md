#FAQ

---

####HTTP 500 Error: Request cannot be processed. What should I do?

Make sure that you have **PHP >= 5.6.4**, since that's minimum PHP version required to use Vanguard.
 
####The requested URL `/install` was not found on this server. Am I missing some files?

Of course that all files are there and the reason why you don't see that "install" folder at all is because Vanguard, as Laravel application, does not work like that.

All requests are routed through `index.php` file (it utilises [front controller pattern](http://martinfowler.com/eaaCatalog/frontController.html)) and then routes are responsible for routing 
your request to appropriate controller and method.

Now, the reason you get such message is probably because you most likely use Apache Web Server which does not have `mod_rewrite` installed and enabled.
This means that you will have to enable Apache `mod_rewrite`, and you can do it by typing the following command into the terminal (after you login to your server via SSH):

```php
a2enmod rewrite
```

This command will enable Apache rewrite module. If you get some message like "Module rewrite already enabled", this means that module is already enabled and you can proceed to next step, which is updating Apache configuration file.

After you are sure that you have your module enabled, next thing to do is to make sure that you have added `allow from all` inside your Vanguard's Apache virtual host configuration, like following:

```xml
<VirtualHost *:80> 
    DocumentRoot /var/www/vanguard/public 
    ServerName mydomain.com 
    <Directory "/var/www/vanguard/public"> 
        allow from all <!-- required -->
        Options FollowSymLinks 
    </Directory> 
</VirtualHost>
```

Of course, your VirtualHost configuration will probably be different, but you must allow Vanguard's `.htaccess` file to actually do some work by defining this `allow` rule.

>**Note!** If you don't have SSH access to your server, or you are using cPanel (or any similar software) you should probably enable Apache rewrite module from there. If not, you will have to contact your support to do that for you.

<a name="redirect-page"></a>
####How to change redirect page after login?

Modifying redirect page after login is simple. Just check `handleUserWasAuthenticated` method available inside `app/Http/Controllers/Web/Auth/AuthController`
and replace `return redirect()->intended();`  line with **one** of the following:

```php
// to redirect to custom url (can be any url)
return redirect()->to("your url here");

//or

// to redirect to specific Vanguard route
// with name that is already defined for that route
return redirect()->route("route_name_here");
```

####Maximum execution time of 30 seconds exceeded. What should I do?

Apache on XAMPP (especially on Windows) is slower than Apache on most other platforms. 
This means that you should increase `max_execution_time` configuration parameter in `php.ini` from default
value of `30` to any reasonably higher value (like `240` for example). After you do that, just restart Apache and everything should work without any problems.

####How to modify session expiration parameters?

Check [session configuration section](configuration.html#session-configuration).

####I cannot use the API to authenticate users. What should I do?

Make sure that you have enabled the API like it is described in [JSON API configuration section](configuration.html#json-api).

