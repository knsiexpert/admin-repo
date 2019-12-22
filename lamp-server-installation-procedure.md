### In case of minimal installation

`sudo yum update`<br />
`sudo yum install httpd`<br />
`sudo systemctl start httpd.service`<br />
`sudo systemctl enable httpd.service`<br />
`sudo yum install mariadb-server mariadb`<br />
`sudo systemctl start mariadb`<br />
`sudo mysql_secure_installation`<br />
`sudo systemctl enable mariadb.service`<br />
`sudo yum install php php-mysql`<br />
`sudo systemctl restart httpd.service`<br />

### Setting up directory for e-xpert.pl

`sudo chmod -R 755 /var/www`<br />
`sudo mkdir -p /var/www/e-xpert.pl/public_html`<br />
`sudo chown -R apache: /var/www/e-xpert.pl/public_html`<br />


### Setting up virtual host
`sudo nano /etc/httpd/conf.d/e-xpert.pl.conf`<br />

```
<VirtualHost *:80>
    ServerName www.e-xpert.pl
    ServerAlias e-xpert.pl
    DocumentRoot /var/www/e-xpert.pl/public_html
    
    <Directory /var/www/e-xpert.pl/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
    
    ErrorLog /var/www/e-xpert.pl/error.log
    CustomLog /var/www/e-xpert.pl/requests.log combined
</VirtualHost>
```
<br />
`sudo apachectl restart`<br />
