# Installing an Existing Plugin

Vanguard plugins can be distributed on multiple ways, either via composer or 
as a ZIP archive. 

**NOTE!** Use only plugins from the trusted sources. Plugins have access to 
all application files as well as your database and some malicious plugins can 
take all the data and the files from your application.

### Installing a Plugin via Composer

You can install Vanguard plugins via composer, just like any other composer package. 
Each plugin can have different necessary steps that you should perform during the 
installation, so make sure that you have followed the plugin installation guide.

After the successful installation you just need to register the plugin inside 
the `VanguardServiceProvider` and you are good to. 

Keep in mind though that you won't be able to edit the plugin files in this case 
since they will be inside the `/vendor` folder. If you want to be able to edit the 
plugin files, you will need to install it inside the `/plugins` folder, like it is 
described below.

### Installing a Plugin Manually

Let's say that we have a plugin named `Foo` that you have purchased from a trusted 
source and it was sent to you as a ZIP archive.

To install this plugin manually, you need to perform the following steps:

1) Extract the plugin zip archive to the `/plugins` folder located inside the 
Vanguard's root folder.

2) Update the `repositories` section in your **main** composer.json file by 
adding one more item as the following:

```json
{
    "type": "path",
    "url": "./plugins/Foo"
}
```


3) Add the following line to the `require` section in your **main** composer.json file:

```json
"vanguardapp/foo": "*"
```

In our case, the full name of the package is `vanguardapp/foo`, but some real 
package will probably have a different name, so make sure that you find the 
name of the package/plugin by checking the `name` property in plugin's `composer.json` 
file (in our case the path to plugin's composer.json file 
is `/plugins/Foo/composer.json`).


4) Follow the plugin installation guide and run all the commands required for 
the plugin to be installed properly.

After the successful installation you just need to register the plugin inside 
the `VanguardServiceProvider` and you are good to.