This folder contains the authentication file I use on scripts.mit.edu to authenticate users via their MIT certificates for kswak account creation and login. My web_scripts folder contains all files found in this directory, the most important of which is auth.php, which is accessed via https://sarivera.scripts.mit.edu:444/auth.php and prompts the users for a certificate (specifically because of https:// and :444). 

The code is a basic PHP script that reads the Kerberos of the user and encrypts their username using SlowAES and a version of base64 encoding for URL safety. The script also creates a password for the user by concatenating a master password to their name and calculating the md5 hash of that. That hash is used as the users password for kswak, but they never need to remember it or type it in because the password is used for logging in through the server. 

Keep in mind that this specific auth.php file IS ONLY A TEMPLATE!!!! You need to assign the ENCRYPTION_KEY and MASTER variables accordingly so that they match those found in the settings.json file in config/. As such, this script without modification will NOT work in conjunction with kswak if copied and pasted into a scripts locker.

The script on https://sarivera.scripts.mit.edu:444/auth.php currently works for kswak! But, if you choose to change the script, keep in mind that you must change the url in the settings.json file to reflect this.

Common issues:
If the server says something like:
Exception while invoking method 'kswak_login' undefined
the problem is probably your MASTER and ENCRYPTION_KEY variables. They must match on the script and kswak! If they don't this (shitty) error message will appear.
