Foundry VTT is a nice piece of software, but today I want to provide ways to have consistently running instance
that is reachable by a (sub)domain name instead of a clunky port number: "http://foundry.myhost.com" is in my opinion a bit nicer than "http://myhost.com:8080". We are leveraging the power of a node process manager to keep the instance running and to provide detailed statistics about the foundry instance, including easy to use start/stop/restart commands and an automatic start when the server boots up.

![Architecture](https://raw.githubusercontent.com/shwill/fvtt-tidbits/master/documentation/reverse-proxy/img/architecture.png)

You and your players will connect to the reverse proxy on an encrypted port, so nobody will connect directly to your Foundry installation. This has additionally a slight benefit to your security - yes, they are talking to the Foundry instance by using their client, but they can't breach the software by other means. So, win/win for everybody, even you!

Furthermore, we will setup an SSL encryption to foundry at no additional costs.

## Setting Up a Subdomain Name for Your Foundry Instance

Depending where you are buying your DNS this will be looking very different on your DNS management dashboard. In short, 
you will create a CNAME with a name of your choice and a value of '@', so pointing to the main IP address of your server.
The name of the CNAME will be your subdomain name, so "CNAME foundry @" will result in foundry.yourhost.com. Name it how
you like, but make sure to remember it.

![DNS Configuration dashboard at GoDaddy.com](https://raw.githubusercontent.com/shwill/fvtt-tidbits/master/documentation/reverse-proxy/img/subdomain-dns-manager.png)

In my example, my
* hostname is **yourhost.com**
* subdomain is **foundry**
* fully-qualified domain name (FQDN) is foundry.yourhost.com

## Setting up the Software Pre-Requisites

We will need several pieces of software to accomplish everything, but it's all very straight forward:

* a reverse proxy that allows a connection to your FQDN (foundry.yourhost.com) instead of the hostname with a specific port, e.g. yourhost.com:8080.
* the nodejs runtime to run Foundry itself and the corresponding package manager npm (node package manager) that will be used to install the process manager
* an utility that allows the creation of an SSL certificate (for free, yay!) using [let's encrypt](http://www.letsencrypt.com).

Let's start with 

### Installing node.js and it's Package Manager

This guide is for linux, sinde all cheaper hosts on the internet are running Linux, so there's that. I will be using Ubuntu, if you are using a different Linux distribution, your commands and packages might differ.

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`
`sudo apt-get install -y nodejs
```

This installs both nodejs and the node package manager npm. Check both with 
`node --version` and `npm --version`, at this time of writing node.js is at version 10.16.0 and npm at version 6.9.0.

### Install the Reverse Proxy and the Unzip Utility

We need both, so let's set those up:

```sudo apt-get install nginx unzip```

If port 80 is not protected by a firewall, you should be seeing the nginx starting page by opening a browser and surfing to http://yourhost.com. nginx comes up with a default web page located at `/var/www/html` which you can overwrite, alternatively you can remove this default website altogether by deleting the config file and restarting the nginx service:

```
sudo rm /etc/nginx/sites-enabled/default
sudo service nginx restart
```

Refreshing the browser window should now result in an error message.

### Install the Process Manager pm2

It could not be easier to install the process manager pm2: 

```sudo npm install pm2 -g```

This will install pm2 globally, so not just in the current directory for you to use. `pm2 --version` will show an output, for me it's version 3.5.1.

### Lets Grab Foundry and Unpack It

Go to your patreon page and grab the link for the Linux version of foundry, it should look like this: 

https://foundryvtt.s3-us-west-2.amazonaws.com/releases/[AccessKey]/FoundryVirtualTabletop-linux-x64.zip

Create a suitable directory to unpack it:

```
# switch to the home directory
mkdir ~/foundry
cd ~/foundry
```

will create a directory called foundry within your home directory. The command `pwd` (print working directory) will show you the full path to your current directory, for me it is `/home/ubuntu/foundry`. Take note of this directory.

Let's download the Foundry archive, unpack it and remove the installation archive afterwards:

```
wget https://foundryvtt.s3-us-west-2.amazonaws.com/releases/[AccessKey]/FoundryVirtualTabletop-linux-x64.zip
unzip FoundryVirtualTabletop-linux-x64.zip
rm FoundryVirtualTabletop-linux-x64.zip
```

Check if Foundry starts up without any errors by running it from the command line: `node /home/ubuntu/foundry/resources/app/main.js --port=8080`:

```
ubuntu@dev:~/foundry$ node /home/ubuntu/foundry/resources/app/main.js --port=8080
Foundry VTT | 2019-07-08 10:26:50 | [info] Foundry Virtual Tabletop - Version 0.3.2
Foundry VTT | 2019-07-08 10:26:50 | [info] Application Options:
{
  "port": 8080,
  "fullscreen": false,
  "isElectron": false,
  "isNode": true,
  "isSSL": false,
  "world": null,
  "background": false,
  "debug": false,
  "demo": false
}
Foundry VTT | 2019-07-08 10:26:51 | [info] Server started and listening on port 8080
```

Great! Let's kill the process with `CTRL-C`.

## Run Foundry Using the Process Manager pm2

First, we need to configure the process manager to startup automatically on server boot. There is [a startup script generator](http://pm2.keymetrics.io/docs/usage/startup/) at the pm2 homepage that will help you with that. For me on ubuntu, I do the following: `pm2 startup` generates the following output:

```
[PM2] Init System found: systemd
[PM2] To setup the Startup Script, copy/paste the following command:
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
```

So I am copying and running the command shown at the end of the output. 

```
[PM2] Writing init configuration in /etc/systemd/system/pm2-ubuntu.service
[PM2] Making script booting at startup...
[PM2] [-] Executing: systemctl enable pm2-ubuntu...
Created symlink /etc/systemd/system/multi-user.target.wants/pm2-ubuntu.service → /etc/systemd/system/pm2-ubuntu.service.
[PM2] [v] Command successfully executed.
+---------------------------------------+
[PM2] Freeze a process list on reboot via:
$ pm2 save

[PM2] Remove init script via:
$ pm2 unstartup systemd
```

It seems to be working. I can start processes with `pm2 start [options]` and freeze the currently running process list with `pm2 freeze`, so all of those processes will be started on server reboot, too. Neat.

Let's start Foundry using pm2: `pm2 start /home/ubuntu/foundry/resources/app/main.js --name "foundry" -- --port=8080`. Please note the two dashes `--` followed by a blank ` ` and the parameter for Foundry itself: `--port=8080`. If you adjust the port number, please take note of it, we will be needing it later on.

```
[PM2] Starting /home/ubuntu/foundry/resources/app/main.js in fork_mode (1 instance)
[PM2] Done.
┌──────────┬────┬─────────┬──────┬───────┬────────┬─────────┬────────┬─────┬───────────┬────────┬──────────┐
│ App name │ id │ version │ mode │ pid   │ status │ restart │ uptime │ cpu │ mem       │ user   │ watching │
├──────────┼────┼─────────┼──────┼───────┼────────┼─────────┼────────┼─────┼───────────┼────────┼──────────┤
│ foundry  │ 0  │ 0.3.2   │ fork │ 31130 │ online │ 0       │ 0s     │ 0%  │ 8.9 MB    │ ubuntu │ disabled │
└──────────┴────┴─────────┴──────┴───────┴────────┴─────────┴────────┴─────┴───────────┴────────┴──────────┘
 Use `pm2 show <id|name>` to get more details about an app
```

Using `pm2 list` you can bring this list up and see e.g. if the number of restarts is going up, indicating a problem probably with wrong startup parameters or something like that. You can see the CPU and memory footprint of the process and with `pm2 show foundry` you can bring up even more details. 

`pm2 start foundry`, `pm2 stop foundry`, `pm2 restart foundry` can control the running status of Foundry and `pm2 delete foundry` will remove this process from the pm2 config. Once everything is settled and running, you can `pm2 save` the current list of applications and to save it for a server reboot. Done!

If the port number is reachable from the internet, you can check the running Foundry instance by browsing to `http://yourhost.com:8080`. Foundry should be accessible then. If not, that's great, because we don't want the port open from the bad, bad internet, so close it after testing!

## Setting Up the Reverse Proxy

Instead, the user should connect to our reverse proxy, which then should talk to foundry, relaying the response back to the user. 

### Create a Log Directory

nginx likes log messages an so do you (even if you don't know it yet). Let's create a directory to store those messages in a structured manner: `sudo mkdir /var/log/nginx/foundry`.

The configuration files for nginx are stored at `/etc/nginx` and split up in `/etc/nginx/sites-available` for configuration thats are already setup, and `/etc/nginx/sites-enabled` with links to configurations that should be enabled. So let's create a reverse proxy configuration for our Foundry instance running on `127.0.0.1:8080`. The `127.0.0.1` is an IP alias (to simplyfy it) for your own host, so whenever you see that or `localhost`, it means: *"This is running locally, on my host, don't search the internet for it, it's right here."*

We need to allow larger upload sizes (scene backgrounds are sometimes rather large). 10 MB should be quite okay, but feel free to adjust this value.

Edit the nginx configuration and append the following line into the section ```http { ... }``` right before the closing bracket, this is rather important:

```sudo nano /etc/nginx/nginx.conf```

```
http {
	# Other settings, puth this right at the end of the http-section (this is important!)
        client_max_body_size 10m;
}
```

Afterwards, we can create a new configuration for our reverse proxy for Foundry: `sudo nano /etc/nginx/sites-available/foundry`.

Copy the following contents and paste it into the nano editor, then adjust every occurance of the port number :8080 and your FQDN to your configuration, then save the file.

```
server {
    listen 80;

    # Adjust this to your the FQDN you chose!
    server_name                 foundry.myhost.com;

    access_log                  /var/log/nginx/foundry/access.log;
    error_log                   /var/log/nginx/foundry/error.log;

    location / {
        proxy_set_header        Host $host;
        proxy_set_header        X-Real-IP $remote_addr;
        proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header        X-Forwarded-Proto $scheme;

        # Adjust the port number you chose!
        proxy_pass              http://127.0.0.1:8080;

        proxy_http_version      1.1;
        proxy_set_header        Upgrade $http_upgrade;
        proxy_set_header        Connection "Upgrade";
        proxy_read_timeout      90;

        # Again, adjust both your FQDN and your port number here!
        proxy_redirect          http://127.0.0.1:8080 http://foundry.myhost.com;
    }
}

```

Let's create a link from this configuration to enable it: `sudo ln -s /etc/nginx/sites-available/foundry /etc/nginx/sites-enabled/foundry`. Restart the server to reflect the changes: `sudo service nginx restart`. Check the browser, not pointing at port 80 (we are not yet installing the certificate) to see if the reverse proxy is working correctly: `http://foundry.myhost.com` should now be showing the foundry instance served by the process manager pm2. Looks great already!

### Optional Step: Use SSL Encryption 

The [Let's encrypt!-Homepage](https://letsencrypt.org/) has information about installing the Certbot on different systems, the one for [Ubuntu Linux and nginx](https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx) should be the right one. Let's just follow the instructions on their website (from 07/08/2019):

```
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install certbot python-certbot-nginx
```

installs the software itself and `sudo certbot --nginx` runs the installer for nginx.

Insert an e-mail address that will be contacted regarding critical information, agree to the terms of service after reading them thouroughly, choose if you want to share your e-mail address with the EFF and then choose your FQDN you want to secure (foundry.myhost.com) and enable automatic redirection of someone insists of using non-encrypted connections.

Everything else, including the automatic renewal after three months is now setup and you are done with a sparkling new installation of Foundry using a subdomain of your choice and an encrypted connection of you and your players to the gaming instance. Have fun!

```
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator nginx, Installer nginx
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel): info@myhost.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v02.api.letsencrypt.org/directory
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(A)gree/(C)ancel: A

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: n

Which names would you like to activate HTTPS for?

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: foundry.myhost.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel): 1
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for foundry.myhost.com
Waiting for verification...
Cleaning up challenges
Deploying Certificate to VirtualHost /etc/nginx/sites-enabled/foundry

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
Redirecting all traffic on port 80 to ssl in /etc/nginx/sites-enabled/foundry

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations! You have successfully enabled
https://foundry.myhost.com

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=foundry.myhost.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/foundry.myhost.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/foundry.myhost.com/privkey.pem
   Your cert will expire on 2019-10-06. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

#### Adding Auto-Refreshing of the SSL Certificate

First, create a new directory that is used by Certbot to auto-refresh your new certificate: `sudo mkdir /var/www/letsencrypt` and reference to this location for a very specific http answer that 
letsencrypt wants to verify. Open up your Nginx configuration for foundry and add some more configuration items: `sudo nano /etc/nginx/sites-available/foundry`.

Right above the section `location / { .... }` you prepend the following block:

```
include conf.d/drop;

location ^~ /.well-known/acme-challenge {
    allow all;
    root /var/www/letsencrypt;
    auth_basic off;
}
```

At the end, the whole configuration file should look like this:

```
server {
    # Adjust this to your the FQDN you chose!
    server_name                 foundry.myhost.com;

    access_log                  /var/log/nginx/foundry/access.log;
    error_log                   /var/log/nginx/foundry/error.log;

    include conf.d/drop;

    location ^~ /.well-known/acme-challenge {
        allow all;
        root /var/www/letsencrypt;
        auth_basic off;
    }

    location / {
        proxy_set_header        Host $host;
        proxy_set_header        X-Real-IP $remote_addr;
        proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header        X-Forwarded-Proto $scheme;

        # Adjust the port number you chose!
        proxy_pass              https://127.0.0.1:8080;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_read_timeout      90;

        # Again, adjust both your FQDN and your port number here!
        proxy_redirect          https://127.0.0.1:8080 http://foundry.myhost.com;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/foundry.myhost.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/foundry.myhost.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
    if ($host = foundry.myhost.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    listen 80;
    server_name                 foundry.myhost.com;
    return 404; # managed by Certbot
}
```

Now create a new file `sudo nano /etc/nginx/conf.d/drop`, add the following contents into it and restart nginx with `sudo service nginx restart`: 

```
# Most sites won't have configured favicon or robots.txt
# and since its always grabbed, turn it off in access log
# and turn off it's not-found error in the error log
location = /favicon.ico { access_log off; log_not_found off; }
location = /robots.txt { access_log off; log_not_found off; }
location = /apple-touch-icon.png { access_log off; log_not_found off; }
location = /apple-touch-icon-precomposed.png { access_log off; log_not_found off; }

# Rather than just denying .ht* in the config, why not deny
# access to all .invisible files
location ~ /\. { deny  all; access_log off; log_not_found off; }
```

### Additional Configuration for Nginx

Create a new file `sudo nano /etc/nginx/conf.d/drop.conf` and insert the following contents in there:

```
# Most sites won't have configured favicon or robots.txt
# and since its always grabbed, turn it off in access log
# and turn off it's not-found error in the error log
location = /favicon.ico { access_log off; log_not_found off; }
location = /robots.txt { access_log off; log_not_found off; }
location = /apple-touch-icon.png { access_log off; log_not_found off; }
location = /apple-touch-icon-precomposed.png { access_log off; log_not_found off; }

# Rather than just denying .ht* in the config, why not deny
# access to all .invisible files
location ~ /\. { deny  all; access_log off; log_not_found off; }
```

## Final Steps

Open up your web browser at http://foundry.myhost.com and it should automatically redirect to the encrypted site at https://foundry.myhost.com. Everything else should work as you are used to.

## Something Went Wrong

* Make sure that your port 443 is accessible. UFW (Universal FireWall) is pretty common, so you can check `ufw status` and see if that is enabled. `sudo ufw allow https` and `sudo ufw allow http` should add ports 80 and 443 to your firewall, thus allowing access to your ssl encrypted foundry instance and the Certbot for it's automatic certification renewal
* Check the `pm2 log foundry` for errors on the configuration there. Perhaps foundry starts up, fails and pm2 wants to restart it all the time, resulting in an endless loop of frustration for everybody? Stop the process by `pm2 stop foundry` and run it manually `node /home/ubuntu/foundry/resources/app/main.js` and check for errors (directory permissions are alright? Perhaps you changed anything there and it's just not working?).

## Contributors
@ShadowMorph from Discord provided additions to the nginx/SSl configuration which I partly added to the above config. Without your support, the auto-refreshing would not have worked and the SSL configuration would be quite a bit less robust. Thanks!