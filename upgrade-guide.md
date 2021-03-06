#Upgrade Guide

* [Upgrade Guide](#upgrade-guide)
    * [To 4.0.0 from 3.2.1](#upgrade-4.0.0)
    * [To 3.2.1 from 3.2.0](#upgrade-3.2.1)
    * [To 3.2.0 from 3.1.0](#upgrade-3.2.0)
    * [To 3.1.0 from 3.0.1](#upgrade-3.1.0)
    * [To 3.0.1 from 3.0.0](#upgrade-3.0.1)
    * [To 3.0.0 from 2.2.0](#upgrade-3.0.0)
    * [To 2.2.0 from 2.1.1](#upgrade-2.2.0)
    * [To 2.1.1 from 2.1.0](#upgrade-2.1.1)
    * [To 2.1.0 from 2.0.2](#upgrade-2.1.0)
    * [To 2.0.2 from 2.0.1](#upgrade-2.0.2)
    * [To 2.0.1 from 2.0.0](#upgrade-2.0.1)
    * [To 2.0.0 from 1.3.3](#upgrade-2.0.0)
    * [To 1.3.3 from 1.3.2](#upgrade-1.3.3)
    * [To 1.3.2 from 1.3.1](#upgrade-1.3.2)
    * [To 1.3.1 from 1.3.0](#upgrade-1.3.1)
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
You can find the version you are currently using inside `config/app.php` file. Complete changelog is available inside the item
description [on CodeCanyon](https://codecanyon.net/item/vanguard-advanced-php-login-and-user-management/14521866).

<a name="upgrade-4.0.0"></a>
###To 4.0.0 from 3.2.1

Version 4 of Vanguard, which runs on Laravel 6, comes with a lot of improvements and, if you have any projects 
created using the previous versions of Vanguard, it's recommended to move all your modifications to a clean Vanguard 4 
installation than to upgrade your existing Vanguard version.

The reason for this is because there are a lot of changed files between Vanguard 3.2.1 and Vanguard 4, and it can 
take pretty long to update all the files to their latest versions.

Anyways, if you decide to upgrade the Vanguard manually, since there are a lot of the changes files, you will need to 
go through each file from the list of modified files available below, and compare it with the one from version 4. 
It's highly recommended to check the Git patch file that contains all the differences between those two versions. 
The patch file is located inside the `Documentation/Patches` directory and you can use any text editor to open it 
(something like [this Chrome plugin](https://chrome.google.com/webstore/detail/git-patch-viewer/hkoggakcdopbgnaeeidcmopfekipkleg) 
will also be a good option).

Modified files:
```
 .gitignore                                                                                                 |    1 +
 app/Events/User/Registered.php                                                                             |   30 -
 app/Events/User/ResetedPasswordViaEmail.php                                                                |   26 -
 app/Exceptions/Handler.php                                                                                 |    8 -
 app/Http/Controllers/Api/ActivityController.php                                                            |   39 -
 app/Http/Controllers/Api/Auth/AuthController.php                                                           |   10 +-
 app/Http/Controllers/Api/Auth/Password/RemindController.php                                                |    4 +-
 app/Http/Controllers/Api/Auth/Password/ResetController.php                                                 |   10 +-
 app/Http/Controllers/Api/Auth/RegistrationController.php                                                   |   19 +-
 app/Http/Controllers/Api/Auth/SocialLoginController.php                                                    |    2 +-
 app/Http/Controllers/Api/Profile/AvatarController.php                                                      |    1 -
 app/Http/Controllers/Api/SessionsController.php                                                            |    2 +
 app/Http/Controllers/Api/SettingsController.php                                                            |    4 +-
 app/Http/Controllers/Api/StatsController.php                                                               |   43 +-
 app/Http/Controllers/Api/Users/AvatarController.php                                                        |   30 +-
 app/Http/Controllers/Api/Users/UsersController.php                                                         |    7 +-
 app/Http/Controllers/Web/ActivityController.php                                                            |   68 --
 app/Http/Controllers/Web/Auth/AuthController.php                                                           |  374 -------
 app/Http/Controllers/Web/Auth/ForgotPasswordController.php                                                 |   45 +
 app/Http/Controllers/Web/Auth/LoginController.php                                                          |  150 +++
 app/Http/Controllers/Web/Auth/PasswordController.php                                                       |  113 --
 app/Http/Controllers/Web/Auth/RegisterController.php                                                       |   63 ++
 app/Http/Controllers/Web/Auth/ResetPasswordController.php                                                  |   61 +
 app/Http/Controllers/Web/Auth/SocialAuthController.php                                                     |   25 +-
 app/Http/Controllers/Web/Auth/TwoFactorTokenController.php                                                 |   75 ++
 app/Http/Controllers/Web/Auth/VerificationController.php                                                   |   41 +
 app/Http/Controllers/Web/{ => Authorization}/PermissionsController.php                                     |   74 +-
 app/Http/Controllers/Web/Authorization/RolePermissionsController.php                                       |   53 +
 app/Http/Controllers/Web/{ => Authorization}/RolesController.php                                           |   43 +-
 app/Http/Controllers/Web/DashboardController.php                                                           |   78 +-
 app/Http/Controllers/Web/InstallController.php                                                             |   14 +-
 app/Http/Controllers/Web/Profile/AvatarController.php                                                      |   85 ++
 app/Http/Controllers/Web/Profile/DetailsController.php                                                     |   45 +
 app/Http/Controllers/Web/Profile/LoginDetailsController.php                                                |   51 +
 app/Http/Controllers/Web/Profile/ProfileController.php                                                     |   64 ++
 app/Http/Controllers/Web/Profile/SessionsController.php                                                    |   52 +
 app/Http/Controllers/Web/ProfileController.php                                                             |  224 ----
 app/Http/Controllers/Web/SettingsController.php                                                            |   36 +-
 app/Http/Controllers/Web/TwoFactorController.php                                                           |   10 +-
 app/Http/Controllers/Web/Users/AvatarController.php                                                        |   83 ++
 app/Http/Controllers/Web/Users/DetailsController.php                                                       |   76 ++
 app/Http/Controllers/Web/Users/LoginDetailsController.php                                                  |   54 +
 app/Http/Controllers/Web/Users/SessionsController.php                                                      |   62 +
 app/Http/Controllers/Web/Users/UsersController.php                                                         |  163 +++
 app/Http/Controllers/Web/UsersController.php                                                               |  326 ------
 app/Http/Kernel.php                                                                                        |   34 +-
 app/Http/Middleware/EncryptCookies.php                                                                     |    2 +-
 app/Http/Middleware/{Registration.php => PasswordResetEnabled.php}                                         |    6 +-
 app/Http/Middleware/RegistrationEnabled.php                                                                |   25 +
 app/Http/Middleware/TwoFactorEnabled.php                                                                   |   25 +
 app/Http/Requests/Activity/GetActivitiesRequest.php                                                        |   28 -
 app/Http/Requests/Auth/PasswordResetRequest.php                                                            |   10 +
 app/Http/Requests/Auth/RegisterRequest.php                                                                 |   31 +-
 app/Http/Requests/Permission/BasePermissionRequest.php                                                     |    8 +-
 app/Http/Requests/Permission/CreatePermissionRequest.php                                                   |    9 +-
 app/Http/Requests/Permission/RemovePermissionRequest.php                                                   |    3 +
 app/Http/Requests/Permission/UpdatePermissionRequest.php                                                   |   11 +-
 app/Http/Requests/User/CreateUserRequest.php                                                               |    1 +
 app/Listeners/PermissionEventsSubscriber.php                                                               |   66 --
 app/Listeners/Registration/SendConfirmationEmail.php                                                       |   43 -
 app/Listeners/Registration/SendSignUpNotification.php                                                      |    8 +-
 app/Listeners/RoleEventsSubscriber.php                                                                     |   72 --
 app/Listeners/UserEventsSubscriber.php                                                                     |  204 ----
 app/Mail/ResetPassword.php                                                                                 |   37 +
 app/Mail/UserRegistered.php                                                                                |   41 +
 app/Notifications/EmailConfirmation.php                                                                    |   54 -
 app/Notifications/ResetPassword.php                                                                        |   53 -
 app/Notifications/UserRegistered.php                                                                       |   70 --
 app/Presenters/Presenter.php                                                                               |   46 +
 app/Presenters/Traits/Presentable.php                                                                      |   26 +
 app/Presenters/UserPresenter.php                                                                           |   25 +-
 app/Providers/AppServiceProvider.php                                                                       |    5 +-
 app/Providers/EventServiceProvider.php                                                                     |   13 +-
 app/Providers/VanguardServiceProvider.php                                                                  |   52 +
 app/Repositories/Activity/ActivityRepository.php                                                           |   59 -
 app/Repositories/Activity/EloquentActivity.php                                                             |   98 --
 app/Rules/ValidPermissionName.php                                                                          |   44 +
 app/Services/Auth/Api/TokenFactory.php                                                                     |    2 +
 app/Services/Auth/ThrottlesLogins.php                                                                      |   81 ++
 app/Services/Logging/UserActivity/Activity.php                                                             |   20 -
 app/Services/Logging/UserActivity/Logger.php                                                               |   86 --
 app/Services/Upload/UserAvatarManager.php                                                                  |   89 +-
 app/Support/Enum/UserStatus.php                                                                            |    6 +-
 app/Support/Plugins/Dashboard/Dashboard.php                                                                |   17 +
 app/Support/Plugins/Dashboard/Widgets/BannedUsers.php                                                      |   44 +
 app/Support/Plugins/Dashboard/Widgets/LatestRegistrations.php                                              |   43 +
 app/Support/Plugins/Dashboard/Widgets/NewUsers.php                                                         |   43 +
 app/Support/Plugins/Dashboard/Widgets/RegistrationHistory.php                                              |   71 ++
 app/Support/Plugins/Dashboard/Widgets/TotalUsers.php                                                       |   43 +
 app/Support/Plugins/Dashboard/Widgets/UnconfirmedUsers.php                                                 |   44 +
 app/Support/Plugins/Dashboard/Widgets/UserActions.php                                                      |   27 +
 app/Support/Plugins/RolesAndPermissions.php                                                                |   31 +
 app/Support/Plugins/Settings.php                                                                           |   40 +
 app/Support/Plugins/Users.php                                                                              |   18 +
 app/Support/Sidebar/Item.php                                                                               |  249 +++++
 app/Support/helpers.php                                                                                    |   21 -
 app/Transformers/ActivityTransformer.php                                                                   |   36 -
 app/Transformers/UserTransformer.php                                                                       |    3 +-
 app/User.php                                                                                               |   38 +-
 composer.json                                                                                              |   56 +-
 composer.lock                                                                                              | 2847 +-
 config/app.php                                                                                             |   19 +-
 config/broadcasting.php                                                                                    |    3 +-
 config/cache.php                                                                                           |   13 +-
 config/database.php                                                                                        |   48 +-
 config/logging.php                                                                                         |   17 +-
 config/mail.php                                                                                            |   11 +
 config/plugins.php                                                                                         |   21 +
 config/queue.php                                                                                           |   10 +-
 config/services.php                                                                                        |   10 +-
 config/session.php                                                                                         |    4 +-
 config/setting.php                                                                                         |   85 ++
 config/settings.php                                                                                        |   17 -
 database/factories/ActivityFactory.php                                                                     |   15 -
 database/factories/RoleFactory.php                                                                         |    2 +-
 database/factories/UserFactory.php                                                                         |    5 +-
 database/migrations/2014_10_12_100000_create_password_resets_table.php                                     |    4 +-
 database/migrations/2015_08_25_172600_create_settings_table.php                                            |   42 -
 database/migrations/2015_10_10_170827_create_users_table.php                                               |    2 +-
 database/migrations/2015_12_29_224252_create_user_activity_table.php                                       |    2 +
 database/migrations/2017_08_24_000000_create_settings_table.php                                            |   41 +
 database/migrations/2019_08_22_140712_create_announcements_table.php                                       |   50 +
 database/seeds/UserSeeder.php                                                                              |    3 +-
 package-lock.json                                                                                          | 5165 +-
 phpunit.xml                                                                                                |    3 +
 public/assets/css/app.css                                                                                  |    2 +-
 public/assets/js/as/app.js                                                                                 |   14 +-
 public/mix-manifest.json                                                                                   |    2 +-
 public/vendor/plugins/announcements/css/announcements.css                                                  |    1 +
 public/vendor/plugins/announcements/js/announcements.js                                                    |    1 +
 public/vendor/plugins/announcements/mix-manifest.json                                                      |    4 +
 resources/lang/de.json                                                                                     |  242 ++++
 resources/lang/de/app.php                                                                                  |  328 +-----
 resources/lang/de/log.php                                                                                  |   32 -
 resources/lang/en/app.php                                                                                  |  331 +-----
 resources/lang/en/log.php                                                                                  |   32 -
 resources/lang/sr.json                                                                                     |  242 ++++
 resources/lang/sr/app.php                                                                                  |  335 +-----
 resources/lang/sr/log.php                                                                                  |   32 -
 resources/sass/_variables.scss                                                                             |   12 +-
 resources/sass/app.scss                                                                                    |    2 +-
 resources/sass/components/card.scss                                                                        |   29 +-
 resources/sass/components/general.scss                                                                     |   12 +-
 resources/sass/components/input.scss                                                                       |    9 +-
 resources/sass/components/navbar.scss                                                                      |   98 +-
 resources/sass/components/sidebar.scss                                                                     |  279 +++--
 resources/sass/components/util.scss                                                                        |   16 +
 resources/views/activity/index.blade.php                                                                   |  100 --
 resources/views/auth/login.blade.php                                                                       |   40 +-
 resources/views/auth/{password/remind.blade.php => passwords/email.blade.php}                              |   26 +-
 resources/views/auth/{password => passwords}/reset.blade.php                                               |   43 +-
 resources/views/auth/register.blade.php                                                                    |   90 +-
 resources/views/auth/token.blade.php                                                                       |   18 +-
 resources/views/auth/tos.blade.php                                                                         |   24 +
 resources/views/auth/verify.blade.php                                                                      |   30 +
 resources/views/dashboard/admin.blade.php                                                                  |  147 +--
 resources/views/dashboard/default.blade.php                                                                |  102 --
 resources/views/emails/notifications/new-registration.blade.php                                            |   10 -
 resources/views/emails/password/remind.blade.php                                                           |   12 -
 resources/views/emails/registration/confirmation.blade.php                                                 |   13 -
 resources/views/errors/403.blade.php                                                                       |    8 -
 resources/views/errors/404.blade.php                                                                       |   12 -
 resources/views/errors/500.blade.php                                                                       |   10 -
 resources/views/errors/503.blade.php                                                                       |    8 -
 resources/views/layouts/app.blade.php                                                                      |   10 +-
 resources/views/layouts/auth.blade.php                                                                     |    5 +-
 resources/views/layouts/errors.blade.php                                                                   |   35 -
 resources/views/layouts/install.blade.php                                                                  |    2 +-
 resources/views/mail/reset-password.blade.php                                                              |   22 +
 resources/views/mail/user-registered.blade.php                                                             |   19 +
 resources/views/partials/navbar.blade.php                                                                  |   33 +-
 resources/views/partials/sidebar.blade.php                                                                 |  122 --
 resources/views/partials/sidebar/items.blade.php                                                           |   26 +
 resources/views/partials/sidebar/main.blade.php                                                            |   37 +
 resources/views/permission/add-edit.blade.php                                                              |   46 +-
 resources/views/permission/index.blade.php                                                                 |   34 +-
 resources/views/plugins/dashboard/widgets/banned-users.blade.php                                           |   14 +
 resources/views/plugins/dashboard/widgets/latest-registrations.blade.php                                   |   31 +
 resources/views/plugins/dashboard/widgets/new-users.blade.php                                              |   14 +
 resources/views/plugins/dashboard/widgets/registration-history-scripts.blade.php                           |   12 +
 resources/views/plugins/dashboard/widgets/registration-history.blade.php                                   |   11 +
 resources/views/plugins/dashboard/widgets/total-users.blade.php                                            |   14 +
 resources/views/plugins/dashboard/widgets/unconfirmed-users.blade.php                                      |   14 +
 resources/views/plugins/dashboard/widgets/user-actions.blade.php                                           |   53 +
 resources/views/role/add-edit.blade.php                                                                    |   46 +-
 resources/views/role/index.blade.php                                                                       |   34 +-
 resources/views/settings/auth.blade.php                                                                    |   12 +-
 resources/views/settings/general.blade.php                                                                 |   18 +-
 resources/views/settings/notifications.blade.php                                                           |   30 +-
 resources/views/settings/partials/auth.blade.php                                                           |   35 +-
 resources/views/settings/partials/recaptcha.blade.php                                                      |   24 +-
 resources/views/settings/partials/registration.blade.php                                                   |   31 +-
 resources/views/settings/partials/throttling.blade.php                                                     |   39 +-
 resources/views/settings/partials/two-factor.blade.php                                                     |   29 +-
 resources/views/user/add.blade.php                                                                         |   20 +-
 resources/views/user/edit.blade.php                                                                        |   60 +-
 resources/views/user/list.blade.php                                                                        |   41 +-
 resources/views/user/partials/auth.blade.php                                                               |   46 +-
 resources/views/user/partials/avatar.blade.php                                                             |   31 +-
 resources/views/user/partials/details.blade.php                                                            |   42 +-
 resources/views/user/partials/row.blade.php                                                                |   35 +-
 resources/views/user/partials/two-factor.blade.php                                                         |   40 +-
 resources/views/user/profile.blade.php                                                                     |   58 +-
 resources/views/user/sessions.blade.php                                                                    |   34 +-
 resources/views/user/two-factor-verification.blade.php                                                     |   25 +-
 resources/views/user/view.blade.php                                                                        |   99 +-
 resources/views/vendor/mail/html/button.blade.php                                                          |   19 +
 resources/views/vendor/mail/html/footer.blade.php                                                          |   11 +
 resources/views/vendor/mail/html/header.blade.php                                                          |    7 +
 resources/views/vendor/mail/html/layout.blade.php                                                          |   54 +
 resources/views/vendor/mail/html/message.blade.php                                                         |   27 +
 resources/views/vendor/mail/html/panel.blade.php                                                           |   13 +
 resources/views/vendor/mail/html/promotion.blade.php                                                       |    7 +
 resources/views/vendor/mail/html/promotion/button.blade.php                                                |   13 +
 resources/views/vendor/mail/html/subcopy.blade.php                                                         |    7 +
 resources/views/vendor/mail/html/table.blade.php                                                           |    3 +
 resources/views/vendor/mail/html/themes/default.css                                                        |  307 +++++
 resources/views/vendor/mail/text/button.blade.php                                                          |    1 +
 resources/views/vendor/mail/text/footer.blade.php                                                          |    1 +
 resources/views/vendor/mail/text/header.blade.php                                                          |    1 +
 resources/views/vendor/mail/text/layout.blade.php                                                          |    9 +
 resources/views/vendor/mail/text/message.blade.php                                                         |   27 +
 resources/views/vendor/mail/text/panel.blade.php                                                           |    1 +
 resources/views/vendor/mail/text/promotion.blade.php                                                       |    1 +
 resources/views/vendor/mail/text/promotion/button.blade.php                                                |    1 +
 resources/views/vendor/mail/text/subcopy.blade.php                                                         |    1 +
 resources/views/vendor/mail/text/table.blade.php                                                           |    1 +
 resources/views/vendor/notifications/email.blade.php                                                       |    6 +-
 routes/api.php                                                                                             |   16 +-
 routes/web.php                                                                                             |  458 +++-----
 storage/app/.gitignore                                                                                     |    0
 storage/framework/.gitignore                                                                               |    1 +
 storage/settings.json                                                                                      |    2 +-
 tests/CreatesApplication.php                                                                               |   24 +
 tests/Feature/Api/Auth/AuthControllerTest.php                                                              |  162 +++
 tests/Feature/Api/Auth/Password/RemindControllerTest.php                                                   |   38 +
 tests/Feature/{Http/Controllers => }/Api/Auth/Password/ResetControllerTest.php                             |   46 +-
 tests/Feature/Api/Auth/RegistrationControllerTest.php                                                      |  104 ++
 tests/Feature/{Http/Controllers => }/Api/Auth/SocialLoginControllerTest.php                                |   69 +-
 tests/Feature/Api/Authorization/PermissionsControllerTest.php                                              |  161 +++
 tests/Feature/{Http/Controllers => }/Api/Authorization/RolePermissionsControllerTest.php                   |   56 +-
 tests/Feature/Api/Authorization/RolesControllerTest.php                                                    |  176 +++
 tests/Feature/{Http/Controllers => }/Api/CountriesControllerTest.php                                       |   16 +-
 tests/Feature/Api/Profile/AuthDetailsControllerTest.php                                                    |   83 ++
 tests/Feature/{Http/Controllers => }/Api/Profile/AvatarControllerTest.php                                  |   74 +-
 tests/Feature/Api/Profile/DetailsControllerTest.php                                                        |  123 ++
 tests/Feature/{Http/Controllers => }/Api/Profile/SessionsControllerTest.php                                |   19 +-
 tests/Feature/{Http/Controllers => }/Api/Profile/TwoFactorControllerTest.php                               |  119 +-
 tests/Feature/{Http/Controllers => }/Api/SessionsControllerTest.php                                        |   61 +-
 tests/Feature/Api/SettingsControllerTest.php                                                               |   38 +
 tests/Feature/{Http/Controllers => }/Api/StatsControllerTest.php                                           |   53 +-
 tests/Feature/Api/Users/AvatarControllerTest.php                                                           |  147 +++
 tests/Feature/{Http/Controllers => }/Api/Users/SessionsControllerTest.php                                  |   26 +-
 tests/Feature/Api/Users/TwoFactorControllerTest.php                                                        |  170 +++
 tests/Feature/{Http/Controllers => }/Api/Users/UsersControllerTest.php                                     |  127 ++-
 tests/Feature/ApiTestCase.php                                                                              |   22 +-
 tests/Feature/FunctionalTestCase.php                                                                       |  203 ----
 tests/Feature/Http/Controllers/Api/ActivityControllerTest.php                                              |  118 --
 tests/Feature/Http/Controllers/Api/Auth/AuthControllerTest.php                                             |  163 ---
 tests/Feature/Http/Controllers/Api/Auth/Password/RemindControllerTest.php                                  |   44 -
 tests/Feature/Http/Controllers/Api/Auth/RegistrationControllerTest.php                                     |  122 --
 tests/Feature/Http/Controllers/Api/Authorization/PermissionsControllerTest.php                             |  190 ----
 tests/Feature/Http/Controllers/Api/Authorization/RolesControllerTest.php                                   |  203 ----
 tests/Feature/Http/Controllers/Api/Profile/AuthDetailsControllerTest.php                                   |   88 --
 tests/Feature/Http/Controllers/Api/Profile/DetailsControllerTest.php                                       |  125 ---
 tests/Feature/Http/Controllers/Api/SettingsControllerTest.php                                              |   37 -
 tests/Feature/Http/Controllers/Api/Users/ActivityControllerTest.php                                        |  109 --
 tests/Feature/Http/Controllers/Api/Users/AvatarControllerTest.php                                          |  154 ---
 tests/Feature/Http/Controllers/Api/Users/TwoFactorControllerTest.php                                       |  196 ----
 tests/Feature/Http/Controllers/Web/ActivityControllerTest.php                                              |   83 --
 tests/Feature/Http/Controllers/Web/Auth/AuthControllerTest.php                                             |  438 --------
 tests/Feature/Http/Controllers/Web/Auth/PasswordControllerTest.php                                         |  159 ---
 tests/Feature/Http/Controllers/Web/PermissionsControllerTest.php                                           |  181 ---
 tests/Feature/Http/Controllers/Web/ProfileControllerTest.php                                               |  266 -----
 tests/Feature/Http/Controllers/Web/RolesControllerTest.php                                                 |  138 ---
 tests/Feature/Http/Controllers/Web/SettingsControllerTest.php                                              |   34 -
 tests/Feature/Http/Controllers/Web/UsersControllerTest.php                                                 |  464 --------
 tests/Feature/ImpersonateUsersTest.php                                                                     |   96 --
 tests/Feature/Listeners/BaseListenerTestCase.php                                                           |   29 -
 tests/Feature/Listeners/PermissionEventsSubscriberTest.php                                                 |   38 -
 tests/Feature/Listeners/RoleEventsSubscriberTest.php                                                       |   44 -
 tests/Feature/Listeners/UserEventsSubscriberTest.php                                                       |  178 ---
 tests/Feature/Repositories/Activity/EloquentActivityTest.php                                               |  128 ---
 tests/Feature/Repositories/Role/EloquentRoleTest.php                                                       |  108 --
 tests/Feature/Web/ImpersonateUsersTest.php                                                                 |   91 ++
 tests/Feature/Web/LoginTest.php                                                                            |  177 +++
 tests/Feature/Web/PermissionsTest.php                                                                      |  348 ++++++
 tests/Feature/Web/RegistrationTest.php                                                                     |  172 +++
 tests/Feature/Web/RolesTest.php                                                                            |  234 ++++
 tests/Feature/Web/Settings/AuthSettingsTest.php                                                            |  105 ++
 tests/Feature/Web/Settings/CaptchaSettingsTest.php                                                         |   49 +
 tests/Feature/Web/Settings/GeneralSettingsTest.php                                                         |   62 +
 tests/Feature/Web/Settings/TwoFactorSettingsTest.php                                                       |   49 +
 tests/Feature/Web/SettingsTest.php                                                                         |  137 +++
 tests/Feature/{Http/Controllers/Web/Auth/SocialAuthControllerTest.php => Web/SocialAuthenticationTest.php} |  141 +--
 tests/Feature/{Http/Controllers/Web/TwoFactorControllerTest.php => Web/TwoFactorAuthTest.php}              |  276 ++---
 tests/Feature/Web/UpdateProfileTest.php                                                                    |  251 +++++
 tests/Feature/Web/UsersTest.php                                                                            |  710 ++++++++++++
 tests/Setup/RoleFactory.php                                                                                |   47 +
 tests/Setup/UserFactory.php                                                                                |   95 ++
 tests/TestCase.php                                                                                         |   65 +-
 tests/{unit => Unit}/Presenters/UserPresenterTest.php                                                      |   31 +-
 tests/{Feature => Unit}/Repositories/Country/EloquentCountryTest.php                                       |   15 +-
 tests/{Feature => Unit}/Repositories/Permission/EloquentPermissionTest.php                                 |   29 +-
 tests/Unit/Repositories/Role/EloquentRoleTest.php                                                          |  117 ++
 tests/{Feature => Unit}/Repositories/Session/DbSessionTest.php                                             |   32 +-
 tests/{Feature => Unit}/Repositories/User/EloquentUserTest.php                                             |  195 ++--
 tests/{Feature => Unit}/Services/Auth/Api/TokenFactoryTest.php                                             |   37 +-
 tests/UpdatesSettings.php                                                                                  |   22 +
 tests/files/.DS_Store                                                                                      |  Bin 6148 -> 0 bytes
 tests/files/image.png                                                                                      |  Bin 38306 -> 0 bytes
 312 files changed, 15667 insertions(+), 16557 deletions(-)
```

<a name="upgrade-3.2.1"></a>
###To 3.2.1 from 3.2.0

Installation bugs fixed. The list of modified files is given below:

```
 app/Http/Controllers/Web/InstallController.php | 3 ++-
 config/app.php                                 | 2 +-
 2 files changed, 3 insertions(+), 2 deletions(-)
```

<a name="upgrade-3.2.0"></a>
###To 3.2.0 from 3.1.0

Vanguard's codebase has been upgraded to Laravel 5.8. The recommended way to upgrade your application is to make sure 
that your `composer.json` file matches the `composer.json` file from this release. Once you update your `composer.json` 
file, just run `composer update` to install those packages, and then you can go through the list of changed files 
inside the list below and make sure that they match the files from this release.

Below is the list of updated files:

```
 app/Http/Controllers/Web/Auth/AuthController.php                         |    7 +-
 app/Http/Controllers/Web/PermissionsController.php                       |    3 +-
 app/Http/Controllers/Web/ProfileController.php                           |   24 +-
 app/Http/Controllers/Web/UsersController.php                             |    5 +-
 app/Http/Requests/Auth/LoginRequest.php                                  |    2 +
 app/Http/Requests/Auth/PasswordResetRequest.php                          |    2 +-
 app/Http/Requests/Auth/RegisterRequest.php                               |    2 +-
 app/Http/Requests/BinaryFileUploadRequest.php                            |    5 +-
 app/Http/Requests/User/UpdateLoginDetailsRequest.php                     |    2 +-
 app/Listeners/Registration/SendConfirmationEmail.php                     |    3 +-
 app/Providers/HtmlServiceProvider.php                                    |    8 +-
 app/Repositories/Role/EloquentRole.php                                   |    2 -
 app/Services/Auth/Api/TokenFactory.php                                   |    3 +-
 app/Services/Auth/Social/SocialManager.php                               |    3 +-
 app/Services/Upload/UserAvatarManager.php                                |    5 +-
 app/Support/Authorization/AuthorizationRoleTrait.php                     |    3 +-
 composer.json                                                            |   14 +-
 composer.lock                                                            | 1216 ++++++++++++--------
 config/app.php                                                           |    2 +-
 config/cache.php                                                         |   10 +-
 database/factories/PermissionFactory.php                                 |    3 +-
 database/factories/RoleFactory.php                                       |    3 +-
 database/factories/TokenFactory.php                                      |    3 +-
 database/factories/UserFactory.php                                       |    3 +-
 phpunit.xml                                                              |    1 +
 resources/lang/de/passwords.php                                          |    2 +-
 resources/lang/en/passwords.php                                          |    2 +-
 resources/lang/sr/passwords.php                                          |    2 +-
 tests/Feature/ApiTestCase.php                                            |    7 -
 tests/Feature/FunctionalTestCase.php                                     |    2 +-
 tests/Feature/Http/Controllers/Api/Auth/Password/ResetControllerTest.php |    6 +-
 tests/Feature/Http/Controllers/Api/Auth/RegistrationControllerTest.php   |   12 +-
 tests/Feature/Http/Controllers/Api/Profile/AuthDetailsControllerTest.php |    6 +-
 tests/Feature/Http/Controllers/Api/Profile/SessionsControllerTest.php    |   13 +-
 tests/Feature/Http/Controllers/Api/SessionsControllerTest.php            |    7 +-
 tests/Feature/Http/Controllers/Api/Users/SessionsControllerTest.php      |    9 +-
 tests/Feature/Http/Controllers/Web/ActivityControllerTest.php            |    2 +-
 tests/Feature/Http/Controllers/Web/Auth/AuthControllerTest.php           |    7 +-
 tests/Feature/Http/Controllers/Web/Auth/PasswordControllerTest.php       |    6 +-
 tests/Feature/Http/Controllers/Web/PermissionsControllerTest.php         |    2 +-
 tests/Feature/Http/Controllers/Web/ProfileControllerTest.php             |   35 +-
 tests/Feature/Http/Controllers/Web/RolesControllerTest.php               |    2 +-
 tests/Feature/Http/Controllers/Web/UsersControllerTest.php               |   25 +-
 tests/Feature/Listeners/BaseListenerTestCase.php                         |    2 +-
 tests/Feature/Listeners/PermissionEventsSubscriberTest.php               |    2 +-
 tests/Feature/Listeners/RoleEventsSubscriberTest.php                     |    2 +-
 tests/Feature/Listeners/UserEventsSubscriberTest.php                     |    2 +-
 tests/Feature/Repositories/Activity/EloquentActivityTest.php             |    2 +-
 tests/Feature/Repositories/Country/EloquentCountryTest.php               |    2 +-
 tests/Feature/Repositories/Permission/EloquentPermissionTest.php         |   11 +-
 tests/Feature/Repositories/Role/EloquentRoleTest.php                     |    2 +-
 tests/Feature/Repositories/Session/DbSessionTest.php                     |    9 +-
 tests/Feature/Repositories/User/EloquentUserTest.php                     |    9 +-
 tests/unit/Presenters/UserPresenterTest.php                              |    2 +-
 55 files changed, 5408 insertions(+), 3309 deletions(-)
```

<a name="upgrade-3.1.0"></a>
###To 3.1.0 from 3.0.1

Vanguard's codebase has been upgraded to Laravel 5.7. The recommended way to upgrade your application is to make sure 
that your `composer.json` file matches the `composer.json` 
file from this release. Once you update your `composer.json` file, just run `composer update` to install those packages,
and then you can go through the list of changed files inside the list below and make sure that they match
the files from this release. 

Two-Factor Authentication has been improved in this version and all users who want to activate 2FA will receive the
phone confirmation SMS first. The reason for this update is to prevent users from locking their accounts and using wrong
phone number.

Below is the list of updated files:

```
 .editorconfig                                                             |   15 +
 .env.example                                                              |   26 +-
 .gitattributes                                                            |    1 +
 .gitignore                                                                |   14 +-
 app/Console/Kernel.php                                                    |   11 +-
 app/Exceptions/Handler.php                                                |   29 +-
 app/Http/Controllers/Api/Profile/TwoFactorController.php                  |   32 +-
 app/Http/Controllers/Api/Users/TwoFactorController.php                    |   37 +-
 app/Http/Controllers/Web/ProfileController.php                            |   56 +--
 app/Http/Controllers/Web/TwoFactorController.php                          |  137 +++++++
 app/Http/Controllers/Web/UsersController.php                              |   55 +--
 app/Http/Kernel.php                                                       |    1 +
 app/Http/Middleware/VerifyTwoFactorPhone.php                              |   42 +++
 app/Http/Requests/TwoFactor/DisableTwoFactorRequest.php                   |   11 +
 app/Http/Requests/{User => TwoFactor}/EnableTwoFactorRequest.php          |    7 +-
 app/Http/Requests/TwoFactor/ReSendTwoFactorTokenRequest.php               |    7 +
 app/Http/Requests/TwoFactor/TwoFactorRequest.php                          |   48 +++
 app/Http/Requests/TwoFactor/VerifyTwoFactorTokenRequest.php               |   18 +
 app/Jobs/Job.php                                                          |   21 --
 app/Listeners/UserEventsSubscriber.php                                    |   28 ++
 app/Policies/.gitkeep                                                     |    0
 app/Services/Auth/TwoFactor/Authy.php                                     |   20 +-
 app/Services/Auth/TwoFactor/Contracts/Provider.php                        |    7 +
 app/Support/CanImpersonateUsers.php                                       |   28 ++
 app/Transformers/UserTransformer.php                                      |    4 +-
 app/User.php                                                              |    4 +-
 composer.json                                                             |   26 +-
 composer.lock                                                             | 1686 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++---------------------------
 config/app.php                                                            |    5 +-
 config/database.php                                                       |   21 +-
 config/filesystems.php                                                    |   38 +-
 config/hashing.php                                                        |   34 +-
 config/logging.php                                                        |   13 +-
 config/mail.php                                                           |    8 +-
 config/queue.php                                                          |   23 +-
 config/services.php                                                       |    4 +
 config/session.php                                                        |    4 +-
 database/migrations/2015_12_29_224252_create_user_activity_table.php      |    8 +-
 database/migrations/2015_12_30_171734_add_foreign_keys.php                |   16 +-
 database/migrations/2017_04_13_200254_create_api_tokens_table.php         |    8 +-
 phpunit.xml                                                               |    4 +-
 public/assets/css/app.css                                                 |    2 +-
 public/assets/js/as/two-factor.js                                         |   36 ++
 public/mix-manifest.json                                                  |    2 +-
 public/svg/403.svg                                                        |    1 +
 public/svg/404.svg                                                        |    1 +
 public/svg/500.svg                                                        |    1 +
 public/svg/503.svg                                                        |    1 +
 readme.md                                                                 |    4 +
 resources/{assets => }/js/app.js                                          |    0
 resources/{assets => }/js/bootstrap.js                                    |    0
 resources/{assets => }/js/components/Example.vue                          |    0
 resources/lang/de/app.php                                                 |   14 +-
 resources/lang/de/log.php                                                 |    5 +-
 resources/lang/en/app.php                                                 |   14 +-
 resources/lang/en/log.php                                                 |    5 +-
 resources/lang/sr/app.php                                                 |   14 +-
 resources/lang/sr/log.php                                                 |    5 +-
 resources/{assets => }/sass/_variables.scss                               |    0
 resources/{assets => }/sass/app.scss                                      |    2 +-
 resources/{assets => }/sass/components/avatar.scss                        |    0
 resources/{assets => }/sass/components/button.scss                        |    0
 resources/{assets => }/sass/components/card.scss                          |    4 +
 resources/{assets => }/sass/components/datepicker.scss                    |    0
 resources/{assets => }/sass/components/general.scss                       |    0
 resources/{assets => }/sass/components/input.scss                         |    0
 resources/{assets => }/sass/components/list-group.scss                    |    0
 resources/{assets => }/sass/components/nav-tabs.scss                      |    0
 resources/{assets => }/sass/components/navbar.scss                        |    0
 resources/{assets => }/sass/components/sidebar.scss                       |    0
 resources/{assets => }/sass/components/sweet-alert.scss                   |    0
 resources/{assets => }/sass/components/switch.scss                        |    0
 resources/{assets => }/sass/components/table.scss                         |    0
 resources/{assets => }/sass/components/util.scss                          |    0
 resources/views/auth/token.blade.php                                      |    4 +-
 resources/views/partials/navbar.blade.php                                 |   15 +
 resources/views/settings/notifications.blade.php                          |    2 +
 resources/views/user/edit.blade.php                                       |    5 +-
 resources/views/user/partials/row.blade.php                               |    7 +
 resources/views/user/profile.blade.php                                    |    4 +-
 resources/views/user/two-factor-verification.blade.php                    |   69 ++++
 resources/views/user/view.blade.php                                       |    8 +
 routes/api.php                                                            |    2 +
 routes/channels.php                                                       |   16 +
 routes/web.php                                                            |   51 ++-
 storage/framework/cache/.gitignore                                        |    1 +
 storage/framework/cache/data/.gitignore                                   |    2 +
 storage/settings.json                                                     |    2 +-
 tests/Feature/FunctionalTestCase.php                                      |   16 +-
 tests/Feature/Http/Controllers/Api/Auth/AuthControllerTest.php            |    4 -
 tests/Feature/Http/Controllers/Api/Auth/Password/RemindControllerTest.php |   41 +--
 tests/Feature/Http/Controllers/Api/Auth/Password/ResetControllerTest.php  |    3 -
 tests/Feature/Http/Controllers/Api/Auth/RegistrationControllerTest.php    |   45 ++-
 tests/Feature/Http/Controllers/Api/Profile/TwoFactorControllerTest.php    |   63 +++-
 tests/Feature/Http/Controllers/Api/Users/TwoFactorControllerTest.php      |   63 +++-
 tests/Feature/Http/Controllers/Api/Users/UsersControllerTest.php          |   39 +-
 tests/Feature/Http/Controllers/Web/Auth/AuthControllerTest.php            |  106 +++---
 tests/Feature/Http/Controllers/Web/Auth/PasswordControllerTest.php        |   32 +-
 tests/Feature/Http/Controllers/Web/Auth/SocialAuthControllerTest.php      |    1 -
 tests/Feature/Http/Controllers/Web/ProfileControllerTest.php              |   65 ----
 tests/Feature/Http/Controllers/Web/TwoFactorControllerTest.php            |  411 +++++++++++++++++++++
 tests/Feature/Http/Controllers/Web/UsersControllerTest.php                |   48 ---
 tests/Feature/ImpersonateUsersTest.php                                    |   96 +++++
 tests/Feature/Listeners/UserEventsSubscriberTest.php                      |   28 +-
 tests/MailTrap.php                                                        |  131 -------
 webpack.mix.js                                                            |    2 +-
 107 files changed, 4917 insertions(+), 1473 deletions(-)
```

<a name="upgrade-3.0.1"></a>
###To 3.0.1 from 3.0.0

Version 3.0.1 is a bug-fix release where some minor (mostly UI related) bugs that are reported by customers are fixed. The main
bug fixed was the one where assets were not being loaded if you install the app in a sub-folder, which was caused by
using the `mix` function without wrapping it with `url` function. Luckily, this is an easy fix applied in 
`resources/views/layouts/app.blade.php` layout file.

Below is the list of updated files, so make sure that you update them to the latest version.

```
 app/Http/Controllers/Web/Auth/SocialAuthController.php |  4 ++++
 app/Repositories/User/EloquentUser.php                 |  4 ++++
 config/app.php                                         |  2 +-
 resources/lang/de/app.php                              |  1 +
 resources/lang/en/app.php                              |  1 +
 resources/lang/sr/app.php                              |  1 +
 resources/views/layouts/app.blade.php                  |  6 +++---
 resources/views/user/partials/details.blade.php        |  2 +-
 resources/views/user/partials/row.blade.php            | 18 ++++++++++++------
 resources/views/user/view.blade.php                    |  6 +++---
 10 files changed, 31 insertions(+), 14 deletions(-)
```

<a name="upgrade-3.0.0"></a>
###To 3.0.0 from 2.2.0

This is the release which contains the complete rewrite of Vanguard frontend. The Bootstrap version is upgraded to 4.1 and 
the whole Vanguard frontend theme is updated to a different, more up-to-date, design.

Upgrading to this version is pretty hard and it means that you need to make sure that all your view files are up to 
date with new classes and staff. 

To start, it's recommended to make sure that your `composer.json` and `package.json` files are updated to the latest version so you can install
all the packages you need. Once you update them to the latest version, run `composer update` and `npm install` to install php and npm packages,
including Bootstrap 4.

Copy new `sass` folder to `resources/assets` folder, update `webpack.mix.js` file and run `npm run dev` to compile assets. Also make sure 
that all the assets in `public/assets` directory are updated to the latest version. If you haven't changed them much, then you can
just overwrite them all. However, if you have modified some of them, make sure that you update them manually.

Once you have updated all the assets, you should start updating your view files one by one. Starting from the `layout` files is recommended,
but you can do it however you decide.

The list of updated files is available below, so make sure that you check each one of them carefully, or you can check the patch file from
`documentation/Patches` directory to see how the files are updated.

```
 app/Http/Controllers/Api/Profile/AuthDetailsController.php                  |    39 +
 app/Http/Controllers/Web/Auth/PasswordController.php                        |     4 +-
 app/Http/Controllers/Web/Auth/SocialAuthController.php                      |    65 +-
 app/Http/Controllers/Web/DashboardController.php                            |     2 +-
 app/Http/Controllers/Web/InstallController.php                              |     4 +-
 app/Http/Requests/User/UpdateProfileLoginDetailsRequest.php                 |     3 -
 app/Presenters/UserPresenter.php                                            |     6 +-
 app/Repositories/User/EloquentUser.php                                      |     5 +-
 app/Services/Auth/Social/ManagesSocialAvatarSize.php                        |    32 +
 app/Services/Auth/Social/SocialManager.php                                  |     4 +-
 app/User.php                                                                |     2 +-
 composer.lock                                                               |   393 ++--
 config/app.php                                                              |     2 +-
 package-lock.json                                                           | 14043 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 package.json                                                                |     4 +-
 public/assets/css/app.css                                                   |  1160 +---------
 public/assets/css/bootstrap-datetimepicker.min.css                          |     5 -
 public/assets/css/bootstrap-social.css                                      |   101 -
 public/assets/css/bootstrap.min.css                                         |     5 -
 public/assets/css/font-awesome.min.css                                      |     4 -
 public/assets/css/fontawesome-all.min.css                                   |     5 +
 public/assets/css/install.css                                               |     4 +-
 public/assets/css/metisMenu.css                                             |    99 -
 public/assets/css/sweetalert.css                                            |   932 --------
 public/assets/css/vendor.css                                                |    10 +
 public/assets/fonts/FontAwesome.otf                                         |   Bin 93888 -> 0 bytes
 public/assets/fonts/fontawesome-webfont.eot                                 |   Bin 60767 -> 0 bytes
 public/assets/fonts/fontawesome-webfont.svg                                 |   565 -----
 public/assets/fonts/fontawesome-webfont.ttf                                 |   Bin 122092 -> 0 bytes
 public/assets/fonts/fontawesome-webfont.woff                                |   Bin 71508 -> 0 bytes
 public/assets/fonts/fontawesome-webfont.woff2                               |   Bin 56780 -> 0 bytes
 public/assets/fonts/glyphicons-halflings-regular.eot                        |   Bin 20127 -> 0 bytes
 public/assets/fonts/glyphicons-halflings-regular.svg                        |   288 ---
 public/assets/fonts/glyphicons-halflings-regular.ttf                        |   Bin 45404 -> 0 bytes
 public/assets/fonts/glyphicons-halflings-regular.woff                       |   Bin 23424 -> 0 bytes
 public/assets/fonts/glyphicons-halflings-regular.woff2                      |   Bin 18028 -> 0 bytes
 public/assets/js/as/app.js                                                  |    22 +-
 public/assets/js/as/btn.js                                                  |     4 +-
 public/assets/js/as/dashboard-admin.js                                      |    54 +-
 public/assets/js/as/dashboard-default.js                                    |    56 +-
 public/assets/js/as/login.js                                                |     2 +-
 public/assets/js/as/profile.js                                              |    11 +-
 public/assets/js/bootstrap-datetimepicker.min.js                            |     9 -
 public/assets/js/bootstrap.min.js                                           |    12 +-
 public/assets/js/bootstrap.min.js.map                                       |     1 +
 public/assets/js/chart.min.js                                               |     9 +-
 public/assets/js/delete.handler.js                                          |     8 +-
 public/assets/js/jquery-2.1.4.min.js                                        |     4 -
 public/assets/js/jquery-3.3.1.min.js                                        |     2 +
 public/assets/js/metisMenu.min.js                                           |    10 -
 public/assets/js/popper.min.js                                              |     5 +
 public/assets/js/sweetalert.min.js                                          |     2 +-
 public/assets/js/vendor.js                                                  |    11 +
 public/assets/plugins/bootstrap-datepicker/bootstrap-datepicker.min.css     |     9 +
 public/assets/plugins/bootstrap-datepicker/bootstrap-datepicker.min.css.map |     1 +
 public/assets/plugins/bootstrap-datepicker/bootstrap-datepicker.min.js      |     9 +
 public/assets/plugins/bootstrap-switch/bootstrap-switch.css                 |   195 --
 public/assets/plugins/bootstrap-switch/bootstrap-switch.min.js              |    22 -
 public/assets/webfonts/fa-brands-400.eot                                    |   Bin 0 -> 111620 bytes
 public/assets/webfonts/fa-brands-400.svg                                    |  1104 +++++++++
 public/assets/webfonts/fa-brands-400.ttf                                    |   Bin 0 -> 111384 bytes
 public/assets/webfonts/fa-brands-400.woff                                   |   Bin 0 -> 71560 bytes
 public/assets/webfonts/fa-brands-400.woff2                                  |   Bin 0 -> 61336 bytes
 public/assets/webfonts/fa-regular-400.eot                                   |   Bin 0 -> 31272 bytes
 public/assets/webfonts/fa-regular-400.svg                                   |   372 +++
 public/assets/webfonts/fa-regular-400.ttf                                   |   Bin 0 -> 31044 bytes
 public/assets/webfonts/fa-regular-400.woff                                  |   Bin 0 -> 14724 bytes
 public/assets/webfonts/fa-regular-400.woff2                                 |   Bin 0 -> 12188 bytes
 public/assets/webfonts/fa-solid-900.eot                                     |   Bin 0 -> 133140 bytes
 public/assets/webfonts/fa-solid-900.svg                                     |  1896 ++++++++++++++++
 public/assets/webfonts/fa-solid-900.ttf                                     |   Bin 0 -> 132920 bytes
 public/assets/webfonts/fa-solid-900.woff                                    |   Bin 0 -> 63836 bytes
 public/assets/webfonts/fa-solid-900.woff2                                   |   Bin 0 -> 50372 bytes
 public/mix-manifest.json                                                    |     5 +
 resources/assets/sass/_variables.scss                                       |    63 +-
 resources/assets/sass/app.scss                                              |    47 +-
 resources/assets/sass/components/avatar.scss                                |    16 +
 resources/assets/sass/components/button.scss                                |    78 +
 resources/assets/sass/components/card.scss                                  |    12 +
 resources/assets/sass/components/datepicker.scss                            |   160 ++
 resources/assets/sass/components/general.scss                               |    13 +
 resources/assets/sass/components/input.scss                                 |     8 +
 resources/assets/sass/components/list-group.scss                            |    17 +
 resources/assets/sass/components/nav-tabs.scss                              |    13 +
 resources/assets/sass/components/navbar.scss                                |    50 +
 resources/assets/sass/components/sidebar.scss                               |   122 +
 resources/assets/sass/components/sweet-alert.scss                           |     3 +
 resources/assets/sass/components/switch.scss                                |   158 ++
 resources/assets/sass/components/table.scss                                 |     8 +
 resources/assets/sass/components/util.scss                                  |    40 +
 resources/lang/de/app.php                                                   |    63 +-
 resources/lang/en/app.php                                                   |    58 +-
 resources/lang/sr/app.php                                                   |    64 +-
 resources/views/activity/index.blade.php                                    |   170 +-
 resources/views/auth/login.blade.php                                        |   103 +-
 resources/views/auth/password/remind.blade.php                              |    52 +-
 resources/views/auth/password/reset.blade.php                               |    82 +-
 resources/views/auth/register.blade.php                                     |   110 +-
 resources/views/auth/social/buttons.blade.php                               |    28 +-
 resources/views/auth/social/twitter-email.blade.php                         |    34 -
 resources/views/auth/token.blade.php                                        |    49 +-
 resources/views/dashboard/admin.blade.php                                   |   168 +-
 resources/views/dashboard/default.blade.php                                 |   106 +-
 resources/views/errors/403.blade.php                                        |    49 +-
 resources/views/errors/404.blade.php                                        |    63 +-
 resources/views/errors/500.blade.php                                        |    49 +-
 resources/views/errors/503.blade.php                                        |    44 +-
 resources/views/install/complete.blade.php                                  |     2 +-
 resources/views/install/database.blade.php                                  |     2 +-
 resources/views/install/error.blade.php                                     |     2 +-
 resources/views/install/permissions.blade.php                               |    12 +-
 resources/views/install/requirements.blade.php                              |     8 +-
 resources/views/install/start.blade.php                                     |     2 +-
 resources/views/layouts/app.blade.php                                       |    89 +-
 resources/views/layouts/auth.blade.php                                      |    24 +-
 resources/views/layouts/errors.blade.php                                    |    35 +
 resources/views/layouts/install.blade.php                                   |    37 +-
 resources/views/partials/messages.blade.php                                 |     4 +-
 resources/views/partials/navbar.blade.php                                   |    79 +
 resources/views/partials/sidebar.blade.php                                  |   167 +-
 resources/views/permission/add-edit.blade.php                               |    46 +-
 resources/views/permission/index.blade.php                                  |   159 +-
 resources/views/role/add-edit.blade.php                                     |    56 +-
 resources/views/role/index.blade.php                                        |   129 +-
 resources/views/settings/auth.blade.php                                     |    64 +-
 resources/views/settings/general.blade.php                                  |    41 +-
 resources/views/settings/notifications.blade.php                            |    78 +-
 resources/views/settings/partials/auth.blade.php                            |    70 +-
 resources/views/settings/partials/recaptcha.blade.php                       |    16 +-
 resources/views/settings/partials/registration.blade.php                    |    78 +-
 resources/views/settings/partials/throttling.blade.php                      |    45 +-
 resources/views/settings/partials/two-factor.blade.php                      |    15 +-
 resources/views/user/add.blade.php                                          |    71 +-
 resources/views/user/edit.blade.php                                         |   153 +-
 resources/views/user/list.blade.php                                         |   170 +-
 resources/views/user/partials/auth.blade.php                                |    57 +-
 resources/views/user/partials/avatar.blade.php                              |    69 +-
 resources/views/user/partials/details.blade.php                             |   118 +-
 resources/views/user/partials/row.blade.php                                 |    59 +
 resources/views/user/partials/two-factor.blade.php                          |    58 +-
 resources/views/user/profile.blade.php                                      |   143 +-
 resources/views/user/sessions.blade.php                                     |   123 +-
 resources/views/user/view.blade.php                                         |   172 +-
 resources/views/vendor/jsvalidation/bootstrap.php                           |    20 +-
 routes/api.php                                                              |     1 +
 storage/settings.json                                                       |     2 +-
 tests/Feature/Http/Controllers/Api/Auth/SocialLoginControllerTest.php       |     2 +
 tests/Feature/Http/Controllers/Api/Profile/AuthDetailsControllerTest.php    |    88 +
 tests/Feature/Http/Controllers/Api/Profile/TwoFactorControllerTest.php      |    28 +-
 tests/Feature/Http/Controllers/Api/Users/TwoFactorControllerTest.php        |    32 +-
 tests/Feature/Http/Controllers/Web/ActivityControllerTest.php               |     1 -
 tests/Feature/Http/Controllers/Web/Auth/AuthControllerTest.php              |     2 +-
 tests/Feature/Http/Controllers/Web/Auth/SocialAuthControllerTest.php        |    26 +-
 tests/Feature/Http/Controllers/Web/ProfileControllerTest.php                |    22 +-
 tests/Feature/Http/Controllers/Web/SettingsControllerTest.php               |     2 +-
 tests/Feature/Http/Controllers/Web/UsersControllerTest.php                  |    40 +-
 tests/Feature/Repositories/User/EloquentUserTest.php                        |    61 +-
 tests/unit/Presenters/UserPresenterTest.php                                 |     6 +-
 webpack.mix.js                                                              |    26 +-
 159 files changed, 20812 insertions(+), 5721 deletions(-)
```

<a name="upgrade-2.2.0"></a>
###To 2.2.0 from 2.1.1

In this release Laravel is upgraded to version 5.6. The only significant change here is that some packages 
(like `proengsoft/laravel-jsvalidation`, `tymon/jwt-auth` etc.) needs to be updated to latest version. 

The recommended way to upgrade your application is to make sure that your composer.json file matches the composer.json 
file from this release. Once you update your composer.json file, just run `composer update` to install those packages,
and then you can proceed and add missing files (there are few new configuration files added in Laravel 5.6) and 
update modified files that are listed below:

```
  _ide_helper.php                                              | 22037 +++---
  app/Http/Controllers/Api/Auth/AuthController.php             |     2 +-
  app/Http/Controllers/Api/StatsController.php                 |     4 +-
  app/Http/Controllers/Web/Auth/AuthController.php             |    42 +-
  app/Http/Controllers/Web/DashboardController.php             |     4 +-
  app/Http/Kernel.php                                          |     1 +
  app/Http/Middleware/TrustProxies.php                         |     8 +-
  app/Http/Requests/Auth/LoginRequest.php                      |    40 +
  app/Repositories/User/EloquentUser.php                       |     1 +
  app/Services/Auth/TwoFactor/Authy.php                        |     8 +-
  app/Services/Auth/TwoFactor/Contracts/Provider.php           |     3 +-
  app/User.php                                                 |     2 -
  composer.json                                                |    28 +-
  composer.lock                                                |  1133 +++----
  config/app.php                                               |    17 +-
  config/broadcasting.php                                      |     3 +
  config/filesystems.php                                       |     9 +-
  config/hashing.php                                           |    20 +
  config/logging.php                                           |    70 +
  config/queue.php                                             |     1 +
  config/services.php                                          |     3 +
  database/migrations/2015_10_10_170827_create_users_table.php |     2 +
  package.json                                                 |     7 +-
  public/.htaccess                                             |     2 +-
  resources/assets/js/app.js                                   |     2 +-
  resources/assets/js/bootstrap.js                             |     7 +-
  resources/assets/js/components/Example.vue                   |    12 +-
  storage/settings.json                                        |     2 +-
  tests/Feature/Http/Controllers/Api/StatsControllerTest.php   |    20 +-
  tests/Feature/Repositories/User/EloquentUserTest.php         |    60 +-
  tests/TestCase.php                                           |     2 +
  30 files changed, 13872 insertions(+), 9680 deletions(-)
```


<a name="upgrade-2.1.1"></a>
###To 2.1.1 from 2.1.0

This is mostly a bug-fix release with few new features added. To upgrade to this release I would recommend you to go through the list of 
modified files available below and to update file to the latest version. You don't have to update files from `/tests` and `/database/factories` folders since 
those files are related to application testing and won't affect the way how application works.

Here is the list of modified files:
```
 app/Http/Controllers/Web/DashboardController.php                      |   2 +-
 app/Http/Controllers/Web/InstallController.php                        |   6 +-
 app/Http/Requests/User/CreateUserRequest.php                          |   4 +-
 app/Http/Requests/User/UpdateDetailsRequest.php                       |   2 +-
 app/Http/Requests/User/UpdateProfileDetailsRequest.php                |   2 +-
 app/Http/Requests/User/UpdateUserRequest.php                          |   4 +-
 app/Listeners/Users/InvalidateSessionsAndTokens.php                   |  39 ++++++++++
 app/Presenters/UserPresenter.php                                      |   2 +-
 app/Providers/AppServiceProvider.php                                  |   1 +
 app/Providers/EventServiceProvider.php                                |   5 ++
 app/Repositories/Session/DbSession.php                                |  43 ++++++++++-
 app/Repositories/Session/SessionRepository.php                        |   7 ++
 app/Repositories/User/EloquentUser.php                                |  42 ++++------
 app/Repositories/User/UserRepository.php                              |   3 +-
 app/Transformers/SessionTransformer.php                               |  11 +--
 composer.json                                                         |   2 +-
 composer.lock                                                         | 511 +++++++++++++++
 config/app.php                                                        |  16 +++-
 database/factories/ActivityFactory.php                                |  15 ++++
 database/factories/CountryFactory.php                                 |  15 ++++
 database/factories/ModelFactory.php                                   |  98 ------------------------
 database/factories/PermissionFactory.php                              |  12 +++
 database/factories/RoleFactory.php                                    |  12 +++
 database/factories/TokenFactory.php                                   |  15 ++++
 database/factories/UserFactory.php                                    |  23 ++++++
 database/migrations/2015_10_10_170827_create_users_table.php          |   2 +-
 extra/auth.php                                                        |   6 +-
 package.json                                                          |  25 +++---
 resources/assets/js/app.js                                            |  22 ++++++
 resources/assets/js/bootstrap.js                                      |  53 +++++++++++++
 resources/assets/js/components/Example.vue                            |  23 ++++++
 resources/assets/sass/_variables.scss                                 |  38 +++++++++
 resources/assets/sass/app.scss                                        |   8 +-
 resources/lang/de/app.php                                             |  29 +++----
 resources/lang/en/app.php                                             |  25 +++---
 resources/lang/sr/app.php                                             |  25 +++---
 resources/views/activity/index.blade.php                              |   2 +-
 resources/views/errors/token-mismatch.blade.php                       |  43 -----------
 resources/views/user/list.blade.php                                   |   2 +-
 resources/views/user/sessions.blade.php                               |  18 +++--
 resources/views/user/view.blade.php                                   |   2 +-
 storage/settings.json                                                 |   2 +-
 tests/Feature/Http/Controllers/Api/Profile/SessionsControllerTest.php |   5 +-
 tests/Feature/Http/Controllers/Api/SessionsControllerTest.php         |   3 +-
 tests/Feature/Http/Controllers/Api/Users/SessionsControllerTest.php   |   9 ++-
 tests/Feature/Http/Controllers/Web/ActivityControllerTest.php         |   2 +-
 tests/Feature/Http/Controllers/Web/ProfileControllerTest.php          |  13 +++-
 tests/Feature/Http/Controllers/Web/UsersControllerTest.php            |  77 ++++++++++++++++---
 tests/Feature/Repositories/Session/DbSessionTest.php                  |  40 ++++++++--
 tests/Feature/Repositories/User/EloquentUserTest.php                  |  24 +++---
 50 files changed, 877 insertions(+), 513 deletions(-)

```


<a name="upgrade-2.1.0"></a>
###To 2.1.0 from 2.0.2

In this release Laravel is upgraded to version 5.5. The only significant change here is that some packages 
(like `proengsoft/laravel-jsvalidation`) needs to be updated to latest version. 

The recommended way to upgrade your application is to make sure that your composer.json file matches the composer.json 
file from this release. Once you update your composer.json file, just run `composer update` to install those packages,
and then you can proceed and update/overwrite modified files that are listed below (tests are excluded):

```
app/Exceptions/Handler.php                                     |   57 +----
 app/Http/Controllers/Web/Auth/AuthController.php               |    7 +-
 app/Http/Kernel.php                                            |    3 +
 app/Http/Middleware/TrimStrings.php                            |   18 ++
 app/Http/Middleware/TrustProxies.php                           |   29 +++
 app/Http/Middleware/UseApiGuard.php                            |    1 +
 app/Http/Requests/User/UpdateLoginDetailsRequest.php           |    4 +-
 artisan                                                        |    4 +-
 bootstrap/autoload.php                                         |   34 ---
 composer.json                                                  |   59 +++--
 composer.lock                                                  | 1440 +++---
 config/app.php                                                 |    2 +-
 config/broadcasting.php                                        |    7 +-
 config/cache.php                                               |   21 +-
 config/compile.php                                             |   35 ---
 config/database.php                                            |   33 +--
 config/filesystems.php                                         |    7 +
 config/mail.php                                                |   18 +-
 config/queue.php                                               |   29 +--
 config/services.php                                            |    4 -
 config/session.php                                             |   49 +++-
 config/settings.php                                            |   26 +-
 config/view.php                                                |    2 +-
 phpspec.yml                                                    |    5 -
 phpunit.xml                                                    |    2 +-
 public/.htaccess                                               |   11 +-
 public/index.php                                               |    4 +-
 public/vendor/jsvalidation/js/jsvalidation.js                  | 1681 +++---
 public/vendor/jsvalidation/js/jsvalidation.js.map              |    2 +-
 public/vendor/jsvalidation/js/jsvalidation.min.js              |    4 +-
 resources/views/activity/index.blade.php                       |    3 +-
 resources/views/user/view.blade.php                            |    2 +-
 resources/views/vendor/jsvalidation/bootstrap.php              |    7 +-
 webpack.mix.js                                                 |    2 +-
```

Since Laravel version is also upgraded, I would recommend you to go through Laravel's official 
[upgrade guide](https://laravel.com/docs/5.5/upgrade#upgrade-5.5.0) to make sure that your custom code is also
up to date. 

<a name="upgrade-2.0.2"></a>
###To 2.0.2 from 2.0.1

This is bug-fix release mainly to fix few glitches related to API authentication for unconfirmed 
and banned users, and other minor issues.

The list of updated files is displayed below:

```
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


<a name="upgrade-2.0.1"></a>
###To 2.0.1 from 2.0.0

This is bug-fix release which addresses few small bugs related mainly to the installation of version 2.0.0.

The following files are changed, so make sure that you update them if you want to install Vanguard via installer again:

```
 app/Http/Controllers/Web/InstallController.php | 1 +
 config/app.php                                 | 2 +-
 database/seeds/UserSeeder.php                  | 4 +---
 phpunit.xml                                    | 1 +
 resources/views/layouts/install.blade.php      | 6 +++---
 5 files changed, 7 insertions(+), 7 deletions(-)
```

If you have installed version 2.0.0 already, but you haven't executed the `php artisan jwt:secret` command since it
was not documented as a part of 2.0.0 update guide (I added it now btw, but it was not there originally), make sure that
you run the command now so it can generate random 32 characters long secret key used for signing JWT tokens for Vanguard
JSON API. Btw, in version 2.0.1 this command **will be automatically executed during the installation process**, so you don't
have to worry about it. 

<a name="upgrade-2.0.0"></a>
###To 2.0.0 from 1.3.3

Version 2 of Vanguard comes with a lot of changes mainly related to addition of JSON API that you can use to authenticate
your users from any application and manage your users through Vanguard. A lot of files are changed, so 
you will have to go through each one and make sure that it looks like it does in latest version, however 
here is the list of some main changes to make things a bit easier:

* Update `composer.json` file and run `composer update` command (or just overwrite composer.json, composer.lock files and vendor folder)
with the latest version.

* Run `php artisan migrate` command to create new database table for storing api token identifiers.

* Run `php artisan jwt:secret` command to generate new 32 characters long secret key used for signing JWT tokens (required only for JSON API)

* "Social Networks" section is completely removed from user's profile page as well as from edit user page. So, to 
remove it from your system, remove the `UserSocialNetworks` model from your `app` directory as well as `user_social_networks`
database table. Also, make sure that you update your view files and remove Social Network section from them as well. 

* There are now two different folders inside `app/Http/Controllers` folder: `Api` and `Web`. The `Api` folder is completely new 
so you can just copy it there from latest version. Your "old" controllers should be moved to `Web` folder and namespace for
each controller should be updated accordingly.

* `routes/api.php` file contains new routes related to the API, so make sure that you update that file too.

* Update `app/Providers/RouteServiceProvider` to support api route mapping.

* Added new `app/Transformers` folder which contains API transformers for all application entities

* Added new `app/Services/Auth/Api` folder which contains files related to API authentication.

* Added new `public/flags` directory which contains all flag images for countries that are available inside the system.

* Added new `UseApiGuard` middleware which is now added to `api` middleware group inside `app/Http/Kernel.php` file.

* Added new `expose_api` configuration parameter to `config/auth.php` file to enable/disable the API.

Here is the list of all modified and added files for this update:

```
 app/Country.php                                                                          |     2 +*
 app/Events/User/Registered.php                                                           |     2 +-
 app/Exceptions/Handler.php                                                               |    15 +-
 app/Http/Controllers/Api/ActivityController.php                                          |    39 +
 app/Http/Controllers/Api/ApiController.php                                               |   208 ++
 app/Http/Controllers/Api/Auth/AuthController.php                                         |    59 +
 app/Http/Controllers/Api/Auth/Password/RemindController.php                              |    41 +
 app/Http/Controllers/Api/Auth/Password/ResetController.php                               |    58 +
 app/Http/Controllers/Api/Auth/RegistrationController.php                                 |    87 +
 app/Http/Controllers/Api/Auth/SocialLoginController.php                                  |    64 +
 app/Http/Controllers/Api/Authorization/PermissionsController.php                         |    97 +
 app/Http/Controllers/Api/Authorization/RolePermissionsController.php                     |    65 +
 app/Http/Controllers/Api/Authorization/RolesController.php                               |   107 +
 app/Http/Controllers/Api/CountriesController.php                                         |    36 +
 app/Http/Controllers/Api/Profile/AvatarController.php                                    |    92 +
 app/Http/Controllers/Api/Profile/DetailsController.php                                   |    61 +
 app/Http/Controllers/Api/Profile/SessionsController.php                                  |    35 +
 app/Http/Controllers/Api/Profile/TwoFactorController.php                                 |    72 +
 app/Http/Controllers/Api/SessionsController.php                                          |    54 +
 app/Http/Controllers/Api/SettingsController.php                                          |    26 +
 app/Http/Controllers/Api/StatsController.php                                             |    92 +
 app/Http/Controllers/Api/Users/ActivityController.php                                    |    49 +
 app/Http/Controllers/Api/Users/AvatarController.php                                      |   106 +
 app/Http/Controllers/Api/Users/SessionsController.php                                    |    36 +
 app/Http/Controllers/Api/Users/TwoFactorController.php                                   |    72 +
 app/Http/Controllers/Api/Users/UsersController.php                                       |   141 ++
 app/Http/Controllers/{ => Web}/ActivityController.php                                    |     4 +-
 app/Http/Controllers/{ => Web}/Auth/AuthController.php                                   |    39 +-
 app/Http/Controllers/{ => Web}/Auth/PasswordController.php                               |     2 +-
 app/Http/Controllers/{ => Web}/Auth/SocialAuthController.php                             |    75 +-
 app/Http/Controllers/{ => Web}/DashboardController.php                                   |     7 +-
 app/Http/Controllers/{ => Web}/InstallController.php                                     |     3 +-
 app/Http/Controllers/{ => Web}/PermissionsController.php                                 |     3 +-
 app/Http/Controllers/{ => Web}/ProfileController.php                                     |    50 +-
 app/Http/Controllers/{ => Web}/RolesController.php                                       |     7 +-
 app/Http/Controllers/{ => Web}/SettingsController.php                                    |     7 +-
 app/Http/Controllers/{ => Web}/UsersController.php                                       |    61 +-
 app/Http/Kernel.php                                                                      |     1 +
 app/Http/Middleware/Authenticate.php                                                     |     2 +-
 app/Http/Middleware/CheckPermissions.php                                                 |     4 +-
 app/Http/Middleware/DatabaseSession.php                                                  |     2 +-
 app/Http/Middleware/UseApiGuard.php                                                      |    40 +
 app/Http/Requests/Activity/GetActivitiesRequest.php                                      |    28 +
 app/Http/Requests/Auth/Social/ApiAuthenticateRequest.php                                 |    25 +
 app/Http/Requests/BinaryFileUploadRequest.php                                            |    77 +
 app/Http/Requests/Permission/RemovePermissionRequest.php                                 |    23 +
 app/Http/Requests/Role/RemoveRoleRequest.php                                             |    23 +
 app/Http/Requests/Role/UpdateRolePermissionsRequest.php                                  |    32 +
 app/Http/Requests/User/CreateUserRequest.php                                             |    10 +-
 app/Http/Requests/User/UpdateDetailsRequest.php                                          |     2 +-
 app/Http/Requests/User/UpdateUserRequest.php                                             |    31 +
 app/Http/Requests/User/UploadAvatarRawRequest.php                                        |    22 +
 app/Http/Requests/User/UploadAvatarRequest.php                                           |    21 -
 app/Listeners/Registration/SendConfirmationEmail.php                                     |    42 +
 app/Listeners/{UserWasRegisteredListener.php => Registration/SendSignUpNotification.php} |     8 +-
 app/Mailers/AbstractMailer.php                                                           |    39 -
 app/Mailers/UserMailer.php                                                               |    20 -
 app/Permission.php                                                                       |     4 +
 app/Providers/AuthServiceProvider.php                                                    |     9 +
 app/Providers/EventServiceProvider.php                                                   |     7 +-
 app/Providers/RouteServiceProvider.php                                                   |    29 +-
 app/Repositories/Country/CountryRepository.php                                           |     8 +-
 app/Repositories/Country/EloquentCountry.php                                             |     8 +
 app/Repositories/Permission/PermissionRepository.php                                     |     2 +-
 app/Repositories/Role/EloquentRole.php                                                   |     7 +-
 app/Repositories/Session/DbSession.php                                                   |    21 +-
 app/Repositories/Session/SessionRepository.php                                           |    12 +-
 app/Repositories/User/EloquentUser.php                                                   |    33 +-
 app/Repositories/User/UserRepository.php                                                 |    22 +-
 app/Services/Auth/Api/ExtendsJwtValidation.php                                           |    69 +
 app/Services/Auth/Api/JWT.php                                                            |     8 +
 app/Services/Auth/Api/JWTAuth.php                                                        |     8 +
 app/Services/Auth/Api/JWTServiceProvider.php                                             |    39 +
 app/Services/Auth/Api/Token.php                                                          |    12 +
 app/Services/Auth/Api/TokenFactory.php                                                   |    79 +
 app/Services/Auth/Social/SocialManager.php                                               |    85 +
 app/Services/Logging/UserActivity/Activity.php                                           |     2 +-
 app/Services/Logging/UserActivity/Logger.php                                             |    10 +-
 app/Services/Upload/UserAvatarManager.php                                                |    86 +-
 app/Support/Authorization/AuthorizationUserTrait.php                                     |    44 +-
 app/Support/DataArraySerializer.php                                                      |   100 +
 app/Support/Enum/UserStatus.php                                                          |     2 +-
 app/Transformers/ActivityTransformer.php                                                 |    36 +
 app/Transformers/CountryTransformer.php                                                  |    32 +
 app/Transformers/PermissionTransformer.php                                               |    22 +
 app/Transformers/RoleTransformer.php                                                     |    33 +
 app/Transformers/SessionTransformer.php                                                  |    27 +
 app/Transformers/UserTransformer.php                                                     |    51 +
 app/User.php                                                                             |    45 +-
 app/UserSocialNetworks.php                                                               |    29 -
 composer.json                                                                            |     5 +-
 composer.lock                                                                            |   909 ++++++--
 config/app.php                                                                           |     7 +-
 config/auth.php                                                                          |    24 +-
 config/jwt.php                                                                           |   262 +++
 database/factories/ModelFactory.php                                                      |    14 +
 database/migrations/2015_10_10_170827_create_users_table.php                             |     4 +-
 database/migrations/2015_10_10_170911_create_user_social_networks_table.php              |    36 -
 database/migrations/2015_12_30_171734_add_foreign_keys.php                               |    11 -
 database/migrations/2017_04_13_200254_create_api_tokens_table.php                        |    49 +
 database/seeds/CountriesSeeder.php                                                       |     6 +-
 public/.htaccess                                                                         |     4 +
 public/flags/AD.png                                                                      |   Bin 0 -> 1407 bytes
 public/flags/AE.png                                                                      |   Bin 0 -> 1010 bytes
 public/flags/AF.png                                                                      |   Bin 0 -> 1335 bytes
 public/flags/AG.png                                                                      |   Bin 0 -> 1928 bytes
 public/flags/AI.png                                                                      |   Bin 0 -> 1765 bytes
 public/flags/AL.png                                                                      |   Bin 0 -> 1458 bytes
 public/flags/AM.png                                                                      |   Bin 0 -> 1005 bytes
 public/flags/AN.png                                                                      |   Bin 0 -> 1384 bytes
 public/flags/AO.png                                                                      |   Bin 0 -> 1323 bytes
 public/flags/AQ.png                                                                      |   Bin 0 -> 1698 bytes
 public/flags/AR.png                                                                      |   Bin 0 -> 1199 bytes
 public/flags/AS.png                                                                      |   Bin 0 -> 1440 bytes
 public/flags/AT.png                                                                      |   Bin 0 -> 1016 bytes
 public/flags/AU.png                                                                      |   Bin 0 -> 1963 bytes
 public/flags/AW.png                                                                      |   Bin 0 -> 1336 bytes
 public/flags/AZ.png                                                                      |   Bin 0 -> 1312 bytes
 public/flags/BA.png                                                                      |   Bin 0 -> 1803 bytes
 public/flags/BB.png                                                                      |   Bin 0 -> 1420 bytes
 public/flags/BD.png                                                                      |   Bin 0 -> 1489 bytes
 public/flags/BE.png                                                                      |   Bin 0 -> 968 bytes
 public/flags/BF.png                                                                      |   Bin 0 -> 1260 bytes
 public/flags/BG.png                                                                      |   Bin 0 -> 971 bytes
 public/flags/BH.png                                                                      |   Bin 0 -> 1136 bytes
 public/flags/BI.png                                                                      |   Bin 0 -> 2248 bytes
 public/flags/BJ.png                                                                      |   Bin 0 -> 1088 bytes
 public/flags/BM.png                                                                      |   Bin 0 -> 1666 bytes
 public/flags/BN.png                                                                      |   Bin 0 -> 1977 bytes
 public/flags/BO.png                                                                      |   Bin 0 -> 959 bytes
 public/flags/BR.png                                                                      |   Bin 0 -> 2101 bytes
 public/flags/BS.png                                                                      |   Bin 0 -> 1401 bytes
 public/flags/BT.png                                                                      |   Bin 0 -> 2042 bytes
 public/flags/BV.png                                                                      |   Bin 0 -> 1465 bytes
 public/flags/BW.png                                                                      |   Bin 0 -> 1024 bytes
 public/flags/BY.png                                                                      |   Bin 0 -> 1336 bytes
 public/flags/BZ.png                                                                      |   Bin 0 -> 2126 bytes
 public/flags/CA.png                                                                      |   Bin 0 -> 1332 bytes
 public/flags/CC.png                                                                      |   Bin 0 -> 1681 bytes
 public/flags/CD.png                                                                      |   Bin 0 -> 2266 bytes
 public/flags/CF.png                                                                      |   Bin 0 -> 1586 bytes
 public/flags/CG.png                                                                      |   Bin 0 -> 1376 bytes
 public/flags/CH.png                                                                      |   Bin 0 -> 1418 bytes
 public/flags/CI.png                                                                      |   Bin 0 -> 1018 bytes
 public/flags/CK.png                                                                      |   Bin 0 -> 1989 bytes
 public/flags/CL.png                                                                      |   Bin 0 -> 1287 bytes
 public/flags/CM.png                                                                      |   Bin 0 -> 1024 bytes
 public/flags/CN.png                                                                      |   Bin 0 -> 1286 bytes
 public/flags/CO.png                                                                      |   Bin 0 -> 957 bytes
 public/flags/CR.png                                                                      |   Bin 0 -> 962 bytes
 public/flags/CS.png                                                                      |   Bin 0 -> 973 bytes
 public/flags/CU.png                                                                      |   Bin 0 -> 1737 bytes
 public/flags/CV.png                                                                      |   Bin 0 -> 1484 bytes
 public/flags/CX.png                                                                      |   Bin 0 -> 1925 bytes
 public/flags/CY.png                                                                      |   Bin 0 -> 1420 bytes
 public/flags/CZ.png                                                                      |   Bin 0 -> 1477 bytes
 public/flags/DE.png                                                                      |   Bin 0 -> 950 bytes
 public/flags/DJ.png                                                                      |   Bin 0 -> 1493 bytes
 public/flags/DK.png                                                                      |   Bin 0 -> 994 bytes
 public/flags/DM.png                                                                      |   Bin 0 -> 1636 bytes
 public/flags/DO.png                                                                      |   Bin 0 -> 1289 bytes
 public/flags/DZ.png                                                                      |   Bin 0 -> 1535 bytes
 public/flags/EC.png                                                                      |   Bin 0 -> 1611 bytes
 public/flags/EE.png                                                                      |   Bin 0 -> 954 bytes
 public/flags/EG.png                                                                      |   Bin 0 -> 1100 bytes
 public/flags/EH.png                                                                      |   Bin 0 -> 1440 bytes
 public/flags/ER.png                                                                      |   Bin 0 -> 2030 bytes
 public/flags/ES.png                                                                      |   Bin 0 -> 1390 bytes
 public/flags/ET.png                                                                      |   Bin 0 -> 1614 bytes
 public/flags/FI.png                                                                      |   Bin 0 -> 1180 bytes
 public/flags/FJ.png                                                                      |   Bin 0 -> 1847 bytes
 public/flags/FK.png                                                                      |   Bin 0 -> 1891 bytes
 public/flags/FM.png                                                                      |   Bin 0 -> 1481 bytes
 public/flags/FO.png                                                                      |   Bin 0 -> 1314 bytes
 public/flags/FR.png                                                                      |   Bin 0 -> 958 bytes
 public/flags/GA.png                                                                      |   Bin 0 -> 959 bytes
 public/flags/GB.png                                                                      |   Bin 0 -> 2299 bytes
 public/flags/GD.png                                                                      |   Bin 0 -> 1918 bytes
 public/flags/GE.png                                                                      |   Bin 0 -> 1582 bytes
 public/flags/GF.png                                                                      |   Bin 0 -> 1437 bytes
 public/flags/GH.png                                                                      |   Bin 0 -> 1354 bytes
 public/flags/GI.png                                                                      |   Bin 0 -> 1605 bytes
 public/flags/GL.png                                                                      |   Bin 0 -> 1615 bytes
 public/flags/GM.png                                                                      |   Bin 0 -> 1080 bytes
 public/flags/GN.png                                                                      |   Bin 0 -> 1064 bytes
 public/flags/GP.png                                                                      |   Bin 0 -> 1952 bytes
 public/flags/GQ.png                                                                      |   Bin 0 -> 1574 bytes
 public/flags/GR.png                                                                      |   Bin 0 -> 1351 bytes
 public/flags/GS.png                                                                      |   Bin 0 -> 1911 bytes
 public/flags/GT.png                                                                      |   Bin 0 -> 1477 bytes
 public/flags/GU.png                                                                      |   Bin 0 -> 1432 bytes
 public/flags/GW.png                                                                      |   Bin 0 -> 1332 bytes
 public/flags/GY.png                                                                      |   Bin 0 -> 2156 bytes
 public/flags/HK.png                                                                      |   Bin 0 -> 1355 bytes
 public/flags/HM.png                                                                      |   Bin 0 -> 2031 bytes
 public/flags/HN.png                                                                      |   Bin 0 -> 1089 bytes
 public/flags/HR.png                                                                      |   Bin 0 -> 1622 bytes
 public/flags/HT.png                                                                      |   Bin 0 -> 1356 bytes
 public/flags/HU.png                                                                      |   Bin 0 -> 994 bytes
 public/flags/ID.png                                                                      |   Bin 0 -> 1021 bytes
 public/flags/IE.png                                                                      |   Bin 0 -> 958 bytes
 public/flags/IL.png                                                                      |   Bin 0 -> 1327 bytes
 public/flags/IN.png                                                                      |   Bin 0 -> 1159 bytes
 public/flags/IO.png                                                                      |   Bin 0 -> 2284 bytes
 public/flags/IQ.png                                                                      |   Bin 0 -> 1129 bytes
 public/flags/IR.png                                                                      |   Bin 0 -> 1100 bytes
 public/flags/IS.png                                                                      |   Bin 0 -> 1243 bytes
 public/flags/IT.png                                                                      |   Bin 0 -> 1057 bytes
 public/flags/JM.png                                                                      |   Bin 0 -> 1907 bytes
 public/flags/JO.png                                                                      |   Bin 0 -> 1571 bytes
 public/flags/JP.png                                                                      |   Bin 0 -> 1350 bytes
 public/flags/KE.png                                                                      |   Bin 0 -> 1552 bytes
 public/flags/KG.png                                                                      |   Bin 0 -> 1392 bytes
 public/flags/KH.png                                                                      |   Bin 0 -> 1490 bytes
 public/flags/KI.png                                                                      |   Bin 0 -> 1551 bytes
 public/flags/KM.png                                                                      |   Bin 0 -> 1810 bytes
 public/flags/KN.png                                                                      |   Bin 0 -> 1909 bytes
 public/flags/KP.png                                                                      |   Bin 0 -> 1377 bytes
 public/flags/KR.png                                                                      |   Bin 0 -> 1883 bytes
 public/flags/KW.png                                                                      |   Bin 0 -> 1291 bytes
 public/flags/KY.png                                                                      |   Bin 0 -> 1536 bytes
 public/flags/KZ.png                                                                      |   Bin 0 -> 1496 bytes
 public/flags/LA.png                                                                      |   Bin 0 -> 1278 bytes
 public/flags/LB.png                                                                      |   Bin 0 -> 1336 bytes
 public/flags/LC.png                                                                      |   Bin 0 -> 1437 bytes
 public/flags/LI.png                                                                      |   Bin 0 -> 1182 bytes
 public/flags/LK.png                                                                      |   Bin 0 -> 2037 bytes
 public/flags/LR.png                                                                      |   Bin 0 -> 1375 bytes
 public/flags/LS.png                                                                      |   Bin 0 -> 1190 bytes
 public/flags/LT.png                                                                      |   Bin 0 -> 959 bytes
 public/flags/LU.png                                                                      |   Bin 0 -> 959 bytes
 public/flags/LV.png                                                                      |   Bin 0 -> 1003 bytes
 public/flags/LY.png                                                                      |   Bin 0 -> 947 bytes
 public/flags/MA.png                                                                      |   Bin 0 -> 1454 bytes
 public/flags/MC.png                                                                      |   Bin 0 -> 981 bytes
 public/flags/MD.png                                                                      |   Bin 0 -> 1464 bytes
 public/flags/ME.png                                                                      |   Bin 0 -> 930 bytes
 public/flags/MG.png                                                                      |   Bin 0 -> 1077 bytes
 public/flags/MH.png                                                                      |   Bin 0 -> 1839 bytes
 public/flags/MK.png                                                                      |   Bin 0 -> 2468 bytes
 public/flags/ML.png                                                                      |   Bin 0 -> 1065 bytes
 public/flags/MM.png                                                                      |   Bin 0 -> 1345 bytes
 public/flags/MN.png                                                                      |   Bin 0 -> 1487 bytes
 public/flags/MO.png                                                                      |   Bin 0 -> 1548 bytes
 public/flags/MP.png                                                                      |   Bin 0 -> 1688 bytes
 public/flags/MQ.png                                                                      |   Bin 0 -> 2145 bytes
 public/flags/MR.png                                                                      |   Bin 0 -> 1565 bytes
 public/flags/MS.png                                                                      |   Bin 0 -> 1805 bytes
 public/flags/MT.png                                                                      |   Bin 0 -> 1171 bytes
 public/flags/MU.png                                                                      |   Bin 0 -> 1092 bytes
 public/flags/MV.png                                                                      |   Bin 0 -> 1444 bytes
 public/flags/MW.png                                                                      |   Bin 0 -> 1163 bytes
 public/flags/MX.png                                                                      |   Bin 0 -> 1326 bytes
 public/flags/MY.png                                                                      |   Bin 0 -> 1762 bytes
 public/flags/MZ.png                                                                      |   Bin 0 -> 1672 bytes
 public/flags/NA.png                                                                      |   Bin 0 -> 2162 bytes
 public/flags/NC.png                                                                      |   Bin 0 -> 1740 bytes
 public/flags/NE.png                                                                      |   Bin 0 -> 1082 bytes
 public/flags/NF.png                                                                      |   Bin 0 -> 1186 bytes
 public/flags/NG.png                                                                      |   Bin 0 -> 958 bytes
 public/flags/NI.png                                                                      |   Bin 0 -> 1086 bytes
 public/flags/NL.png                                                                      |   Bin 0 -> 974 bytes
 public/flags/NO.png                                                                      |   Bin 0 -> 1366 bytes
 public/flags/NP.png                                                                      |   Bin 0 -> 1810 bytes
 public/flags/NR.png                                                                      |   Bin 0 -> 1267 bytes
 public/flags/NU.png                                                                      |   Bin 0 -> 1700 bytes
 public/flags/NZ.png                                                                      |   Bin 0 -> 1731 bytes
 public/flags/OM.png                                                                      |   Bin 0 -> 1334 bytes
 public/flags/PA.png                                                                      |   Bin 0 -> 1343 bytes
 public/flags/PE.png                                                                      |   Bin 0 -> 1015 bytes
 public/flags/PF.png                                                                      |   Bin 0 -> 1258 bytes
 public/flags/PG.png                                                                      |   Bin 0 -> 1933 bytes
 public/flags/PH.png                                                                      |   Bin 0 -> 1704 bytes
 public/flags/PK.png                                                                      |   Bin 0 -> 1541 bytes
 public/flags/PL.png                                                                      |   Bin 0 -> 953 bytes
 public/flags/PM.png                                                                      |   Bin 0 -> 2605 bytes
 public/flags/PN.png                                                                      |   Bin 0 -> 2064 bytes
 public/flags/PR.png                                                                      |   Bin 0 -> 1507 bytes
 public/flags/PS.png                                                                      |   Bin 0 -> 1287 bytes
 public/flags/PT.png                                                                      |   Bin 0 -> 1597 bytes
 public/flags/PW.png                                                                      |   Bin 0 -> 1445 bytes
 public/flags/PY.png                                                                      |   Bin 0 -> 1145 bytes
 public/flags/QA.png                                                                      |   Bin 0 -> 1358 bytes
 public/flags/RE.png                                                                      |   Bin 0 -> 1775 bytes
 public/flags/RO.png                                                                      |   Bin 0 -> 958 bytes
 public/flags/RU.png                                                                      |   Bin 0 -> 982 bytes
 public/flags/RW.png                                                                      |   Bin 0 -> 1344 bytes
 public/flags/SA.png                                                                      |   Bin 0 -> 1686 bytes
 public/flags/SB.png                                                                      |   Bin 0 -> 1809 bytes
 public/flags/SC.png                                                                      |   Bin 0 -> 2034 bytes
 public/flags/SD.png                                                                      |   Bin 0 -> 1411 bytes
 public/flags/SE.png                                                                      |   Bin 0 -> 965 bytes
 public/flags/SG.png                                                                      |   Bin 0 -> 1415 bytes
 public/flags/SH.png                                                                      |   Bin 0 -> 1720 bytes
 public/flags/SI.png                                                                      |   Bin 0 -> 1297 bytes
 public/flags/SJ.png                                                                      |   Bin 0 -> 1310 bytes
 public/flags/SK.png                                                                      |   Bin 0 -> 1570 bytes
 public/flags/SL.png                                                                      |   Bin 0 -> 989 bytes
 public/flags/SM.png                                                                      |   Bin 0 -> 1514 bytes
 public/flags/SN.png                                                                      |   Bin 0 -> 1297 bytes
 public/flags/SO.png                                                                      |   Bin 0 -> 1278 bytes
 public/flags/SR.png                                                                      |   Bin 0 -> 1341 bytes
 public/flags/ST.png                                                                      |   Bin 0 -> 1562 bytes
 public/flags/SV.png                                                                      |   Bin 0 -> 1089 bytes
 public/flags/SY.png                                                                      |   Bin 0 -> 1077 bytes
 public/flags/SZ.png                                                                      |   Bin 0 -> 1814 bytes
 public/flags/TC.png                                                                      |   Bin 0 -> 1856 bytes
 public/flags/TD.png                                                                      |   Bin 0 -> 958 bytes
 public/flags/TF.png                                                                      |   Bin 0 -> 1631 bytes
 public/flags/TG.png                                                                      |   Bin 0 -> 1332 bytes
 public/flags/TH.png                                                                      |   Bin 0 -> 965 bytes
 public/flags/TJ.png                                                                      |   Bin 0 -> 1247 bytes
 public/flags/TK.png                                                                      |   Bin 0 -> 1707 bytes
 public/flags/TL.png                                                                      |   Bin 0 -> 1775 bytes
 public/flags/TM.png                                                                      |   Bin 0 -> 1647 bytes
 public/flags/TN.png                                                                      |   Bin 0 -> 1521 bytes
 public/flags/TO.png                                                                      |   Bin 0 -> 1181 bytes
 public/flags/TR.png                                                                      |   Bin 0 -> 1616 bytes
 public/flags/TT.png                                                                      |   Bin 0 -> 1893 bytes
 public/flags/TV.png                                                                      |   Bin 0 -> 1982 bytes
 public/flags/TW.png                                                                      |   Bin 0 -> 1322 bytes
 public/flags/TZ.png                                                                      |   Bin 0 -> 1721 bytes
 public/flags/UA.png                                                                      |   Bin 0 -> 953 bytes
 public/flags/UG.png                                                                      |   Bin 0 -> 1100 bytes
 public/flags/UM.png                                                                      |   Bin 0 -> 1670 bytes
 public/flags/US.png                                                                      |   Bin 0 -> 1718 bytes
 public/flags/UY.png                                                                      |   Bin 0 -> 1280 bytes
 public/flags/UZ.png                                                                      |   Bin 0 -> 1394 bytes
 public/flags/VA.png                                                                      |   Bin 0 -> 1412 bytes
 public/flags/VC.png                                                                      |   Bin 0 -> 1637 bytes
 public/flags/VE.png                                                                      |   Bin 0 -> 1224 bytes
 public/flags/VG.png                                                                      |   Bin 0 -> 1864 bytes
 public/flags/VI.png                                                                      |   Bin 0 -> 2001 bytes
 public/flags/VN.png                                                                      |   Bin 0 -> 1435 bytes
 public/flags/VU.png                                                                      |   Bin 0 -> 1786 bytes
 public/flags/WF.png                                                                      |   Bin 0 -> 1603 bytes
 public/flags/WS.png                                                                      |   Bin 0 -> 1290 bytes
 public/flags/YE.png                                                                      |   Bin 0 -> 987 bytes
 public/flags/YT.png                                                                      |   Bin 0 -> 1982 bytes
 public/flags/ZA.png                                                                      |   Bin 0 -> 1881 bytes
 public/flags/ZM.png                                                                      |   Bin 0 -> 1280 bytes
 public/flags/ZW.png                                                                      |   Bin 0 -> 1630 bytes
 resources/lang/de/app.php                                                                |     1 +
 resources/lang/en/app.php                                                                |     4 +-
 resources/lang/en/validation.php                                                         |     1 +
 resources/lang/sr/app.php                                                                |     1 +
 resources/views/auth/register.blade.php                                                  |     2 +-
 resources/views/partials/sidebar.blade.php                                               |     2 +-
 resources/views/user/edit.blade.php                                                      |    15 -
 resources/views/user/partials/details.blade.php                                          |     4 +-
 resources/views/user/partials/social-networks.blade.php                                  |    69 -
 resources/views/user/profile.blade.php                                                   |    15 -
 resources/views/user/view.blade.php                                                      |    47 -
 routes/api.php                                                                           |    72 +-
 routes/web.php                                                                           |    10 -
 storage/settings.json                                                                    |     2 +-
 tests/Feature/ApiTestCase.php                                                            |    76 +
 tests/Feature/FunctionalTestCase.php                                                     |    49 +-
 tests/Feature/Http/Controllers/Api/ActivityControllerTest.php                            |   118 +
 tests/Feature/Http/Controllers/Api/Auth/AuthControllerTest.php                           |    99 +
 tests/Feature/Http/Controllers/Api/Auth/Password/RemindControllerTest.php                |    57 +
 tests/Feature/Http/Controllers/Api/Auth/Password/ResetControllerTest.php                 |   106 +
 tests/Feature/Http/Controllers/Api/Auth/RegistrationControllerTest.php                   |   125 ++
 tests/Feature/Http/Controllers/Api/Auth/SocialLoginControllerTest.php                    |   181 ++
 tests/Feature/Http/Controllers/Api/Authorization/PermissionsControllerTest.php           |   190 ++
 tests/Feature/Http/Controllers/Api/Authorization/RolePermissionsControllerTest.php       |    90 +
 tests/Feature/Http/Controllers/Api/Authorization/RolesControllerTest.php                 |   203 ++
 tests/Feature/Http/Controllers/Api/CountriesControllerTest.php                           |    31 +
 tests/Feature/Http/Controllers/Api/Profile/AvatarControllerTest.php                      |   114 +
 tests/Feature/Http/Controllers/Api/Profile/DetailsControllerTest.php                     |   125 ++
 tests/Feature/Http/Controllers/Api/Profile/SessionsControllerTest.php                    |    69 +
 tests/Feature/Http/Controllers/Api/Profile/TwoFactorControllerTest.php                   |   108 +
 tests/Feature/Http/Controllers/Api/SessionsControllerTest.php                            |   113 +
 tests/Feature/Http/Controllers/Api/SettingsControllerTest.php                            |    37 +
 tests/Feature/Http/Controllers/Api/StatsControllerTest.php                               |   108 +
 tests/Feature/Http/Controllers/Api/Users/ActivityControllerTest.php                      |   109 +
 tests/Feature/Http/Controllers/Api/Users/AvatarControllerTest.php                        |   154 ++
 tests/Feature/Http/Controllers/Api/Users/SessionsControllerTest.php                      |    66 +
 tests/Feature/Http/Controllers/Api/Users/TwoFactorControllerTest.php                     |   125 ++
 tests/Feature/Http/Controllers/Api/Users/UsersControllerTest.php                         |   248 +++
 tests/Feature/Http/Controllers/{ => Web}/ActivityControllerTest.php                      |     2 +-
 tests/Feature/Http/Controllers/{ => Web}/Auth/AuthControllerTest.php                     |    13 +-
 tests/Feature/Http/Controllers/{ => Web}/Auth/PasswordControllerTest.php                 |     2 +-
 tests/Feature/Http/Controllers/{ => Web}/Auth/SocialAuthControllerTest.php               |     2 +-
 tests/Feature/Http/Controllers/{ => Web}/PermissionsControllerTest.php                   |     2 +-
 tests/Feature/Http/Controllers/{ => Web}/ProfileControllerTest.php                       |    22 +-
 tests/Feature/Http/Controllers/{ => Web}/RolesControllerTest.php                         |     2 +-
 tests/Feature/Http/Controllers/{ => Web}/SettingsControllerTest.php                      |     2 +-
 tests/Feature/Http/Controllers/{ => Web}/UsersControllerTest.php                         |    51 +-
 tests/Feature/Listeners/BaseListenerTestCase.php                                         |     6 +-
 tests/Feature/Listeners/UserEventsSubscriberTest.php                                     |    14 +-
 tests/Feature/Repositories/Session/DbSessionTest.php                                     |     9 +-
 tests/Feature/Repositories/User/EloquentUserTest.php                                     |    87 +-
 tests/Feature/Services/Auth/Api/TokenFactoryTest.php                                     |   101 +
 395 files changed, 13687 insertions(+), 6162 deletions(-)
```
 

<a name="upgrade-1.3.3"></a>
###To 1.3.3 from 1.3.2

Fix compatibility issues with `laravel-jsvalidation` package and Laravel Framework version `5.4.19+` and fix issue where country is set to null after user logs in.

First, you need to update `Vanguard\Repositories\User\EloquentUser::update` method to fix the country issue, and then you can proceed and update 
`composer.json` file to fix compatibility issues with `laravel-jsvalidtion` package. 
After updating composer.json file to the latest version, you can run `composer update` command to update your packages.

P.S.
This compatibility issue only exists for latest version of Laravel Framework (5.4.19 at the moment of typing).

<a name="upgrade-1.3.2"></a>
###To 1.3.2 from 1.3.1

In version 1.3.2 `zizaco/entrust` package has been removed, and Vanguard now has it's own, built in way, of handling the user permissions. 

The main change is that you will now have to use `$user->hasPermission('permission_name')` instead of `$user->can('permission_name')`, and the reason is to support Laravel's native authorization system that uses `can` method.

Another thing that you will have to do is to remove "role_user" database table (after you execute the SQL code below), since it is not being after `entrust` package is removed, and to create new `role_id` field in `users` database table which should be `int(10) unsigned NOT NULL`. From now on this field will hold the user's role.
Now, since you probably already have users in your system, here is the sql code that you can execute to create this new field in `users` table and to update it's value to current user's role:

```mysql
ALTER TABLE users ADD `role_id` int(10) unsigned NOT NULL;

UPDATE `users`
INNER JOIN `role_user` ON `users`.`id` = `role_user`.`user_id` 
SET `users`.`role_id` = `role_user`.`role_id`;

ALTER TABLE `users` ADD CONSTRAINT users_role_id_foreign FOREIGN KEY(`role_id`) REFERENCES roles(id);
```

After you perform the above actions, next thing to do is to check the modified files and update your files to match the files from version 1.3.2:

```
 app/Http/Controllers/Auth/AuthController.php                                |   7 ++--
 app/Http/Controllers/Auth/SocialAuthController.php                          |  12 +++---
 app/Http/Controllers/ProfileController.php                                  |   8 ++--
 app/Http/Controllers/UsersController.php                                    |  16 ++++----
 app/Http/Kernel.php                                                         |   6 +--
 app/Http/Middleware/CheckPermissions.php                                    |  41 -------------------
 app/Http/Middleware/CheckRole.php                                           |  36 -----------------
 app/Listeners/UserWasRegisteredListener.php                                 |   2 +-
 app/Permission.php                                                          |   8 ++--
 app/Presenters/UserPresenter.php                                            |   4 +-
 app/Providers/AuthServiceProvider.php                                       |  16 +-------
 app/Repositories/Role/EloquentRole.php                                      |  12 ++++--
 app/Repositories/Role/RoleRepository.php                                    |   2 +-
 app/Repositories/User/EloquentUser.php                                      |   7 +++-
 app/Role.php                                                                |  20 +++++++---
 app/Support/Authorization/AuthorizationRoleTrait.php                        | 153 ++++++++++++++++++++++++++++++++++++++++-------------------------------
 app/Support/Authorization/AuthorizationUserTrait.php                        |  65 +++++++++++-------------------
 app/Support/Authorization/CacheFlusherTrait.php                             |  35 +++++++++++++++++
 app/User.php                                                                |   2 +-
 composer.lock                                                               | 251 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++-----------------------------------------------------------
 config/app.php                                                              |   2 +
 config/entrust.php                                                          |  92 +++++++++++++++++++++++++++++++++++++++++++
 database/factories/ModelFactory.php                                         |   5 ---
 database/migrations/2015_08_25_172600_create_settings_table.php             |  61 ++++++++++++++--------------
 database/migrations/2015_09_19_191655_setup_countries_table.php             |  79 +++++++++++++++++++------------------
 database/migrations/2015_10_10_170827_create_users_table.php                |   4 +-
 database/migrations/2015_10_10_170911_create_user_social_networks_table.php |   2 +-
 database/migrations/2015_10_10_171049_create_social_login_table.php         |   2 +-
 database/migrations/2015_10_10_171734_add_foreign_keys.php                  |  56 ++++++++++++++++++++++++++
 database/migrations/2015_12_19_191656_charify_countries_table.php           |  42 ++++++++++++++++++++
 database/migrations/2015_12_24_080704_entrust_setup_tables.php              |  73 ++++++++++++++++++++++++++++++++++
 database/migrations/2015_12_24_080704_setup_authorization_tables.php        |  59 ----------------------------
 database/migrations/2015_12_29_224252_create_user_activity_table.php        |   4 +-
 database/migrations/2015_12_30_171734_add_foreign_keys.php                  |  61 ----------------------------
 database/seeds/UserSeeder.php                                               |   6 +--
 resources/views/user/partials/details.blade.php                             |   2 +-
 tests/Feature/FunctionalTestCase.php                                        |   4 +-
 tests/Feature/Http/Controllers/Auth/AuthControllerTest.php                  |  22 ++++-------
 tests/Feature/Http/Controllers/PermissionsControllerTest.php                |  12 +++---
 tests/Feature/Http/Controllers/ProfileControllerTest.php                    |   8 ++--
 tests/Feature/Http/Controllers/RolesControllerTest.php                      |  20 ++++------
 tests/Feature/Http/Controllers/UsersControllerTest.php                      |   3 +-
 tests/Feature/Repositories/Role/EloquentRoleTest.php                        |   4 +-
 tests/Feature/Repositories/User/EloquentUserTest.php                        |  36 +++++++----------
 45 files changed, 720 insertions(+), 644 deletions(-)
 ```

> **Note** If you don't write automated tests for your application, you don't have to update the files within `tests` directory.

<a name="upgrade-1.3.1"></a>
###To 1.3.1 from 1.3.0

This version contains only few bug fixes, and only few files has to be updated. Check the modified files below:

```
 app/Http/Controllers/InstallController.php |   2 +-
 app/Providers/HtmlServiceProvider.php      |   2 +-
 composer.lock                              | 266 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-----------------------------------------------------------------------
 config/app.php                             |   2 +-
 4 files changed, 142 insertions(+), 130 deletions(-)
```

<a name="upgrade-1.3.0"></a>
###To 1.3.0 from 1.2.1

Update to Laravel 5.4 for Vanguard has arrived. The best way to upgrade to version 1.3 is to follow [laravel upgrade guide](https://laravel.com/docs/5.4/upgrade) which will cover 99% of the things that should be updated. 

There was also one potential security issue related to avatar image upload which can be exploited on web servers where directory listing is allowed (such as default Apache configuration). To be sure that you are protected, please update `UsersController::updateAvatar` method, `ProfileController::updateAvatar` method, as well as `Vanguard\Services\Upload\UserAvatarManager` class.

There are a lot of modifications inside `tests` directory, but if you don't use automated tests to test your application, you don't have to update it.

Here is a list of modified files:

```
 app/Exceptions/Handler.php                                          |    2 +-
  app/Http/Controllers/ActivityController.php                         |    1 +
  app/Http/Controllers/Auth/SocialAuthController.php                  |    7 +-
  app/Http/Controllers/InstallController.php                          |    2 +-
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
  composer.lock                                                       | 1781 ++++++++++++++++++++++++++++++++++++++++++++++++++++++---------------------------------------------------------------------
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
  storage/settings.json                                               |    2 +-
  tests/Feature/FunctionalTestCase.php                                |  168 ++++++++++++
  tests/Feature/Http/Controllers/ActivityControllerTest.php           |   84 ++++++
  tests/Feature/Http/Controllers/Auth/AuthControllerTest.php          |  399 ++++++++++++++++++++++++++++
  tests/Feature/Http/Controllers/Auth/PasswordControllerTest.php      |  167 ++++++++++++
  tests/Feature/Http/Controllers/Auth/SocialAuthControllerTest.php    |  238 +++++++++++++++++
  tests/Feature/Http/Controllers/PermissionsControllerTest.php        |  183 +++++++++++++
  tests/Feature/Http/Controllers/ProfileControllerTest.php            |  326 +++++++++++++++++++++++
  tests/Feature/Http/Controllers/RolesControllerTest.php              |  134 ++++++++++
  tests/Feature/Http/Controllers/SettingsControllerTest.php           |   34 +++
  tests/Feature/Http/Controllers/UsersControllerTest.php              |  486 ++++++++++++++++++++++++++++++++++
  tests/Feature/Listeners/BaseListenerTestCase.php                    |   29 ++
  tests/Feature/Listeners/PermissionEventsSubscriberTest.php          |   38 +++
  tests/Feature/Listeners/RoleEventsSubscriberTest.php                |   44 ++++
  tests/Feature/Listeners/UserEventsSubscriberTest.php                |  148 +++++++++++
  tests/Feature/Repositories/Activity/EloquentActivityTest.php        |  128 +++++++++
  tests/Feature/Repositories/Country/EloquentCountryTest.php          |   34 +++
  tests/Feature/Repositories/Permission/EloquentPermissionTest.php    |   86 ++++++
  tests/Feature/Repositories/Role/EloquentRoleTest.php                |  106 ++++++++
  tests/Feature/Repositories/Session/DbSessionTest.php                |  109 ++++++++
  tests/Feature/Repositories/User/EloquentUserTest.php                |  379 ++++++++++++++++++++++++++
  tests/MailTrap.php                                                  |    4 +
  tests/TestCase.php                                                  |    9 +-
  tests/functional/FunctionalTestCase.php                             |  163 ------------
  tests/functional/Http/Controllers/ActivityControllerTest.php        |   81 ------
  tests/functional/Http/Controllers/Auth/AuthControllerTest.php       |  393 ---------------------------
  tests/functional/Http/Controllers/Auth/PasswordControllerTest.php   |  151 -----------
  tests/functional/Http/Controllers/Auth/SocialAuthControllerTest.php |  207 ---------------
  tests/functional/Http/Controllers/PermissionsControllerTest.php     |  180 -------------
  tests/functional/Http/Controllers/ProfileControllerTest.php         |  292 ---------------------
  tests/functional/Http/Controllers/RolesControllerTest.php           |  131 ---------
  tests/functional/Http/Controllers/SettingsControllerTest.php        |   29 --
  tests/functional/Http/Controllers/UsersControllerTest.php           |  447 -------------------------------
  tests/functional/Listeners/BaseListenerTestCase.php                 |   26 --
  tests/functional/Listeners/PermissionEventsSubscriberTest.php       |   36 ---
  tests/functional/Listeners/RoleEventsSubscriberTest.php             |   43 ---
  tests/functional/Listeners/UserEventsSubscriberTest.php             |  146 -----------
  tests/functional/Repositories/Activity/EloquentActivityTest.php     |  125 ---------
  tests/functional/Repositories/Country/EloquentCountryTest.php       |   31 ---
  tests/functional/Repositories/Permission/EloquentPermissionTest.php |   82 ------
  tests/functional/Repositories/Role/EloquentRoleTest.php             |  100 -------
  tests/functional/Repositories/Session/DbSessionTest.php             |   78 ------
  tests/functional/Repositories/User/EloquentUserTest.php             |  326 -----------------------
  tests/unit/Presenters/UserPresenterTest.php                         |    3 +
  webpack.mix.js                                                      |   15 ++
  75 files changed, 4469 insertions(+), 4358 deletions(-)
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