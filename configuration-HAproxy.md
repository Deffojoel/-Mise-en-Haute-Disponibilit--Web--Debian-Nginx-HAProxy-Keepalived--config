HAproxy Un répartiteur de charge : il envoie les visiteurs vers le serveur le moins occupé.



###### Installation : 



sudo apt install -y haproxy 



###### Configuration : 



sudo tee /etc/haproxy/haproxy.cfg > /dev/null <<'EOF'

global 

log /dev/log local0 

maxconn 4096 

daemon 

defaults 

log     global 

mode    http 

option  httplog 

timeout connect 5s 

timeout client  30s 

timeout server  30s 

&nbsp;

frontend fe\_http 

&nbsp;   bind \*:80 

&nbsp;   default\_backend be\_sites 

&nbsp;

backend be\_sites 

&nbsp;   balance roundrobin 

&nbsp;   option httpchk GET / 

&nbsp;   server web1 192.168.50.11:80 check 

&nbsp;   server web2 192.168.50.12:80 check 

EOF



sudo systemctl enable --now haproxy 

