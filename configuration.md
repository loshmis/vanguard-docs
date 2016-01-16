#Configuration

* [Configuration](#configuration)
	* [Social Authentication](#social-authentication)
	* [Two-Factor Authentication (2FA)](#two-factor-auth)
	* [Google reCAPTCHA](#recaptcha)
	* [Email Configuration](#email-configuration)
	* [Session Configuration](#session-configuration)

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

####Twitter

In order to create Twitter application, and get the required Application Id and Secret key, go to [Twitter Application Management](https://apps.twitter.com/) and click **Create New App** button at the top right corner. 
When app creation form is opened, fill all required fields and click **Create your Twitter Application** button at the bottom of the page.

>**Note!** Your **Callback URL** is `http://YOUR_DOMAIN/auth/twitter/callback`.

After application is created, go to **Keys and Access Tokens** tab, grab your Consumer Key and Consumer Secret and paste them into your `.env` file as following:

```
TWITTER_CLIENT_ID=your_consumer_key
TWITTER_CLIENT_SECRET=your_consumer_secret
TWITTER_CALLBACK_URI=http://YOUR_DOMAIN/auth/twitter/callback
```

####Google+

In order to utilise Google+ Authentication, first you need to create new Google Project/Application. To do that, first you have to go to https://console.developers.google.com/projec, click **Create project** button at top left corner and enter your Project name.

After you have created your project, you now have to enable Google+ API and get the credentials that will be used for authentication. Go to https://console.developers.google.com/apis/library, select your project from dropdown available on top right header and click on Google+ API link inside the list of available Google APIs.

![Vanguard Social Authentication - Google APIs](assets/image/g_plus_api.png)

After opening the Google+ API page, click **Enable API** button in order to enable the API.

![Vanguard Social Authentication - Enable Google+ API](assets/image/g_plus_api_enable.png)

After enabling the API, the only remaining step is to get the credentials you need. Just click on **Go to Credentials** button, fill the displayed credentials form as following and click **What credentials do I need?** button:

![Vanguard Social Authentication - Getting Credentials](assets/image/g_plus_api_credentials1.png)

After entering in the required application Name, make sure that you enter `http://YOUR_DOMAIN` in **Authorized JavaScript origins** section, and `http://YOUR_DOMAIN/auth/google/callback` in **Authorized redirect URIs** section. 

After you fill those fields, click **Create client ID" button, provide your product name as required, and get your Client Id and Client Secret keys.

When you have those keys, the only thing left for you to do is to paste them into your `.env` file as following:

```
GOOGLE_CLIENT_ID=your_client_id
GOOGLE_CLIENT_SECRET=your_client_secret
GOOGLE_CALLBACK_URI=http://YOUR_DOMAIN/auth/google/callback
```

###Two-Factor Authentication (2FA)

Vanguard utilises [Authy](https://www.authy.com/), reliable third-party service, to allow Two-Factor Authentication for users. 

All you need to do is to login to your [Authy Dashboard](https://dashboard.authy.com/signin) (or create an Authy account if you are not already registered) and create New Application. After creating the application, you will be able to get your Api Key from your application's Dashboard. When you have your API Key, you should paste it to your `.env` file as following:

```
AUTHY_KEY=your_authy_api_key
```

And that's it, you are now able to Enable/Disable Two-Factor authentication anytime you want from your [Auth and Registration](settings/auth-and-registration) settings page.

###Google reCAPTCHA

Google's reCAPTCHA is available for Vanguard's user registration form. Enabling reCAPTCHA is, fortunately, an easy thing to do. Just go to [reCaptcha Website](https://www.google.com/recaptcha/intro/index.html), get your _Site Key_ and _Secret Key_ and paste them into your `.env` file as following:

```
RECAPTCHA_SECRETKEY=your_recaptcha_secret_key
RECAPTCHA_SITEKEY=your_recaptcha_site_key
```

That's all you need to do. Now you are able to enable or disable reCAPTCHA on your registration page from  [Auth and Registration](settings/auth-and-registration) settings page.

###Email Configuration

By default, Vanguard will be configured to use native PHP mail driver for sending emails. However, you can configure it to use `SMTP`,  `Sendmail`,  `Mailgun`, `Mandrill`, `Amazon SES` or `Log` driver (good for development purposes).

Here we will cover only SMTP configuration, and if you are interested in other options mentioned above, you can find all details of how to enable them inside [Laravel Documentation](https://laravel.com/docs/5.2/mail#introduction).

####SMTP

In order to switch to SMTP driver, instead of native PHP mail, just open your `.env` file and define your mail environment variables as following:

```
MAIL_DRIVER=smtp
MAIL_HOST=your_smtp_host
MAIL_PORT=your_smtp_port
MAIL_USERNAME=your_smtp_username
MAIL_PASSWORD=your_smtp_password
MAIL_ENCRYPTION=your_smtp_encryption
```

>**Note** If your SMTP server does not have encryption, just set it to `null`, or set it to blank like this: `MAIL_ENCRYPTION=`.

