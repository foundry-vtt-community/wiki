Unpack the zip file in a suitable location, and then open the unpacked folder. Open a terminal window in this location and run the command:
`node resources/app/main.js`

You should now see a message saying VTT is running. 

Closing the terminal will stop the application.

For a server that runs without the need for a terminal or that restarts automatically at boot up, you should leverage a tool such as [`systemd`](https://www.freedesktop.org/wiki/Software/systemd/) or [`upstart`](http://upstart.ubuntu.com/).

## Example systemd unit
```
[Unit]
Description=Foundry VTT
After=network.target

[Service]
User=%i
ExecStart=node /path/to/foundryvtt/resources/app/main.js
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

### Running

`sudo systemctl start foundryvtt@username.service`

`sudo systemctl enable foundryvtt@username.service`

## Example nginx config with certbot
```
    server {
        listen 443 ssl;
        listen [::]:443 ssl;
        server_name foundry.example.com;

        location / {
            proxy_pass http://localhost:30000;
            proxy_intercept_errors on;
            proxy_set_header Host            $host;
            proxy_set_header X-Real-IP       $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;

            # required for websockets to work
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }
    }
```

After running certbot, certbot will modify your nginx config file to add ssl certs and optionally an http->https redirect
