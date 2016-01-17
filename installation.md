#Installation

* [Installation](#installation)
	* [Server Requirements](#server-requirements)
	* [Installing Vanguard](#installing-vanguard)

---
<a name="installation"></a>
##Installation

<a name="server-requirements"></a>
###Server Requirements

In order to install Vanguard application, your server must meet following requirements:


* PHP >= 5.5.9
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension

<a name="installing-vanguard"></a>
###Installing Vanguard

After downloading the ZIP archive, and uploading it to your server, first thing you have to do is to create the database where system tables will be created. Let's say, you create the database called **vanguard**.

####Step 1 - Welcome Screen
After creating the database next step is accessing the system URL from a browser. Since this is the first time that you are accessing the system, the installation wizard, will be displayed.

![alt Vanguard Installation - Welcome Screen](assets/img/install_step1.png)

####Step 2 - System Requirements

After clicking on "Next" button, you will be redirected to second step during the installation wizard, System Requirements. 

![alt Vanguard Installation - System Requirements](assets/img/install_step2.png)

In order to install the script, your system must have installed and enabled all PHP extensions listed on that second installation step.

####Step 3 - Directory Permissions

After successfully enabling and installing all required PHP extensions, next step is to set the appropriate permissions for some system folders. All directories listed on the step 3 has to be writable by the application, as it is displayed on following picture.

![alt Vanguard Installation - Directory Permissions](assets/img/install_step3.png)

After making all those directories writable by changing their permissions to ```777``` (or ```775```,  if owner of your files is webserver user), you are ready to proceed to next step and insert your database credentials.

####Step 4 - Database Info

On step 4 you have to fill in your database credentials and choose a prefix for your database tables if you want. Of course, you can leave prefix field empty if you don't want your database tables to be prefixed.

![alt Vanguard Installation - Database Credentials](assets/img/install_step4.png)

If you have any problems saying that Vanguard is unable to connect to your database, you can check error log inside `storage/logs` directory for more informations about the error.

####Step 5 - Installation

After passing all those steps, you are now ready to install your application. If you want, you can change application name to something else by typing the application name here, before you press Install button. 

![alt Vanguard Installation - Installation](assets/img/install_step5.png)

Once you are ready, just press the **Install** button and installation process will start immediately. It should not take more than few seconds.

####Step 6 - Complete Installation

Once application is successfully completed, you will see the last step from installation wizard, as per below

![alt Vanguard Installation - Installation Completed](assets/img/install_step6.png)

> **Note!** Since your root directory is still writable by the group, you should now change the permissions to `755` and make it writable only by root system user. This is for security reasons.