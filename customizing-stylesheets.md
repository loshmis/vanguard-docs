#Customizing Stylesheets

* [Introduction](#intro)
* [Requirements](#requirements)
* [Using Laravel Mix](#using-laravel-mix)
* [Changing Theme Colors](#changing-theme-colors)

---

<a name="intro"></a>
##Introduction

Vanguard is based on [Bootstrap 4](http://getbootstrap.com/) and it uses [SASS](https://sass-lang.com/) pre-processor for generating application stylesheets. This means that the recommended way to modify the stylesheets is to modify the sass files located in `resources/assets/sass` folder and then to compile them down to a single css file. 

Of course, if you want, you can always create your own css file and include after the main application css file in `resources/assets/layouts/app.blade.php` layout file, but it is much easier to use sass for any styling you want to add or update.

<a name="requirements"></a>
##Requirements

[Laravel Mix](https://laravel.com/docs/5.6/mix), which is the default way to compile assets for Laravel applications, requires **Node.js** and **NPM** to be installed on your development machine. More info on how to install it is available in [Mix's documentation](https://laravel.com/docs/5.6/mix#installation).

<a name="using-laravel-mix"></a>
##Using Laravel Mix

After you install Node.js and NPM, you need to run the following command from a Vanguard's root directory to install all required packages: 

```
npm install
```

After the package installation is finished, you can run the following commands to compile (and minify) Vanguard styles:

```
// Run all Mix tasks...
npm run dev

// Run all Mix tasks and minify output...
npm run production
```

By running the above commands you will automatically compile everything to plain CSS and put it in `public/assets/css/app.css` file. 

More info about other available Laravel Mix commands can be found in [Mix's documentation](https://laravel.com/docs/5.6/mix#installation).

<a name="changing-theme-colors"></a>
##Changing Theme Colors

As mentioned above, Vanguard's theme is based on Bootstrap 4, which means that you can easily override any SASS variables available inside the bootstrap itself like it's explained in [Bootstrap's documentation](https://getbootstrap.com/docs/4.0/getting-started/theming/).

Vanguard overrides some of Bootstrap's variables in `resources/assets/sass/_variables.scss` file. So, for example, if you want to change the theme primary color from `#179970` to `#aa0000` all you need to do is to update the `$primary` variable in `_variables.scss` file like follows

```sass
$primary: #aa0000;
```

and then to run the following command

```
npm run dev

// or, if you are building for production version of the site
npm run prod
```