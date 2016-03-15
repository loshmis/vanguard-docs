#Upgrade Guide

* [Upgrade Guide](#upgrade-guide)
	* [To 1.1.0 from 1.0.4](#upgrade-1.1.0)
	
---

<a name="upgrade-guide"></a>
##Upgrade Guide

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
