#Adding custom fields to registration form

* [Introduction](#intro)
* [Adding Missing Database Fields](#database)
* [Updating Form HTML](#form-html)
* [Updating Auth Controller](#controller)
* [Updating User Model](#model)

---

##Introduction

Registration form customisation is something that probably no one can avoid if it comes to Vanguard customisation. If you are familiar with [Laravel](https://laravel.com/) then adding another field into registration form will be an easy task for you.

However,  for those who doesn't have a clue how Laravel is working, this will be challenging tutorial.

Lets say that we want to add two new fields into the registration form: **Nick Name** and **Country**.
Also, we will make Nick Name to be required and minimum 3 characters long.

This is probably the most difficult scenario, so if you understand how this one is working, then you can add any other field into that form.

##Adding Missing Database Fields

Since **Nick Name** does not exist into our database schema, we will have to add it. There are many ways to add this field into users table, and we will cover two of them.

###Laravel's Migrations (recommended)

Creating [migrations](https://laravel.com/docs/5.2/migrations) for your database schema is the best way to create and modify your database schema. Also, since migrations are basically PHP files, those files will be stored on your Version Control System (Git, Mercurial, etc.) so any of your coworkers will have access to database schema that is being used for your project, and, the best thing about it, is that you will be able to see full history of changes for any of your database tables.

So, for our tutorial, we will create new database migrations by typing the following command into our terminal:

```
php artisan make:migration add_nick_name_field_to_users_table
```

After this command is executed, new file will be created into our `database/migrations` folder. Since we want to alter the existing `users` table, the  newly created migration class will look like following:

```php
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class AddNickNameFieldToUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->string('nick', 20);
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropColumn('nick');
        });
    }
}

``` 

When it is executed, this migration will add new column into `users` database table called `nick`, and it will be type of `VARCHAR(20)`. If you want to learn more about Laravel Migrations, check the [documentation](https://laravel.com/docs/5.2/migrations#modifying-columns).

Now, since our migration is ready, we can execute it by typing the following command into our terminal:

```
php artisan migrate
```

If you check the database using PHPMyAdmin (or some other similar app) you will see that our `nick` field is added to `users` database table. 

###Manually Add Missing Field

If for some reason you decide not to use the migrations for altering the database, you can manually add missing `nick` field using PHPMyAdmin or similar application. Just make it `varchar(20)` and we are good to go.

>**Note!** This maybe looks easier for now, but what if you forgot to tell to your co-workers that you have added that new field? Or even if you tell them, each one of them will have to create it manually.

## Updating Form HTML

