# Template Hooks

Vanguard provides a convenient way to hook into the Blade template rendering 
process and add any custom HTML you want at a specific place on the page.
This will allow your plugins to add some plugin-related HTML at the specific 
place on the page and have it be rendered on every request.

## Template Hooks Placeholders

If you want to define a hook placeholder somewhere inside your blade template file, 
you can easily do it by using the `@hook` blade directive, like following:

```
@hook('hook-name')
```

This means that when the blade template is rendering, if there are any hook 
handlers defined for a hook with name `hook-name` then each hook handler will 
be executed and whatever each of the handler returns will be at the same place 
inside the template where the `@hook('hook-name')` is defined.

## Hook Handlers

A hook handler is a simple class that implements 
the `Vanguard\Plugins\Contracts\Hook` interface and has one `handle()` method. 
You can place this class anywhere you want and, since this class will be resolved 
out of Laravel's [service container](https://laravel.com/docs/6.0/container) you 
can inject any dependencies through the constructor.

Here is an example class for the Announcements plugin that renders 5 most recent 
announcements inside the navbar:

```php
<?php

namespace Vanguard\Announcements\Hooks;

use Vanguard\Announcements\Repositories\AnnouncementsRepository;
use Vanguard\Plugins\Contracts\Hook;

class NavbarItemsHook implements Hook
{
    /**
     * @var AnnouncementsRepository
     */
    private $announcements;

    public function __construct(AnnouncementsRepository $announcements)
    {
        $this->announcements = $announcements;
    }

    /**
     * Execute the hook action.
     *
     * @return \Illuminate\Contracts\View\Factory|\Illuminate\View\View
     */
    public function handle()
    {
        $announcements = $this->announcements->latest(5);
        $announcements->load('creator');

        return view('announcements::partials.navbar.list', compact('announcements'));
    }
}

```

## Registering Hook Handlers

Once you create a hook handler class, the only remaining thing to do is to 
register it as a handler for a specific view hook. You can do this inside 
the `boot` method in your plugin service provider class like following

```php
use Vanguard\Plugins\Vanguard;
use Vanguard\Announcements\Hooks\NavbarItemsHook;

//...

public function boot()
{
    Vanguard::hook('navbar:items', NavbarItemsHook::class);
}
```

The above code means that whenever inside the template we have a hook placeholder 
defined as `@hook('navbar:items')`, the placeholder will be replaced with 
whatever is returned from the `NavbarItemsHook::handle` method.

## Pre-defined Vanguard Template Hooks

Vanguard comes with the following list of hooks that you can hook into:

- `auth:styles` - Hook into the template right before the closing `</head>` tag for the **auth layout**.
- `auth:scripts` - Hook into the template right before the closing `</body>` tag for the **auth layout**.
- `app:styles` - Hook into the template right before the closing `</head>` tag for the **main application layout**.
- `app:scripts` - Hook into the template right before the closing `</body>` tag for the **main application layout**.
- `navbar:items` - Hook into the template where header navigation items are defined. Whatever you print here will be displayed next to the user's avatar inside the header.
- `navbar:dropdown` - Hook into the header dropdown displayed when you click on the user's avatar. This is a convinient hook if you need to add an item to the dropdown menu.