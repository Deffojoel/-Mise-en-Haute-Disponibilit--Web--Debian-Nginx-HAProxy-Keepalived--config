NGINX est Un petit serveur web qui répond sur le port 80 et affiche des pages HTML.



###### Installation : 



sudo apt install -y nginx 



###### Configuration :



* sudo mkdir -p /var/www/site 
* echo "<h1>Site A - Serveur WEB1</h1>" | sudo tee /var/www/site/index.html 
* sudo tee /etc/nginx/sites-available/site <<'EOF'

server {

&nbsp; listen 80;

&nbsp; server\_name \_;

&nbsp; root /var/www/site;

&nbsp; index index.html;

}

EOF

* sudo ln -s /etc/nginx/sites-available/site /etc/nginx/sites-enabled/site 
* sudo rm -f /etc/nginx/sites-enabled/default 
* sudo systemctl restart nginx 
