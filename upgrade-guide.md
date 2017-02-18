#Upgrade Guide

* [Upgrade Guide](#upgrade-guide)
    * [To 1.3.0 from 1.2.1](#upgrade-1.3.0)
    * [To 1.2.1 from 1.2.0](#upgrade-1.2.1)
    * [To 1.2.0 from 1.1.2](#upgrade-1.2.0)
    * [To 1.1.2 from 1.1.1](#upgrade-1.1.2)
	* [To 1.1.1 from 1.1.0](#upgrade-1.1.1)
	* [To 1.1.0 from 1.0.4](#upgrade-1.1.0)
	
---

<a name="upgrade-guide"></a>
##Upgrade Guide

This section contains some info about what's changed in the latest version and how you should update your Vanguard application. 
You can find the version you are currently using inside `config/app.php` file.

<a name="upgrade-1.2.1"></a>
###To 1.3.0 from 1.2.1

Update to Laravel 5.4 for Vanguard has arrived. The best way to upgrade to version 1.3 is to follow [laravel upgrade guide](https://laravel.com/docs/5.4/upgrade) which will cover 99% of the things that should be updated. 

There was also one potential security issue related to avatar image upload which can be exploited on web servers where directory listing is allowed (such as default Apache configuration). To be sure that you are protected, please update `UsersController::updateAvatar` method, `ProfileController::updateAvatar` method, as well as `Vanguard\Services\Upload\UserAvatarManager` class.

There are a lot of modifications inside `tests` directory, but if you don't use automated tests to test your application, you don't have to update it.

Here is a list of modified files (except `tests`):

```
 app/Exceptions/Handler.php                                          |    2 +-
 app/Http/Controllers/ActivityController.php                         |    1 +
 app/Http/Controllers/Auth/SocialAuthController.php                  |    7 +-
 app/Http/Controllers/InstallController.php                          |    4 +-
 app/Http/Controllers/PermissionsController.php                      |    1 +
 app/Http/Controllers/ProfileController.php                          |   11 +-
 app/Http/Controllers/RolesController.php                            |    1 +
 app/Http/Controllers/SettingsController.php                         |    5 +
 app/Http/Controllers/UsersController.php                            |   15 +-
 app/Http/Middleware/SocialLogin.php                                 |    2 +-
 app/Listeners/RoleEventsSubscriber.php                              |    4 +-
 app/Providers/HtmlServiceProvider.php                               |    4 +-
 app/Repositories/Session/DbSession.php                              |    4 +
 app/Repositories/User/EloquentUser.php                              |    2 +-
 app/Services/Auth/TwoFactor/Authenticatable.php                     |    4 -
 app/Services/Upload/UserAvatarManager.php                           |   11 +-
 app/User.php                                                        |    1 -
 composer.json                                                       |   33 ++-
 config/app.php                                                      |    2 +-
 config/database.php                                                 |   15 +-
 config/mail.php                                                     |   17 ++
 database/factories/ModelFactory.php                                 |    4 +-
 gulpfile.js                                                         |   16 --
 package.json                                                        |   12 +-
 phpunit.xml                                                         |   11 +-
 resources/lang/en/app.php                                           |    4 +-
 resources/lang/sr/app.php                                           |    4 +-
 resources/views/user/profile.blade.php                              |    4 +-
 routes/web.php                                                      |  427 +++++++++++++++---------------
 webpack.mix.js                                                      |   15 ++
 75 files changed, 4470 insertions(+), 4359 deletions(-)

```

<a name="upgrade-1.2.1"></a>
###To 1.2.1 from 1.2.0

This is bug-fix release, which contains few small bug fixes and tests improvements. 

Here is the list of all modified files, and git patch is provided inside `documentation` folder in downloaded zip file:

```php
 app/Repositories/User/EloquentUser.php                        |  6 +++++-
 composer.json                                                 |  4 +---
 database/factories/ModelFactory.php                           |  2 +-
 resources/views/user/list.blade.php                           |  4 ++--
 resources/views/user/view.blade.php                           |  2 +-
 tests/TestCase.php                                            | 16 ++++++++++++++++
 tests/functional/FunctionalTestCase.php                       |  9 ++++++++-
 tests/functional/Http/Controllers/Auth/AuthControllerTest.php | 21 ++++++++++++++-------
 tests/functional/Http/Controllers/ProfileControllerTest.php   |  6 +++++-
 tests/functional/Http/Controllers/UsersControllerTest.php     | 39 +++++++++++++++++++++++++++++++++++++--
 tests/functional/Repositories/Session/DbSessionTest.php       | 15 +++++++++++----
 12 files changed, 102 insertions(+), 24 deletions(-)
```

If you don't care about automated tests, you don't have to update those files.

> Important: Don't forget to update image validation on avatar upload inside `UsersController` and `ProfileController` improve application security.

<a name="upgrade-1.2.0"></a>
###To 1.2.0 from 1.1.2

This version is mostly an upgrade to Laravel 5.3, with some other small fixes and design updates.
The best way to go through the update process is to fully follow [Laravel's upgrade guide](https://laravel.com/docs/5.3/upgrade#upgrade-5.3.0). This section inside Laravel's documentation will give you the complete idea of which files are changed and will drive you through full update process. 

The easiest way is to just overwrite the file affected by this update with the new one from the latest version. However, if you have modified some files, you will have to go through the update process manually. 

Git patch is provided inside the `documentation` folder in downloaded zip file.

**Note:** To make [Entrust](https://github.com/Zizaco/entrust) package compatible with Laravel 5.3, new EntrustServiceProvider is created inside `app/Providers`, and that service provider is now referenced inside `config/app.php` instead of original one from Entrust package.

List of modified and added files:

```php
 .gitignore                                                          |    1 +
 _ide_helper.php                                                     | 2448 ++++++++-----------------------------------
 app/Console/Commands/Inspire.php                                    |   33 +
 app/Console/Kernel.php                                              |   17 +-
 app/Exceptions/Handler.php                                          |   24 +-
 app/Http/Controllers/ActivityController.php                         |    1 -
 app/Http/Controllers/Auth/PasswordController.php                    |   18 +-
 app/Http/Controllers/InstallController.php                          |    1 -
 app/Http/Controllers/ProfileController.php                          |    6 +-
 app/Http/Controllers/UsersController.php                            |   16 +-
 app/Http/Kernel.php                                                 |    6 +-
 app/Http/routes.php                                                 |  378 +++++++
 app/Listeners/UserWasRegisteredListener.php                         |   14 +-
 app/Mailers/NotificationMailer.php                                  |   17 +
 app/Mailers/UserMailer.php                                          |    7 +-
 app/Notifications/EmailConfirmation.php                             |   54 -
 app/Notifications/ResetPassword.php                                 |   53 -
 app/Notifications/UserRegistered.php                                |   70 --
 app/Providers/AppServiceProvider.php                                |    1 -
 app/Providers/AuthServiceProvider.php                               |    5 +-
 app/Providers/BroadcastServiceProvider.php                          |   36 -
 app/Providers/EntrustServiceProvider.php                            |   62 --
 app/Providers/EventServiceProvider.php                              |    6 +-
 app/Providers/RouteServiceProvider.php                              |   59 +-
 app/Repositories/Activity/EloquentActivity.php                      |    6 +-
 app/Repositories/Country/EloquentCountry.php                        |    4 +-
 app/Repositories/Permission/EloquentPermission.php                  |    2 +-
 app/Repositories/Role/EloquentRole.php                              |    2 +-
 app/Repositories/Session/DbSession.php                              |    3 +-
 app/Repositories/User/EloquentUser.php                              |   15 +-
 app/User.php                                                        |   15 +-
 composer.json                                                       |    9 +-
 composer.lock                                                       | 1107 +++++++++----------
 config/app.php                                                      |   24 +-
 config/database.php                                                 |    1 -
 database/factories/ModelFactory.php                                 |    2 +-
 database/migrations/2015_09_19_191655_setup_countries_table.php     |    2 +-
 database/migrations/2015_10_10_170827_create_users_table.php        |    2 +-
 extra/auth.php                                                      |    6 +-
 public/assets/css/app.css                                           |   30 +-
 public/assets/js/as/app.js                                          |   42 +-
 public/assets/js/as/dashboard-admin.js                              |   12 +
 public/web.config                                                   |   23 -
 resources/lang/en/app.php                                           |   12 +-
 resources/views/layouts/app.blade.php                               |    4 +-
 resources/views/partials/sidebar.blade.php                          |    2 +-
 resources/views/settings/partials/auth.blade.php                    |    3 +-
 resources/views/user/partials/avatar.blade.php                      |    2 +-
 resources/views/vendor/notifications/email-plain.blade.php          |   22 -
 resources/views/vendor/notifications/email.blade.php                |  193 ----
 resources/views/vendor/pagination/bootstrap-4.blade.php             |   36 -
 resources/views/vendor/pagination/default.blade.php                 |   36 -
 resources/views/vendor/pagination/simple-bootstrap-4.blade.php      |   17 -
 resources/views/vendor/pagination/simple-default.blade.php          |   17 -
 routes/api.php                                                      |   12 -
 routes/console.php                                                  |   18 -
 routes/web.php                                                      |  378 -------
 storage/settings.json                                               |    2 +-
 tests/functional/FunctionalTestCase.php                             |   50 +-
 tests/functional/Http/Controllers/ActivityControllerTest.php        |    9 +-
 tests/functional/Http/Controllers/Auth/AuthControllerTest.php       |   83 +-
 tests/functional/Http/Controllers/Auth/PasswordControllerTest.php   |   38 +-
 tests/functional/Http/Controllers/Auth/SocialAuthControllerTest.php |    8 -
 tests/functional/Http/Controllers/PermissionsControllerTest.php     |    2 +-
 tests/functional/Repositories/Country/EloquentCountryTest.php       |    2 +-
 tests/functional/Repositories/Role/EloquentRoleTest.php             |    4 +-
 tests/functional/Repositories/User/EloquentUserTest.php             |    2 +-
 68 files changed, 1560 insertions(+), 4032 deletions(-)
```

<a name="upgrade-1.1.2"></a>
###To 1.1.2 from 1.1.1

Version 1.1.2 fixes missing VerifyInstallation middleware that redirects user to install page if they try to access some page when Vanguard is not installed.

List of modified files:

```php
 app/Http/Kernel.php     |   1 -    // added missing middleware
 config/app.php          |   2 +-   // updated version number
```

<a name="upgrade-1.1.1"></a>
###To 1.1.1 from 1.1.0

Version 1.1.1 contains only few bug fixes as well as **German** translation files.

Below is the list of changed and added files with some basic info about the changes:

```php
 app/Http/Controllers/Auth/SocialAuthController.php |   4 +   // check redirectToProvider method
 app/Http/Kernel.php                                |  25 +-
 app/Providers/RouteServiceProvider.php             |  17 +-
 config/app.php                                     |   2 +-  //increased Vanguard version number
 resources/views/user/list.blade.php                |   2 +-  //fix translation for "page-title" section
 resources/views/user/view.blade.php                |   2 +-  //fix translation for "Phone"

 //New files (you don't have to add them if you don't want to translate Vanguard to German):
 resources/lang/de/app.php                          | 334 +++++++++++++++++++++
 resources/lang/de/auth.php                         |  19 ++
 resources/lang/de/log.php                          |  29 ++
 resources/lang/de/pagination.php                   |  19 ++
 resources/lang/de/passwords.php                    |  22 ++
 resources/lang/de/validation.php                   | 115 +++++++
```

<a name="upgrade-1.1.0"></a>
###To 1.1.0 from 1.0.4

Version 1.1.0 comes with localization feature, which means that all strings inside Controllers and views are replaced with some kind of translatable identifier. 

The easiest way to upgrade to this version is to just overwrite all files, however, if you have already changed something inside the Vanguard's source code, this is not an option. Below is the list of all changed files inside the system (there are some new files too), so if you know that you haven't changed some of them, just overwrite them. I case you changed some file, just compare it to the latest version to see what's changed. 

```php
 app/Http/Controllers/Auth/AuthController.php                        |   32 +-
 app/Http/Controllers/Auth/PasswordController.php                    |    2 +-
 app/Http/Controllers/Auth/SocialAuthController.php                  |   12 +-
 app/Http/Controllers/PermissionsController.php                      |   19 +-
 app/Http/Controllers/ProfileController.php                          |   18 +-
 app/Http/Controllers/RolesController.php                            |    6 +-
 app/Http/Controllers/SettingsController.php                         |   10 +-
 app/Http/Controllers/UsersController.php                            |   28 +-
 app/Http/Requests/Auth/RegisterRequest.php                          |    2 +-
 app/Http/Requests/Permission/BasePermissionRequest.php              |    2 +-
 app/Listeners/PermissionEventsSubscriber.php                        |   18 +-
 app/Listeners/RoleEventsSubscriber.php                              |   20 +-
 app/Listeners/UserEventsSubscriber.php                              |   56 +--
 app/Providers/AppServiceProvider.php                                |    3 +-
 app/Repositories/Activity/EloquentActivity.php                      |    8 +-
 app/Repositories/User/EloquentUser.php                              |   10 +-
 app/Support/Enum/UserStatus.php                                     |    6 +-
 composer.json                                                       |   10 +-
 composer.lock                                                       |  645 +++++++++++++++-------------
 config/app.php                                                      |    6 +-
 config/database.php                                                 |    3 +
 config/filesystems.php                                              |    2 +-
 public/assets/js/as/dashboard-admin.js                              |    6 +-
 resources/lang/en/app.php                                           |  333 ++++++++++++++
 resources/lang/en/log.php                                           |   29 ++
 resources/lang/sr/app.php                                           |  328 ++++++++++++++
 resources/lang/sr/auth.php                                          |   19 +
 resources/lang/sr/log.php                                           |   29 ++
 resources/lang/sr/pagination.php                                    |   19 +
 resources/lang/sr/passwords.php                                     |   22 +
 resources/lang/sr/validation.php                                    |  119 +++++
 resources/views/activity/index.blade.php                            |   28 +-
 resources/views/auth/login.blade.php                                |   18 +-
 resources/views/auth/password/remind.blade.php                      |   10 +-
 resources/views/auth/password/reset.blade.php                       |   18 +-
 resources/views/auth/register.blade.php                             |   18 +-
 resources/views/auth/social/twitter-email.blade.php                 |   15 +-
 resources/views/auth/token.blade.php                                |   10 +-
 resources/views/dashboard/admin.blade.php                           |   43 +-
 resources/views/dashboard/default.blade.php                         |   18 +-
 resources/views/emails/notifications/new-registration.blade.php     |    8 +-
 resources/views/emails/password/remind.blade.php                    |   10 +-
 resources/views/emails/registration/confirmation.blade.php          |   10 +-
 resources/views/layouts/app.blade.php                               |    6 +-
 resources/views/layouts/auth.blade.php                              |    2 +-
 resources/views/partials/sidebar.blade.php                          |   21 +-
 resources/views/permission/add-edit.blade.php                       |   26 +-
 resources/views/permission/index.blade.php                          |   32 +-
 resources/views/role/add-edit.blade.php                             |   26 +-
 resources/views/role/index.blade.php                                |   32 +-
 resources/views/settings/auth.blade.php                             |   16 +-
 resources/views/settings/general.blade.php                          |   18 +-
 resources/views/settings/notifications.blade.php                    |   20 +-
 resources/views/settings/partials/auth.blade.php                    |   16 +-
 resources/views/settings/partials/recaptcha.blade.php               |   10 +-
 resources/views/settings/partials/registration.blade.php            |   16 +-
 resources/views/settings/partials/throttling.blade.php              |   15 +-
 resources/views/settings/partials/two-factor.blade.php              |   16 +-
 resources/views/user/add.blade.php                                  |   14 +-
 resources/views/user/edit.blade.php                                 |   16 +-
 resources/views/user/list.blade.php                                 |   44 +-
 resources/views/user/partials/auth.blade.php                        |   20 +-
 resources/views/user/partials/avatar.blade.php                      |   14 +-
 resources/views/user/partials/details.blade.php                     |   28 +-
 resources/views/user/partials/social-networks.blade.php             |    6 +-
 resources/views/user/partials/two-factor.blade.php                  |   19 +-
 resources/views/user/profile.blade.php                              |   14 +-
 resources/views/user/sessions.blade.php                             |   28 +-
 resources/views/user/view.blade.php                                 |   34 +-
 tests/functional/FunctionalTestCase.php                             |    4 +-
 tests/functional/Http/Controllers/Auth/SocialAuthControllerTest.php |   16 +-
 tests/functional/Http/Controllers/PermissionsControllerTest.php     |   35 +-
```