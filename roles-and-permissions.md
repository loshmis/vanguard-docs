#Roles And Permissions

* [Roles And Permissions](#roles-and-permissions)
	* [Available System Roles](#roles-available)
	* [Managing Roles](#roles-manage)
	* [System Permissions](#permissions)
	* [Managing Permissions](#permissions-manage)
	
---

<a name="roles-and-permissions"></a>
##Roles and Permissions

Vanguard comes with advanced roles and permissions mechanism based on [Entrust](https://github.com/Zizaco/entrust) package. System is created to allow users to have **only one** role, and to allow different permissions for each role.

<a name="roles-available"></a>
###Available System Roles

On roles section of the website administrators (or other users with appropriate permissions) can see and manage available system roles, as well as add unlimited number of new roles. Page with default system roles (**Admin** and **User**) is provided below.

![Vanguard - Roles](assets/img/roles-list.png)

>**Note!** Default system roles cannot be deleted from UI. Custom created roles can be deleted without any problem.

<a name="roles-manage"></a>
###Managing Roles

As it was already mentioned, users with appropriate permissions can add unlimited number of roles, and use them to customise the application. More on that can be found in [customisation](customisation) section.

Form for adding new role, and editing existing roles, is provided below.

![Vanguard - Roles](assets/img/roles-add.png)

Every role has **name**, that is used as key inside the source code of application. Display name is used inside the UI to better explain who is this role referring to.

<a name="permissions"></a>
###System Permissions

Permissions represent some concrete actions that specific role can perform. For example, one of default permissions is `users.manage`, and every user with role which has this permission can manage system users. 

This means that, for example, you can create new system role called `Manager`, and allow managers to only edit system users, without them being able to update system settings etc.

>**Note!** Default system permissions cannot be deleted from UI. Custom created permissions can be deleted without any problem.

<a name="permissions-manage"></a>
###Managing Permissions

List of available permissions, including available system roles and their permissions, is provided below.

![Vanguard - Permissions](assets/img/permissions-list.png)

If we want, for example, to allow system users with role `User` to be able to View System Activity Log, all we have to do is to check the corresponding checkbox for that role, and click **Save Permissions** button at the bottom of the page. After that all users will be able to see Activity Log in sidebar menu as well as to access the activity log for all system users.

Vanguard support unlimited number of permissions, and they can be added via form provided below.

![Vanguard - Permissions](assets/img/permissions-add.png)

Permission **name** is used as key/constant inside the source code to check if user has permissions to perform some action (more on that inside [custom registration form example](registration-form.html)), and **display name** is used inside the UI, to better explain what the permission is used for.