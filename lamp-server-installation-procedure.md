sudo yum update
sudo yum install httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
sudo yum install mariadb-server mariadb
sudo systemctl start mariadb
sudo mysql_secure_installation
sudo systemctl enable mariadb.service
sudo yum install php php-mysql
sudo systemctl restart httpd.service

# Setting up directory for e-xpert.pl

sudo chmod -R 755 /var/www
sudo mkdir -p /var/www/e-xpert.pl/public_html
sudo chown -R $USER:$USER /var/www/e-xpert.pl/public_html
sudo mkdir /etc/httpd/sites-available
sudo mkdir /etc/httpd/sites-enabled

# /etc/httpd/conf/httpd.conf
Add `IncludeOptional sites-enabled/*.conf` line at the end of the file

# Setting up virtual host config file
sudo nano /etc/httpd/sites-available/e-xpert.pl.conf

```
<VirtualHost *:80>
    ServerName www.e-xpert.pl
    ServerAlias e-xpert.pl
    DocumentRoot /var/www/e-xpert.pl/public_html
    ErrorLog /var/www/e-xpert.pl/error.log
    CustomLog /var/www/example.com/requests.log combined
</VirtualHost>
```

sudo ln -s /etc/httpd/sites-available/example.com.conf /etc/httpd/sites-enabled/example.com.conf
sudo apachectl restart
