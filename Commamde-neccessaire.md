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


###### **config des interfaces sur Linux** 

**chemin : /etc/network/interfaces*** 

**
#interface en DHCP
auto enp0s3
allow-hotplug enp0s3
iface enp0s3 inet dhcp
*** 

**
#interface en Static
auto enp0s3
allow-hotplug enp0s3
iface enp0s3 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 1.1.1.1 8.8.8.8

*** 

