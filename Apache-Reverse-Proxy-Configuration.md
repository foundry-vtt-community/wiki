These example configurations are for setting up Apache2 as a reverse proxy for Foundry, and apply to Foundry versions 0.5.6 or later. Compatibility with 0.5.5 and below is not guaranteed, although the RewriteRule method is reported to work.

The important change for Foundry 0.5.6+ is the correct forwarding of the websocket requests. If it is not done properly, expect to see the "Join Game Session" button greyed out and stuck as "Loading...", with a 400 error shown in the browser console. 

Note that most `ProxyPass` type directives are not allowed in `.htaccess` files, so the configuration must be done in the appropriate `.conf` files.

### Foundry Configuration

First, although not Apache specific, ensure your Foundry configuration is set to work from behind a reverse proxy to match your Apache configuration. For example, set the options in `foundrydata/Config/options.json` file like:
```
"hostname": "vtt.example.com",
"port": 30000,
"routePrefix": null,
"sslCert": null,
"sslKey": null,
"proxySSL": true,
"proxyPort": 443,
```

**`NOTE`**: "sslKey" and "sslCert" are the same as for Apache2 configuration if you're using Foundry on the same server. Make sure Foundry (application) **has read access** to the keys. E.g. Certbot generates ssl-keys with `root:root` permissions and you will see `The proxy server could not handle the request` error if not change permissions.

### RewriteRule Method

This method requires mod_rewrite (reference [here](https://www.happyassassin.net/posts/2018/11/23/reverse-proxying-websockets-with-apache-a-generic-approach-that-works-even-with-firefox/)) as well as mod_proxy, mod_proxy_http, and maybe mod_proxy_wstunnel modules enabled.

Note that while this method is versatile and should "just work" without modification for most installations, performance may not be as good as a specific websocket ProxyPass, as described in the ProxyPass and wstunnel Method section below.

Replace `vtt.example.com` with your domain name where appropriate, and `localhost:30000` to match your Foundry server and port. If you happen to be running Foundry in SSL mode, also change occurrences of `http://` to `https://` and `ws://` to `wss://`.

```
# Apache .conf for reverse proxy of Foundry VTT.
# Uses LetsEncrypt/certbot to manage SSL certificates, which needs to be
# configured separately (https://certbot.eff.org/instructions)
# Note, requires mod_proxy mod_proxy_http mod_proxy_wstunnel as well as usual
# modules for SSL etc.

<VirtualHost *:443>
    ServerAdmin webmaster@example.com
    ServerName vtt.example.com
    ErrorLog "/var/log/httpd/vtt.example.com.error_log"
    CustomLog "/var/log/httpd/vtt.example.com.access_log" common
    LogLevel error
    # Uncomment this SSLProxyEngine line if Foundry running in SSL mode
    #SSLProxyEngine on
    SSLCertificateKeyFile "/etc/letsencrypt/live/vtt.example.com/privkey.pem"
    SSLCertificateFile "/etc/letsencrypt/live/vtt.example.com/fullchain.pem"
    Include /etc/letsencrypt/options-ssl-apache.conf
    ProxyPreserveHost On
    # Change localhost:30000 if your Foundry instance is running on a
    # different server or port.
    # Additionally, if you are running Foundry with SSL enabled, change
    # any ws:// to wss:// and any http:// to https://
    # If you have Foundry configured to use a routeprefix, then no modifications
    # should be needed to anything here, it should just work.
    ProxyPass / http://localhost:30000/
    ProxyPassReverse / http://localhost:30000/
    # The following rewrite will modify websocket requests to pass them properly
    RewriteEngine on
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule .* "ws://localhost:30000%{REQUEST_URI}" [P]
</VirtualHost>

<VirtualHost *:80>
    ServerName vtt.example.com
    Redirect permanent / https://vtt.example.com/
</VirtualHost>
```
### ProxyPass and wstunnel Method

This method uses mod_proxy_wstunnel and a specific `ProxyPass` line for the Foundry websocket traffic. It should provide better performance than using the RewriteRule method, as per the performance warning on the [Apache RewriteRule Flags page](https://httpd.apache.org/docs/2.4/rewrite/flags.html) for use of the `[P]` (proxy) flag:

> Using this flag triggers the use of mod_proxy, without handling of persistent connections. This means the performance of your proxy will be better if you set it up with ProxyPass or ProxyPassMatch. This is because this flag triggers the use of the default worker, which does not handle connection pooling/reuse. Avoid using this flag and prefer those directives, whenever you can.

Note, however, that in this method the `ProxyPass  "/socket.io/" "ws://localhost:30000/socket.io/"` line may require modification to match your server and/or Foundry routeprefix etc, unlike the RewriteRule method.

The `ProxyPass  "/socket.io/" "ws://localhost:30000/socket.io/"` line must come before the `ProxyPass / http://localhost:30000/`, as the more specific rules must be specified first.

Replace `vtt.example.com` with your domain name where appropriate, and `localhost:30000` to match your Foundry server and port. If you happen to be running Foundry in SSL mode, also change occurrences of `http://` to `https://` and `ws://` to `wss://`.

```
# Apache .conf for reverse proxy of Foundry VTT.
# Uses LetsEncrypt/certbot to manage SSL certificates, which needs to be
# configured separately (https://certbot.eff.org/instructions)
# Note, requires mod_proxy mod_proxy_http mod_proxy_wstunnel as well as usual
# modules for SSL etc.

<VirtualHost *:443>
    ServerAdmin webmaster@vtt.example.com
    ServerName vtt.example.com
    ErrorLog "/var/log/httpd/vtt.example.com.error_log"
    CustomLog "/var/log/httpd/vtt.example.com.access_log" common
    LogLevel error
    # Uncomment SSLProxyEngine line if Foundry running in SSL mode
    # SSLProxyEngine on
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
