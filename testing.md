#Automated Testing

* [Automated Testing](#automated-testing)
	* [Preparation](#preparation)
	* [Running Tests](#running-tests)

---

<a name="automated-testing"></a>
##Automated Testing

Vanguard comes with more than a **hundred** automated test. Most of them are functional tests that are using to verify all vital parts of Vanguard application, but there are also unit tests for some parts of the system. If you want to, you can run those automated tests by following steps below and use them as starting point and continue adding tests for everything you change inside the application.

<a name="preparation"></a>
###Preparation

Since Vanguard is using [Mailtrap](https://mailtrap.io/) for testing emails that should be sent to the users, you will have to sign up for Mailtrap (it's free) and put your API key into `.env` file as following.

```php
MAILTRAP_SECRET=your_mailtrap_secret_key
```

Also, you have to tell Laravel that what credentials should be used for sending emails by adding following variables into your `.env` file:

```php
MAIL_HOST=mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=mailtrap_username
MAIL_PASSWORD=mailtrap_password
MAIL_ENCRYPTION=null
```

<a name="running-tests"></a>
###Running Tests

After you insert required Mailtrap credentials, you are ready to start your tests just by typing 

```php
phpunit
```

PHP unit will then execute your tests and you will be sure that your application is working as you expect.

Vanguard is fully tested and working on PHP 5.6.4+ (including PHP 7).

![Vanguard - Automated Tests - PHP](assets/img/testing-php.png)