#Localization

* [Localization](#localization)
    * [Available Locales](#available-locales)
	* [Translating Vanguard](#translating-vanguard)
	* [Setting Application Locale](#setting-application-locale)
	
---

<a name="localization"></a>
##Localization

Vanguard utilizes Laravel's default localization mechanism. All translation files are located inside `resources/lang` folder. Within this directory there should be a subdirectory for each language supported by the application:

```php
/resources
    /lang
        /en
            app.php
        /es
            app.php
```

<a name="available-locales"></a>
###Available Locales

Out of the box, you can switch among following locales:

- English
- Serbian Latin

More locales will be added in the future.

<a name="translating-vanguard"></a>
###Translating Vanguard

If you want to translate Vanguard application, all you need to do is to create subfolder inside `resources/lang` directory that match your locale, copy the files from existing locale (`en` for example), and translate them to your language.
 
 **Note!** Vanguard specific files are `app.php` and `log.php`. All other files are Laravel's default localization files, and there is a big chance that someone has already translated those files for you. Check it [here](https://github.com/caouecs/Laravel-lang).

For example, if we want to translate Vanguard to Russian, we will do the following:

1. Create new folder inside `resources/lang` called `ru`. 

2. Copy `app.php` and `log.php` files from `resources/lang/en` to your newly created `ru` folder.

3. Translate all copied files to Russian.

4. Download Laravel's default translation files for Russian language from [here](https://github.com/caouecs/Laravel-lang) and put them inside your newly created `ru` folder.

<a name="setting-application-locale"></a>
###Setting Application Locale

Now, when you have your translations ready, you just need to change the currently active language by defining `APP_LOCALE` environment variable inside your `.env` file.

For example, if we want to set our language to Russian, we would set that variable as following:

```php
//...
APP_LOCALE=ru
//...
```


