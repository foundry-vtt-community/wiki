Unpack the zip file in a suitable location, and then open the unpacked folder. Open a terminal window in this location and run the command:
`node resources/app/main.js`

You should now see a message saying VTT is running. 

Closing the terminal will stop the application.

For a server that runs without the need for a terminal or that restarts automatically at boot up, you should leverage a tool such as [`systemd`](https://www.freedesktop.org/wiki/Software/systemd/) or [`upstart`](http://upstart.ubuntu.com/).


## Docker setup

A simple docker container has been built by a community member, and allows for easy setup in a docker environment. Information for that container can be found on DockerHub here: [https://hub.docker.com/r/spoctoss/foundryvtt](https://hub.docker.com/r/spoctoss/foundryvtt)

This has been confirmed to work behind a Docker reverse proxy. SSL front-to-back tunneling needs to be setup for Audio/Video relay to work correctly. 

### Docker Compose

Here is an example docker compose including a reverse proxy and letsencrypt certificate manager.
```version: '3.5'
services:
  foundryvtt:
    image: spoctoss/foundryvtt
    restart: unless-stopped
    volumes:
        - /data/foundryvtt:/home/foundry/fvtt
        - /data/config:/home/foundry/data
        # The next line is used to load the certificates into the container for A/V relay
        - /proxy/certificates/myserver.com:/home/foundry/fvtt/sslcerts:ro 
    hostname: myserver.com
    domainname: myserver.com
    environment: 
        VIRTUAL_HOST: myserver.com
        VIRTUAL_PROTO: HTTPS
        LETSENCRYPT_HOST: myserver.com
        LETSENCRYPT_MAIL: myemail@myserver.com
  proxy:
    image: jwilder/nginx-proxy
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - /proxy/certificates/myserver.com:/etc/nginx/certs:rw
      - /proxy/vhost.d:/etc/nginx/vhost.d 
      - /proxy/html:/usr/share/nginx/html
      - /etc/localtime:/etc/localtime:ro

  letsencrypt:
    image: jrcs/letsencrypt-nginx-proxy-companion
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - /proxy/certificates:/etc/nginx/certs:rw
      - /proxy/vhost.d:/etc/nginx/vhost.d 
      - /proxy/html:/usr/share/nginx/html
      - /etc/localtime:/etc/localtime:ro```