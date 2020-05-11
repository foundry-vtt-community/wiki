Example configuration for setting up Apache2 as a reverse proxy for Foundry.  The list of modules required are in the comments at the start.  Credit to @Failbot42 on Discord for this.

Replace vtt.example.com with your domain name where appropriate.

```# Apache .conf for reverse proxy of Foundry VTT.
# Uses LetsEncypt/certbot to manage SSL certificates, which needs to be
# configured separately (https://certbot.eff.org/instructions)
# Note, requires mod_proxy mod_proxy_http mod_proxy_wstunnel as well as usual
# modules for SSL etc.

<VirtualHost *:443>
    ServerAdmin webmaster@vtt.example.com
    ServerName vtt.example.com
    ErrorLog "/var/log/httpd/vtt.example.com.error_log"
    CustomLog "/var/log/httpd/vtt.example.com.access_log" common
    LogLevel error
    SSLProxyEngine on
    SSLCertificateKeyFile "/etc/letsencrypt/live/vtt.example.com/privkey.pem"
    SSLCertificateFile "/etc/letsencrypt/live/vtt.example.com/fullchain.pem"
    Include /etc/letsencrypt/options-ssl-apache.conf
    ProxyPreserveHost On
    ProxyPass  "/socket.io/" "ws://localhost:30000/socket.io/"
    ProxyPass / https://localhost:30000/
    ProxyPassReverse / https://localhost:30000/
</VirtualHost>


# Forward normal http requests to https
<VirtualHost *:80>
    ServerName vtt.example.com
    Redirect permanent / https://vtt.example.com/
</VirtualHost>```