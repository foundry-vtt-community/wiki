You can use Docker to run FoundryVTT.

### For this you only need 3 files.
<!--ts-->
      * Dockerfile
      * docker-compose.yml
      * foundryvtt-x.x.x.zip (Give by Patreon)

**Dockerfile** describe installation of your container

```yaml
FROM ubuntu:latest

# make directory
RUN mkdir -p /home/foundry/fvtt
RUN mkdir -p /root/.local/share/FoundryVTT

# Build-arg: User ID for the created foundry user
ENV UID=1026
# Build-arg: Group ID for the created group
ENV GUID=65534
# Set the foundry install home
ENV FOUNDRY_HOME=/home/foundry/fvtt

RUN echo "UID ${UID}"
# add a foundry group with a guid listed above

RUN echo "UID: ${UID} GUID: $GUID"
# create the foundry use
RUN adduser -u $UID -h "$FOUNDRY_HOME" -D foundry

# Set the current working directory
WORKDIR "${FOUNDRY_HOME}"

# installing unzip and bash shell
RUN apt-get update

# curl nodejs nginx unzip
RUN apt-get install apt-utils -y
RUN apt-get install curl -y
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get -y install nodejs
RUN apt-get -y install nginx unzip

# nginx pararm 
RUN rm /etc/nginx/sites-enabled/default
RUN service nginx restart

# copy found
COPY ./foundryvtt*.zip .

# unzip 
RUN unzip foundryvtt*.zip
RUN rm foundryvtt*.zip

EXPOSE 30000
CMD [ "node", "resources/app/main.js" ]
```

###  **docker-compose.yml** describe creation image
```yaml
version: '3.3'

services:
   fvtt:
        build:
            context: ./
            dockerfile: ./Dockerfile
            args:
                UID: 1026
                GUID: 65534
        image: fvtt:1.11.0            
        container_name: FoudryVTT
        ports:
            - "30000:30000"
        restart: always

```

#### **foundryvtt-x.x.x.zip** FoundryVTT (Give by Patreon)
copy your foundryvtt-x.x.x.zip file to the same level as the other files


## *Build image*
`sudo docker-compose build`

After build image you can use or test your container with this commands :

Run the container (for test no save modifications)
#### `sudo docker run --restart=always --name FoundryVTT.x.x.x -p 30000:30000 -d fvtt:1.11.0`


#### Run the docker with volume map for save yours modifications : ####
```sudo docker run --restart=always --name FoundryVTT.x.x.x -p 30000:30000 \
 -v /YourLocalDirectory1:/home/foundry/fvtt \
 -v /yourLocalDirectory2:/root/.local/share/FoundryVTT \
-d fvtt:1.11.0```

