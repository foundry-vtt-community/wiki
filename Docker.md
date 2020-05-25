You can use Docker to run Foundry VTT. You may use several different approaches.

## mikysan's Dockerfile (Recommended Approach)

Dockerfile and guides for manual and docker-compose setup available at [https://github.com/mikysan/simple-fvtt-dockerfile](https://github.com/mikysan/simple-fvtt-dockerfile).

## DirecktHit's Guide to Running FVTT-Docker with Traefik and Portainer (Recommended for Cloud Hosting)

Please visit [DirecktHit's blog](https://benprice.dev/posts/fvtt-docker-tutorial/) for the most up to date directions.

## DirecktHit's Docker Hub Image via `docker-compose`

Please visit the README in the [fvtt-docker repository](https://github.com/BenjaminPrice/fvtt-docker) for the most up to date directions.

## trotroyanas's docker-compose Setup

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


### *Build image*
`sudo docker-compose build`

After build image you can use or test your container with this commands :

Run the container (for test no save modifications)
#### `sudo docker run --restart=always --name FoundryVTT.x.x.x -p 30000:30000 -d fvtt:1.11.0`


#### Run the docker with volume map for save yours modifications : ####
```
sudo docker run --restart=always --name FoundryVTT.x.x.x -p 30000:30000 \
 -v /YourLocalDirectory1:/home/foundry/fvtt \
 -v /yourLocalDirectory2:/root/.local/share/FoundryVTT \
-d fvtt:1.11.0
```

## Jake
updated version of mikysan's dockerfile.  
Using the node version zip. Extract the contents into foundryvtt directory below. This dockerfile will copy your modules, worlds, assets, etc. into your docker image. 
I created a directory structure as:
* FoundryVtt
    * foundryvtt
    * foundrydata
        * Config
        * Data
        * Logs
    * Dockerfile

### Contents of Docker File
```
FROM node:12-alpine

ENV UID=1000
ENV GUID=1000

RUN deluser node
RUN adduser -u $UID -D foundry

USER foundry
RUN mkdir -p /home/foundry/data
RUN mkdir -p /home/foundry/app

WORKDIR /home/foundry/data
COPY --chown=$UID /foundrydata/ .

WORKDIR /home/foundry/app
COPY /foundryvtt/ .

EXPOSE 80:30000
CMD ["node", "/home/foundry/app/resources/app/main.js", "--headless", "--dataPath=/home/foundry/data" ]
```
### Docker commands
```
docker build . -t {something/something}
```

after the build is finished

```
docker run --rm -it  -p 80:30000/tcp {something/something}:latest
```

## thomasfa18's dockerhub image
 
This is a prebuilt node image that expects to have two paths (pkg & data) mounted to it:
/pkg - which is the contents of the node.js foundryvtt.zip from foundryvtt.com
/data - this is/will be your userdata folder. (If you are migrating from an existing install you can copy your existing data or target that folder)

The benefit of this image is that your app and data is decoupled from the node.js instance so you can place them on a shared folder if you like, and because ts a dockerhub image is can be easily pulled and run by many standalone home NAS devices (synology and qnap for instance).

Firstly configure you app and data directories (if you are using a NAS, create these folder on your NAS)
1. Create a new folder in the file system called `Docker`
2. Under this folder create a new folder called `foundry`
3. Under the foundry folder create a new folder called `pkg` and another folder called `data`
3. Copy the contents of the node.js foundryvtt.zip to the `pkg` folder
4. If you have existing userdata, copy this to the `data` folder

To download and run the container on a synology NAS
1. Install Docker from the package center
2. From docker goto registry and search for thomasfa18
3. Download the thomasfa18/node-foundry image
4. Go to Image, click on thomasfa18/node-foundry:latest, click launch
5. Click advance settings
6. On the first tab tick the checkbox for 'Enable auto-restart'
7. On the volume tab, add folders and mount paths that contain your data. eg. `docker/foundry/data` as mount path `/data` and `docker/foundry/pkg` as `/pkg`
8. On Port Setting tab set the local port to the port you want to use on your NAS to access the foundry website eg 30000, and the container port to the default 30000 (if you are migrating use the port that corresponds to your existing configuration)
9. Click next and then click apply
10. Click on the container menu and confirm the docker container is now running (if you right click and go to detail you can also review the log file for the container). You can now access the foundry server from any browser on you home network, and the internet if you configure your port forwarding.

It is a similar process to achieve the same using a computer, assuming you have already installed docker
1. `docker pull thomasfa18/node-foundry:latest`
2. `docker run -v [your windows path to foundry data]:/data -v [your windows path to the extracted node.js foundry package]:/pkg -it -p 30000:30000 thomasfa18/node-foundry:latest`
*Note:* using `-it` runs the container interactively, if you close the command window you will shut down the container. If you omit the `-it` form the command you will need to find the container name using `docker stats` or something to be able to shut it down via `docker kill [container name]`

## Felddy's Easy Docker Container

1. Clone the project to your machine:

    ```console
    git clone https://github.com/felddy/foundryvtt-docker.git
    cd foundryvtt-docker
    ```

1. Build the container using your FoundryVTT site credentials.  Your credentials
   are only used to download a Foundry release, and **are not stored** in the
   image:

    ```console
    docker-compose build \
    --build-arg USERNAME='your_username' \
    --build-arg PASSWORD='your_password'
    ```

1. Start the container and detach:

    ```console
    docker-compose up --detach
    ```

For more information about the available configuration options please see the [project README](https://github.com/felddy/foundryvtt-docker/blob/develop/README.md)