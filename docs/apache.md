### I need apache to redirect my request https://pingfederate.local/authorize to https://localhost:9031/as/authorization.oauth2
I have 127.0.0.1 pingfederate.local in /etc/hosts

1. execute these commands to create the certs:
```
cd /etc/apache2/other
sudo openssl genrsa -out server.key 1024
sudo openssl req -new -key server.key -out server.csr
sudo openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```
2. create /etc/apache2/other/ping.conf with the following content
```
Listen 443
<IfModule !ssl_module>
    LoadModule ssl_module libexec/apache2/mod_ssl.so
</IfModule>
<VirtualHost *:443>
    ServerName pingfederate.local
    SSLEngine on
    SSLCertificateFile "/etc/apache2/other/server.crt"
    SSLCertificateKeyFile "/etc/apache2/other/server.key"
    Redirect /authorize https://localhost:9031/as/authorization.oauth2
</VirtualHost>
```

### I just need step 2 to redirect http://pingfederate.local/authorize to https://localhost:9031/as/authorization.oauth2
```
<VirtualHost *:80>
    ServerName pingfederate.local
    Redirect /authorize https://localhost:9031/as/authorization.oauth2
</VirtualHost>
```
### proxy configuration, not verified
```
<VirtualHost *:80>
    ServerName pingfederate.local
    RewriteEngine On
    ProxyPass /authorize            http://localhost:9031/as/authorization.oauth2
    ProxyPassReverse /authorize     http://localhost:9031/as/authorization.oauth2
    ProxyPreserveHost On
</VirtualHost>
```
