## The gist of it ##
Paranoia is a way to keep your application profiles more secure by helping
you sync them between a tmpfs and encrypted medium.

If you are paranoid like me, you don't want your firefox .mozilla directory 
accessible by anyone who can gain physical access to your computer.

I use a tmpfs directory so I can pull my encrypted thumbdrive and go to lunch 
while my browser crunches away at something. At the end of the day, I sync the 
profile from the tmpfs to my encrypted thumbdrive. It then kills (shreds) the 
entire tmpfs directory and firefox is no longer workable.

It's not limited to .mozilla profiles. It can be used for anything that stores 
data in, say, your home directory.

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

If you just want to create an SSH session for your key:

cat@cats ~ $ `paranoia -i /path/to/id_rsa`

NOTE: The above just uses ssh-add and an expiration of 21600 seconds.

Every once in a while you will want to sync your session (or not):

cat@cats ~ $ `paranoia -s`

Then, at the end of the day, you will want to kill your session and erase it 
from the tmpfs:

cat@cats ~ $ `paranoia -k -s` - the `-s` is so you can sync it back to your secure location.
