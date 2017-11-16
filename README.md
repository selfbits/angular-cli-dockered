Minimal node:8-alpine based image with npm, git, bash, openssl, @angular/cli, ionic and cordova.

Segmentation error with ionic serve and sass is fixed with the help of 
https://github.com/jubel-han/dockerfiles/blob/master/node/Dockerfile

------------------------------
Docker installation:
- Windows: Install docker-toolbox from
https://www.docker.com/products/docker-toolbox
- Mac: Install docker from 
https://www.docker.com/docker-mac

------------------------------
Usage to create an angular-cli project in a folder at /PATH/TO/YOUR/HOSTDIRECTORY
```
docker run --rm --name ngx-development -p 4200:4200 -v /PATH/TO/YOUR/HOSTDIRECTORY:/opt/workdir -dit selfbits/angular-cli /bin/bash
docker exec -it ngx-development /bin/bash
cd /opt/workdir
ng new myproject
cd myproject
ng serve --host=0.0.0.0

### Pull and run the angular-cli image in a container named "ngx-development". Param explanation:
### --rm Deletes the container after it is exited
### -p X:Y Forwards the host port X to the docker container port Y. You can use -p 4201:4200 to see your live project at localhost:4201 even if you start the ng serve in the docker container at port 4200.
### Default development port for angular-cli projects is 4200. Default port for ionic is 8100.
### -dit d starts the container in detached mode which prevents that it exits automatically. it is used to execute a command ( "/bin/bash") interactively
### -v Share a volume between host and docker container. For windows you can use "-v /c/Users/myuser/Desktop/myproject:/opt/workdir". This will mount the folder myprojet of the host in the docker container at /opt/workdir
```
------------------------------
Usage to create an ionic-cli project in a folder at /PATH/TO/YOUR/HOSTDIRECTORY
```
### Pull and run the selfbits/angular-cli image in a container named "ionic-development" with standard port and live reload ports
docker run --rm --name ionic-development -p 8100:8100 -p 35729:35729 -p 53703:53703 -v /PATH/TO/YOUR/HOSTDIRECTORY:/opt/workdir -dit selfbits/angular-cli /bin/bash
docker exec -it ionic-development /bin/bash
cd /opt/workdir
ionic start
# Follow cli commands
cd $PROJECTNAME
ionic serve
```
Open browser on host machine and go to localhost:8100 
