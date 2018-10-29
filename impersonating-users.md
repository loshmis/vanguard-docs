#Impersonating Users

* [Impersonating Users](#impersonating-users)
	* [How to Impersonate a User](#how-to-impersonate-a-user)
	* [Stop Impersonating](#stop-impersonating)
	* [Changing Permissions](#changing-permissions)
	
---

<a name="impersonating-users"></a>
##Impersonating Users

All Vanguard users with `users.manage` permission can impersonate other system users.
This is very handy feature when your users report some bugs and when you need to see the
application exactly how they can see it. Instead of asking them for their credentials
you can simply impersonate them.

<a name="how-to-impersonate-a-user"></a>
###How to impersonate a user?

One way to impersonate a user is from a user list page, as displayed on the image below:

![Vanguard - Impersonate User from User List Page](assets/img/impersonate-user-list.png)

Users can also be impersonated from their profile page:

![Vanguard - Impersonate User from Profile Page](assets/img/impersonate-user-profile.png)

<a name="stop-impersonating"></a>
##Stop Impersonating

While you are impersonating a user, you can do everything that the user can do himself.
Once you are done and you want to return to your account and stop impersonating the user,
just click on the "Stop Impersonating" button inside the header.

![Vanguard - Stop Impersonating](assets/img/stop-impersonating.png)

<a name="changing-permissions"></a>
##Changing Permissions

If you want to customize who can impersonate other users or which users can be impersonated,
you can do that by updating appropriate methods inside  `app/Support/CanImpersonateUsers.php` file.
