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
`sudo chown -R $USER:$USER /var/www/e-xpert.pl/public_html`<br />
`sudo mkdir /etc/httpd/sites-available`<br />
`sudo mkdir /etc/httpd/sites-enabled`<br />

### Modification of /etc/httpd/conf/httpd.conf
Add `IncludeOptional sites-enabled/*.conf` line at the end of the file<br />

### Setting up virtual host config file
`sudo nano /etc/httpd/sites-available/e-xpert.pl.conf`<br />

```
<VirtualHost *:80>
    ServerName www.e-xpert.pl
    ServerAlias e-xpert.pl
    DocumentRoot /var/www/e-xpert.pl/public_html
    ErrorLog /var/www/e-xpert.pl/error.log
    CustomLog /var/www/example.com/requests.log combined
</VirtualHost>
```
<br />

`sudo ln -s /etc/httpd/sites-available/example.com.conf /etc/httpd/sites-enabled/example.com.conf`
`sudo apachectl restart`
