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

frontend fe_http
    bind *:80
    default_backend be_sites

backend be_sites
    balance roundrobin
    option httpchk GET /
    server web1 192.168.50.11:80 check
    server web2 192.168.50.12:80 check
EOF



sudo systemctl enable --now haproxy 

