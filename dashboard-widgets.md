# Dashboard Widgets

Vanguard's dashboard consists of a set of widgets that are being rendered in a 
predefined fashion. 

Dashboard widget is a class that extends the abstract `Vanguard\Plugins\Widget` 
class and provides one simple `render()` method that is responsible for rendering 
a widget.

All widget classes will be resolved out of Laravel's 
[service container](https://laravel.com/docs/6.0/container) so you can inject 
any dependencies you want through the constructor.

## Creating a New Widget

The easiest way to understand how to create a widget is to look at the existing one. 
Default Vanguard widgets can be found in `app/Support/Plugins/Dashboard/Widgets` 
folder and below is an example of the widget responsible for displaying the total 
number of users available inside the system.

```php
<?php

namespace Vanguard\Support\Plugins\Dashboard\Widgets;

use Vanguard\Plugins\Widget;
use Vanguard\Repositories\User\UserRepository;

class TotalUsers extends Widget
{
    /**
     * {@inheritdoc}
     */
    public $width = '3';

    /**
     * {@inheritdoc}
     */
    protected $permissions = 'users.manage';

    /**
     * @var UserRepository
     */
    private $users;

    /**
     * TotalUsers constructor.
     * @param UserRepository $users
     */
    public function __construct(UserRepository $users)
    {
        $this->users = $users;
    }

    /**
     * {@inheritdoc}
     */
    public function render()
    {
        return view('plugins.dashboard.widgets.total-users', [
            'count' => $this->users->count()
        ]);
    }
}

```

### Widget Width

Each widget has a `$width` property that is actually a number 
between **1** and **12**. This is basically the equivalent to the 
[Bootstrap columns](https://getbootstrap.com/docs/4.3/layout/grid/) so if you 
set the width to `4` it means that it will be transformed to a bootstrap 
class named `col-md-4`.

In case if you want to provide your own layout classes, you should set 
the `$width` to `null` (which is also the default value) and you should 
provide the column classes on your own.

### Widget permissions

You can define who can see a specific widget by defining the permissions required 
for that widget. There are 3 different ways to define the required widget 
permissions, depending on what exactly you need to check:

**Single Permission** - A currently authenticated user must have the defined 
permission to be able to see the widget on the dashboard:

```php
//...

protected $permissions = 'users.manage';

//...
```

**Multiple Permissions** - A currently authenticated user must have all the 
permissions from the given list.

```php
//...

protected $permissions = ['users.manage', 'foo.bar'];

//...
```

**Closure Based Permission** - If a closure returns `true` then Vanguard will 
consider that the current user has the permission to see the widget on the dashboard.

In this case, you will need to define your permission inside the constructor.

```php
//...

public function __construct()
{
    $this->permissions = function ($user) {
        return $user->status === 'Foo';
    };
}

//..
```

## Registering Widgets

To register a widget you need to add the full path to the widget class inside 
the array that is being returned from the `widgets()` method 
in `VanguardServiceProvider`. 

Here is an example (pay attention to the `use` line at the top of the file):

```php
use Vanguard\Support\Plugins\Dashboard\Widgets\TotalUsers;

//...

protected function widgets()
{
    return [
        //...

        TotalUsers::class,

        //...
    ];
}
```

The widget position on the dashboard will depend on the index inside the array 
from above. For example, if you have two widgets, `WidgetA` and `WidgetB`, and 
your widgets array looks like inside the code snippet below, then `WidgetB` will 
be rendered before the `WidgetA`.

```php
//...

protected function widgets()
{
    return [
        //...

        WidgetB::class,
        WidgetA::class,

        //...
    ];
}
```
