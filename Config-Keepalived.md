Keepalived est  Un superviseur qui donne une IP virtuelle (VIP) à un serveur. 

Si le maître tombe, le backup prend automatiquement cette IP. 



###### Installation 



sudo apt install -y keepalived



###### Configuration



**- config sur le load balancer 1 (maitre)**



sudo tee /etc/keepalived/keepalived.conf > /dev/null <<'EOF'
vrrp_script chk_haproxy {
    script "/usr/bin/pgrep haproxy"
    interval 2
    weight -20
}

vrrp_instance VI_1 {
    state MASTER
    interface ens37
    virtual_router_id 51
    priority 110
    advert_int 1

    authentication {
        auth_type PASS
        auth_pass formatecinfo
    }

    virtual_ipaddress {
        192.168.50.100/24 dev ens37
    }

    track_script {
        chk_haproxy
    }
}
EOF


**- config sur le load balancer 2 (Backup)**

sudo tee /etc/keepalived/keepalived.conf > /dev/null <<'EOF'
vrrp_script chk_haproxy {
    script "/usr/bin/pgrep haproxy"
    interval 2
    weight -20
}

vrrp_instance VI_1 {
    state BACKUP
    interface ens37
    virtual_router_id 51
    priority 100
    advert_int 1

    authentication {
        auth_type PASS
        auth_pass formatecinfo
    }

    virtual_ipaddress {
        192.168.50.100/24 dev ens37
    }

    track_script {
        chk_haproxy
    }
}
EOF



sudo systemctl enable --now keepalived 



**test avec : watch -n1 curl -s http://192.168.50.100** 

