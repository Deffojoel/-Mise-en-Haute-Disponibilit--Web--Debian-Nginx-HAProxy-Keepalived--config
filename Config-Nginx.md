NGINX est Un petit serveur web qui répond sur le port 80 et affiche des pages HTML.



###### Installation : 



sudo apt install -y nginx 



###### Configuration :



# Créer le fichier index.html avec un contenu simple
echo "Site A - Serveur WEB1" | sudo tee /var/www/site/index.html

# Créer le fichier de configuration Nginx pour le site
sudo tee /etc/nginx/sites-available/site > /dev/null <<'EOF'
server {
    listen 80;
    server_name _;

    root /var/www/site;
    index index.html;
}
EOF

* sudo ln -s /etc/nginx/sites-available/site /etc/nginx/sites-enabled/site 
* sudo rm -f /etc/nginx/sites-enabled/default 
* sudo systemctl restart nginx 
