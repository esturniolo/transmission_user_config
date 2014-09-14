transmission_user_config
========================

La manera correcta (?) para poder configurar el usuario de Transmission y que no de error de escritura.


via http://askubuntu.com/questions/221081/permission-denied-when-downloading-with-transmission-deamon



Assuming the path to the download folder is /home/chen/TV shows, run the following:

add chen to the debian-transmission group

sudo usermod -a -G debian-transmission chen

change the folder ownership

sudo chgrp debian-transmission /home/chen/TV\ shows

grant write access to the group

sudo chmod 770 /home/chen/TV\ shows

Stop the deamon with  sudo service transmission-daemon stop

The last thing to do is change the file creation mask, so that the downloaded files would be writeable by chen.

sudo nano /etc/transmission-daemon/settings.json
...and change "umask": 18 to "umask": 2. Hit ctrl+o to save and ctrl+x to exit.

Start the daemon with sudo service transmission-daemon start
