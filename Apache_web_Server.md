### Apache HTTP Server  ###

```sh
sudo yum update httpd
```
```ruby
rpm -q httpd or rpm -qa | grep -i http
```
> check for Apache
```java
sudo yum install httpd
```
```xml
sudo firewall-cmd --permanent --add-service=http
or sudo firewall-cmd ––permanent ––add-port=80/tcp
sudo firewall-cmd --permanent --add-service=https
or sudo firewall-cmd ––permanent ––add-port=443/tcp
```
sudo firewall-cmd --reload

sudo systemctl start/stop/reload/restart httpd
sudo systemctl status httpd

hostname -I
curl -4 icanhazip.com
http://your_server_ip

— Setting Up Virtual Hosts (Recommended)
sudo mkdir /var/www/MyWebsite/{public_html, logs}
sudo chmod -R 755 /var/www
sudo systemctl restart httpd

- Test wich port Appatche is listedning 

# %%%%%%%%%%%%%%%%%%%%%%% HTTPS/SSL %%%%%%%%%%%%%%%%%%%%%
yum install openssl mod_ssl or
yum install mod_ssl
sudo systemctl restart httpd or service httpd restart


Copy the certificate to the path, for example /etc/pki/tls/certs/www.example.com.crt
mv /etc/httpd/conf/httpsd.key /etc/pki/tls/private/server.key
mv /etc/httpd/conf/httpsd.crt /etc/pki/tls/certs/server.crt

    Edit 
/etc/httpd/conf.d/ssl.conf. 
    Change the SSLCertificateFile and SSLCertificateKey lines to be.
SSLCertificateFile /etc/pki/tls/certs/www.example.com.crt
SSLCertificateKeyFile /etc/pki/tls/private/www.example.com.key

service httpd start
----------------------- ## ProxyPass ----------------------------

[user@server conf.d]$ cat bolt.conf
ProxyPass "/bolt/api" "http://localhost:8080/bolt/api"
ProxyPassReverse "/bolt/api" "http://localhost:8080/bolt/api"

ProxyPass "/bolt/oauth" "http://localhost:8080/bolt/oauth"
ProxyPassReverse "/bolt/oauth" "http://localhost:8080/bolt/oauth"


## KEY ---------------------------------------------------------
----------
$ netstat -tupan | grep -i http or $ netstat -tupan | grep -i '80\|443'
ps aux | grep -i[h]ttp

httpd -t > Check the Syntax
httpd -v > Check installed apache version

Configuration Files
1- /etc/httpd/conf/httpd.conf
2- /etc/httpd/conf.d/*.conf

# View all active cofiguration
$cat httpd.conf | grep -v '^$\|^\s*#'

 > Log Files
/var/log/httpd/*

PID File 
/var/log/httpd/httpd.pid

startup script
/usr/lib/systemd/httpd.service
/etc/init.d/httpd

################## Create the Virtual Host #################

mkdir /var/www/html/example.com
chown apache:apache /var/www/html/example.com
vi index.html // echo Apache on RHEL 8 / CentOS 8 > /var/www/html/example.com/index.html
```ruby
<VirtualHost *:80>
  ServerName www.example.com
  ServerAlias example.com *.example.com
  ServerAdmin webmaster@example.com
  DocumentRoot /var/www/html/example.com
  ErrorLog /logs/example.com/error.log
  CustomLog /logs/example.com/access.log common
  DirectoryIndex index.html
</VirtualHost>
```

Note: The SSL config file can be in a <VirtualHost> block in another config file. 
You can always search for the SSL conf file on Linux distributions using this grep command:
```cmd
$ grep -i -r “SSLCertificateFile” /etc/httpd/
```
Configure the httpd.conf file and enter the following commands on your VirtualHost to successfully enable SSL:
```shell
<VirtualHost [IP ADDRESS]:443>
  ServerAdmin webmaster@ssl-tutorials.com
  DocumentRoot var/www
  ServerName www.ssl-tutorials.com
  ErrorLog www/home/logs/error_log
  SSLEngine on
  SSLCertificateFile /etc/ssl/ssl-tutorials_com.crt
  SSLCertificateKeyFile /etc/ssl/ssl-tutorials.key
  SSLCertificateChainFile /etc/ssl/ssl-tutorials_com.ca-bundle
</VirtualHost> 
```

