# Dependencies
* PHP 5 (> 5.1.2)
* apache2
* mod_dav enable (in Apache httpd.conf - DSO support - "LoadModule dav_module modules/mod_dav.so")
* mod_dav_fs enable (in Apache httpd.conf - DSO support - "LoadModule dav_fs_module modules/mod_dav_fs.so")
* mod_rewrite enable (in Apache httpd.conf - DSO support - "LoadModule rewrite_module modules/mod_rewrite.so")
* proper AllowOverride configuration (see below example - "AllowOverride All")
* Subversion - below modules are packed in most binary distributions
* mod_authz_svn enable (in Apache httpd.conf - DSO support - "LoadModule authz_svn_module modules/mod_authz_svn.so")
* mod_dav_svn enable (in Apache httpd.conf - DSO support - "LoadModule dav_svn_module modules/mod_dav_svn.so")

# Apache Configuration Example

    # Configure access to usvn
    Alias /usvn /path/to/usvn/public
    <Directory "/path/to/usvn/public">
        Options +SymLinksIfOwnerMatch
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>

# Install USVN

To use USVN you need to install PHP 5 and Apache on your computer. After this, download USVN and uncompress the archive into a directory accessible by Apache. After that with your web browser go to usvn location and the installation will start.