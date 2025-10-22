###### Cmd pour créer un nouvelle utilisateur :



sudo adduser alice

sudo passwd alice





###### cmd pour installer sudo : 



**su - // super utilisateur**

**apt install -y sudo** 



###### **cmd pour add un utilisateur a un groupe** 



**usermod -aG sudo formatec (on add formatec au groupe sudo)**



###### **repertoire pour acceder a sudoersg**



**/etc/sudoers**



###### **Nettoyage avant clonage** 



**Supprime l’historique et fichiers uniques :** 



**sudo apt clean** 

**sudo rm -rf /tmp/\*** 

**sudo rm -f /etc/ssh/ssh\_host\_\*** 

**sudo truncate -s 0 /var/log/\*.log** 

**history -c** 



