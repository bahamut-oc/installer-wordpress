Installation des paquets (les services)
apt install php nginx mysql-server

Installation des extensions
apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-zip php-bcmath php-intl php-soap php-exif php-imagick

Contrôler les versions des services
php -v
mysql -v
nginx -v

Activer et démarrer les services
systemctl enable nginx && systemctl start nginx
systemctl enable php8.1-fpm && systemctl start php8.1-fpm
systemctl enable mysql && systemctl start mysql

Vérifier l’activation des services
systemctl status nginx
systemctl status php8.1-fpm
systemctl status mysql

Créer la configuration Nginx pour le site
rm /etc/nginx/sites-enabled/default
nano /etc/nginx/sites-available/xtendoptic.com
ln -s /etc/nginx/sites-available/xtendoptic.com /etc/nginx/sites-enabled/

Recharger les services
nginx -t
systemctl restart nginx
systemctl restart php8.1-fpm
systemctl restart mysql

Nettoyage du repertoire
ls /var/www/html/
rm -rf /var/www/html/*
rm -rf /var/www/html/.* 2>/dev/null

Télécharger et installer WordPress
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
cp -a wordpress/. /var/www/html/

Définir les bonnes permissions
chown -R www-data:www-data /var/www/html/
chmod -R 755 /var/www/html/

ip a

mysql -u root -p

CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'AOImfW1wRk1lilTj';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
