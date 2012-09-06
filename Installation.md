_This was copied from Google-cache version of installation documentation at trac.usvn.info. The sites www.usvn.info and trac.usvn.info were down when I was attempting to install USVN. So, it made sense to put some of this documentation on GitHub as it is probably a little more reliable than usvn.info. Unfortunately, several images are missing and the documentation is not quite complete. Please update this page if you have some time and knowledge of the installation process._

# Dependencies

* PHP 5 (5.1.2 <= ver < 5.3)
* apache2
* mod_dav enable (in Apache httpd.conf - DSO support - "LoadModule dav_module modules/mod_dav.so")
* mod_dav_fs enable (in Apache httpd.conf - DSO support - "LoadModule dav_fs_module modules/mod_dav_fs.so")
* mod_rewrite enable (in Apache httpd.conf - DSO support - "LoadModule rewrite_module modules/mod_rewrite.so")
* proper AllowOverride configuration (see below example - "AllowOverride All")
* Subversion - below modules are packed in most binary distributions
* mod_authz_svn enable (in Apache httpd.conf - DSO support - "LoadModule authz_svn_module modules/mod_authz_svn.so")
* mod_dav_svn enable (in Apache httpd.conf - DSO support - "LoadModule dav_svn_module modules/mod_dav_svn.so")

# Apache Configuration Example

## Configure access to usvn

    Alias /usvn /path/to/usvn/public
    <Directory "/path/to/usvn/public">
        Options +SymLinksIfOwnerMatch
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>

## Apache configure access to usvn with https

    <Directory /srv/www/htdocs/usvn>
        <IfDefine SSL>
            SSLRequireSSL On
        </IfDefine>
        Options +FollowSymlinks
        AllowOverride FileInfo Limit
    </Directory>

# Configure access to usvn
    Alias /usvn /srv/www/htdocs/usvn/public
    <Directory "/srv/www/htdocs/usvn/public">
        Options +SymLinksIfOwnerMatch
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>

    <Location /usvn/svn/>
        DAV svn
        Require valid-user
        SVNParentPath /srv/www/htdocs/usvn/files/svn
        SVNListParentPath off
        AuthType Basic
        AuthName "USVN"
        AuthUserFile /srv/www/htdocs/usvn/files/htpasswd
    </Location>

# Install USVN

To use USVN you need to install PHP 5 and Apache on your computer. After this, download USVN and uncompress the archive into a directory accessible by Apache. After that with your web browser go to usvn location and the installation will start.

In this step, choose your SQL adapter

At the end of the installation, USVN will display the configuration that you have to copy paste into your apache httpd.conf

And that's all. Now you can create and administrate subversion repositories.

# Commons problems

## Subversion is not installed on your system

If at the begining of the installation you see that kind of message:

It's means that you need to install the subversion binaries.

## Windows

Download and install:  http://subversion.tigris.org/files/documents/15/36797/svn-1.4.3-setup.exe

Don't forget to restart your computer after this step.

If you do have subversion installed

Alternatively, if you have subversion installed, you should add the 'bin' folder to your PATH (right click on my computer, properties, advanced, environment variables.

Find 'Path' under 'system variables', at the end, add a semicolon (;) with the full path of the 'bin' folder of your installation e.g. c:\Program Files\Subversion\bin

It is important to restart Apache after that. Do not use the Apache monitor, otherwise the path will not be updated for PHP: Right click on My Computer, and choose 'manage' from the menu. Double click 'services and applications' and then 'services'. Find your apache server in there, right click and choose 'restart'. After this, you don't need to restart your computer.

## Unix

On ubuntu or debian type:

    sudo apt-get install subversion

## The mysql driver is not currently installed

During the installation, if you see that kind of message:


It's means that you need to install the pdo mysql driver.

## Error 500 after the install

If you have an error 500 after the installation please activate the RewriteUrl? module into your apache configuration.

On most unix systems:

    a2enmod rewrite

Apache won't reboot

After the installation, if when you reboot apache you get the message Invalid command 'Dav.

It's means that you need to install the mod subversion for apache.

On debian or ubuntu type:

    apt-get install libapache2-subversion

## Error 404 after the installation

If you have an error 404 after the installation please authorize override of apache by .htaccess.

In configuration of /var/www (adapt path to your location) replace:

    AllowOverride none

By:

    AllowOverride all

## SQLSTATE[HY000]: General error: 2050

It's a bug with the pdo_mysql_driver in config.ini replace. Use MYSQLI driver instead PDO_MYSQL.

## Parse error: syntax error, unexpected T_OBJECT_OPERATOR in

USVN need PHP 5 and you use PHP 4. The only solution is upgrade to PHP 5.

## Config file creation fail


You can create two files named config.ini and .htaccess . Theses files must be writable by your httpd user and you must check rights access twice.

You also have to put this bloc in config.ini

    [general]