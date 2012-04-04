## The gist of it ##
Paranoia is a way to keep your application profiles more secure.

## Installation ##

You need to create a temporary trashable directory. The best is a small tmpfs 
mount in your home directory. You will also need a secure device like an 
encrypted thumbdrive to store the profiles on.

    cd /path/to/paranoia
    sudo make install
    touch ${HOME}/.paranoiarc
    echo SECURE_BASE_DIR="/path/to/secure/dir" >> ~/.paranoiarc
    echo TMPFS_MOUNT_POINT="/path/to/trashable/dir" >> ~/.paranoiarc
    echo PROFILES_TO_MANAGE=(.mozilla .other_secure_profile) >> ~/.paranoiarc

## Use it ##

Creating a secure session:

cat@cats ~ $ `paranoia -c`

If you want to include adding a ssh identity to your ssh agent:

cat@cats ~ $ `paranoia -c -i /path/to/id_rsa`

Every once in a while you will want to sync your session (or not):

cat@cats ~ $ `paranoia -s`

Then, at the end of the day, you will want to kill your session and erase it 
from the tmpfs:

cat@cats ~ $ `paranoia -k -s` - the `-s` is so you can sync it back to your secure location.
