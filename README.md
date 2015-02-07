
WHAT THIS MODULE IS GOOD FOR
----------------------------
This module can basically be useful in 2 ways:
1. For making your users passwords readable by admins.
2. As a very simple general purpose AES encryption API to use in other modules.

INSTALATION
-----------

Install this module using the official Backdrop CMS instructions at https://backdropcms.org/guide/modules

Visit the configuration page under Administration > Configuration > AES settings (admin/config/system/aes) and select required configurations options.

LICENSE
-------

This project is GPL v2 software. See the LICENSE.txt file in this directory for complete text.

CURRENT MAINTAINERS
-------------------

Shurik Barkov (https://github.com/ShurikBarkov)
Dennis Povshedny (https://github.com/dpovshed)

CREDITS
-------

This module was originally written for Drupal 6.x by easyfit, and was maintained briefly by EvanDonovan, primarily for 7.x, since it was a requirement for the Salesforce Suite prior to the new 7.x-3.x branch.
Since January 2014 module is maintained by dpovshed.


HOW TO GET AN AES IMPLEMENTATION
--------------------------------
If you don't have an AES implementation (you'll notice this when you install this module) then the easiest implementation for you to get is probably the PHP Secure Communications Library (phpseclib).

Just download the latest version from http://phpseclib.sourceforge.net/ and extract it into a directory called "phpseclib" inside the aes directory. Note that the zip file of the version of phpseclib that this module was developed with doesn't create the phpseclib directory itself, it just extracts its various directories directly into the location you unzip it, so create that "phpseclib" directory first and then move the zip file into it, and unzip. The complete path to the file which will be included by this module (AES.php) should look like this:
aes/phpseclib/Crypt/AES.php . You also may install PhpSecLib as a regular Drupal library.

That's it! Try installing/enabling the module again.

This module was developed using phpseclib version 1.5, but hopefully future versions should work as well (and might contain security bug fixes, so always get the latest). If you've got a version of phpseclib that's newer than 1.5 and you're running into trouble, then please create an issue at drupal.org/project/aes

If you want to use the Mcrypt implementation instead then you can find information on how to install it here: http://php.net/mcrypt
Note that you most likely need to be running your own webserver in order to install Mcrypt. If you're on a shared host you'll probably have to ask your hosting provider to install Mcrypt for you (or use phpseclib instead).

ABOUT KEY STORAGE METHODS
-------------------------
Something you should pay attention to (if you want any sort of security) is how you store your encryption key. You have the option of storing it in the database as a normal Drupal variable, this is also the default, but it's the default only because there is no good standard location to store it. Switching to a file-based storage is strongly encouraged since storing the key in the same database as your encrypted strings will sort of nullify the point of them being encrypted in the first place. Also make sure to set the permission on the keyfile to be as restrictive as possible, assuming you're on a unix-like system running apache, I recommend setting the ownership of the file to apache with the owner being the only one allowed to read and write to it (0600). Above all make sure that the file is not readable from the web! The easiest way to do that is probably to place it somewhere outside the webroot.
