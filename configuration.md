#Configuration

* [Configuration](#configuration)
	* [Social Authentication](#social-authentication)
	* [Email](#email)
	* [Session](#session)

---


##Configuration

This section contains some important configuration options that are specific to Vanguard application. Since Vanguard is using Laravel PHP framework, full configuration options for some framework specific stuff can be found inside [Laravel documentation](https://laravel.com/docs/5.2/configuration). 

###Social Authentication

If you want to allow social authentication for your users, you will have to define which social providers you want to allow. List of social providers is declared inside `config/auth.php` file.  Vanguard supports **Facebook**, **Twitter** and **Google+** by default.

 The following code is an example of allowing all three default supported providers for Vanguard application:

```php
'social' => [
    'providers' => ['facebook', 'twitter', 'google']
],
```
If you want to disable some social provider, just remove it from that providers array and you are good to go. Also, if you don't want social authentication on your website, just **empty** that providers array, as following:

```php
'social' => [
    'providers' => []
],
```

####Facebook

[Here](https://developers.facebook.com/docs/apps/register) is an detailed explanation of how you can create an Facebook application and acquire application id and secret key, required for social authentication. During the application creation and configuration, make sure that you have entered correct application domain on application's settings page.

After you create an application, you can find your App Id and App Secret keys on your application's Dashboard. Those keys should be copied to `.env` configuration file available inside Vanguard's root directory, as following:

```
FACEBOOK_CLIENT_ID=your_application_id_from_facebook
FACEBOOK_CLIENT_SECRET=your_application_secret_from_facebook
FACEBOOK_CALLBACK_URI=http://YOUR_DOMAIN/auth/facebook/callback
```

>**Note!** The `.env` file will be available inside your root folder **after** successful installation, so make sure that you have already installed the application before you start the configuration process.

