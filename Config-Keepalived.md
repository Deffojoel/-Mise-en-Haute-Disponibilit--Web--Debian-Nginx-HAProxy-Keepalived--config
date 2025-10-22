Keepalived est  Un superviseur qui donne une IP virtuelle (VIP) à un serveur. 

Si le maître tombe, le backup prend automatiquement cette IP. 



###### Installation 



sudo apt install -y keepalived



###### Configuration



**- config sur le load balancer 1 (maitre)**



sudo tee /etc/keepalived/keepalived.conf > /dev/null <<'EOF'

vrrp\_script chk\_haproxy {

&nbsp;   script "/usr/bin/pgrep haproxy"

&nbsp;   interval 2

&nbsp;   weight -20

}



vrrp\_instance VI\_1 {

&nbsp;   state MASTER

&nbsp;   interface ens34

&nbsp;   virtual\_router\_id 51

&nbsp;   priority 110

&nbsp;   advert\_int 1



&nbsp;   authentication {

&nbsp;       auth\_type PASS

&nbsp;       auth\_pass formatecinfo

&nbsp;   }

&nbsp;   virtual\_ipaddress {

&nbsp;       192.168.50.100/24 dev ens34

&nbsp;   }

&nbsp;   track\_script {

&nbsp;       chk\_haproxy

&nbsp;   }

}

EOF



sudo systemctl enable --now keepalived 



**- config sur le load balancer 2 (Backup)**



sudo tee /etc/keepalived/keepalived.conf > /dev/null <<'EOF'

vrrp\_script chk\_haproxy {

&nbsp;   script "/usr/bin/pgrep haproxy"

&nbsp;   interval 2

&nbsp;   weight -20

}



vrrp\_instance VI\_1 {

&nbsp;   state BACKUP

&nbsp;   interface ens34

&nbsp;   virtual\_router\_id 51

&nbsp;   priority 100

&nbsp;   advert\_int 1

&nbsp;   authentication {

&nbsp;       auth\_type PASS

&nbsp;       auth\_pass formatecinfo

&nbsp;   }

&nbsp;   virtual\_ipaddress {

&nbsp;       192.168.50.100/24 dev ens34

&nbsp;   }

&nbsp;   track\_script {

&nbsp;       chk\_haproxy

&nbsp;   }

}

EOF



sudo systemctl enable --now keepalived 



**test avec : watch -n1 curl -s http://192.168.50.100** 

