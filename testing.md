#Automated Testing

* [Automated Testing](#automated-testing)
	* [Running Tests](#running-tests)

---

<a name="automated-testing"></a>
##Automated Testing

Vanguard comes with more than **three hundred** automated test. Most of them are functional tests that are 
using to verify all vital parts of Vanguard application, but there are also unit tests for some parts of the system. 
If you want to, you can run those automated tests by following steps below and use them as starting point and continue 
adding tests for everything you change inside the application.

<a name="running-tests"></a>
###Running Tests

You can easily run the tests just by typing 

```php
phpunit
```

or, if you don't have the `phpunit` in your PATH, then do it like following from Vanguard's root folder

```php
./vendor/bin/phpunit
```

PHP unit will then execute your tests and you will be sure that your application is working as you expect.

Vanguard is fully tested and working on PHP 7.1.3+.

![Vanguard - Automated Tests - PHP](assets/img/testing-php-full.png)

###Different Databases

By default, Vanguard is configured to use SQLite in Memory database to perform tests. However, if you would like to test it on some other databases like MySQL, 
then you will have to modify `DB_CONNECTION` environment variable inside `phpunit.xml` file and set it to `mysql` (or you can just completely remove it, since MySQL driver is default)
and you have to add the name for test database by defining `DB_DATABASE` variable like following:

```xml
<php>
    <env name="APP_ENV" value="testing"/>
    <env name="CACHE_DRIVER" value="array"/>
    <env name="SESSION_DRIVER" value="array"/>
    <env name="QUEUE_DRIVER" value="sync"/>
    <env name="DB_CONNECTION" value="mysql"/> <!-- database connection -->
    <env name="DB_DATABASE" value="vanguard_test"/> <!-- test db name -->
    <env name="MAIL_DRIVER" value="log"/>
</php>
```

You can modify any other environment variables here if necessary.