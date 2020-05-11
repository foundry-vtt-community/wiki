This configuration is intended for use with Foundry 0.5.6 or later.  Compatibility with 0.5.5 and below is not guaranteed.

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
    # Change localhost:30000 if your Foundry instance is running on a
    # different server or port.
    # Additionally, if you are running Foundry with SSL enabled, change
    # any ws:// to wss:// and the http:// to https://
    # If you have Foundry configured to use a routeprefix, include it in this
    # next websocket ProxyPass line, for example, for a "vtt" routeprefix:
    # ProxyPass "/vtt/socket.io/" "ws://localhost:30000/vtt/socket.io/"
    ProxyPass  "/socket.io/" "ws://localhost:30000/socket.io/"
    # But don't include your routeprefix in these next two lines
    ProxyPass / http://localhost:30000/
    ProxyPassReverse / http://localhost:30000/
</VirtualHost>

# Forward normal http requests to https
<VirtualHost *:80>
    ServerName vtt.example.com
    Redirect permanent / https://vtt.example.com/
</VirtualHost>
```

Additionally, though not Apache specific, ensure your Foundry configuration is set to work from behind a reverse proxy to match your Apache configuration. For example, for the above, set the options in `foundrydata/Config/options.json` file like:
```
  "port": 30000,
  "routePrefix": null,
  "sslCert": null,
  "sslKey": null,
  "proxySSL": true,
  "proxyPort": 443,
```

