# Removing a Plugin

You can always manually delete a plugin from the `/plugins` directory or, 
if you want, you can use the `php artisan vanguard:delete-plugin Foo` command 
and let the system delete it for you and take care of updating the main 
`composer.json` file.

If you have installed the plugin via Composer and you want to remove it, 
the procedure is as easy as above. For example, if you want to remove the 
Vanguard official Announcements plugin that comes with Vanguard out of the box, 
you'll need to do the following two things:

1) Remove the `\Vanguard\Announcements\Announcements::class,` line from the 
array of active plugins in `VanguardServiceProvider`. This will make plugin 
inactive and it won't appear inside the Vanguard at all.

2) Run `composer remove vanguardapp/announcements` to completely remove plugin 
from the system.