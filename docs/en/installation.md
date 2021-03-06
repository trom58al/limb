# How to setup Limb3 based project
To setup Limb3 based project first create a directory somewhere inside your root web folder, say **/var/www/limbapp**. The easiest way to start Limb3 is to download sandbox application (empty application with minimum design and with bundled main Limb3 packages) from SourceForge http://sourceforge.net/project/showfiles.php?group_id=109345&package_id=239481.

After you downloaded limb-app to the following::

* Unpack limb-app archive into you project directory /var/www/limbapp. (we consider /var/www — is your document root and available via web server as http://localhost)
* Make sure Apache has write permition for /var/www/limbapp/var. If not then just type:

        $ chmod 777 /var/www/limbapp/var

That it!

Now you can check your installation by typing http://localhost/limbapp/www in you browser. If everything is ok, you will see something like this:

![Alt-limb_app](http://wiki.limb-project.com/2011.1/lib/exe/fetch.php?cache=&media=limb3:en:limb_app.png)

You can also may want to setup virtual host for your project:

* Add a new host for limbapp in Apache httpd.conf file:

        <VirtualHost *>
          DocumentRoot /var/www/limbapp/www/
          ServerName limbapp
          ErrorLog logs/limbapp-error_log
          CustomLog logs/limbapp-access_log common
        </VirtualHost>

* Add limbapp ip-address in /etc/hosts(or %WINDOWS%/system32/drivers/etc/hosts for Windows):

        127.0.0.1  limbapp

* Restart Apache
* Type http://limbapp/ in you browser
