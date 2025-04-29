 ### Mongo run command 
    docker run -d -p 27017:27017 mongo

### building the project
    docker build -t <image_name> 

 ### creating custom_network to talk contaibers each other 
    docker network create <network_name>

###  checks the network is created 
    docker network ls 
### run the mongodb in created network 
    docker run -d -v volume_database:/data/db --name <name (important this should given to url of mongodb)> --network my_custom_network -p 27017:27017 <image name >


### run the backend 
    docker run -d -p 3000:3000 --name <backen name > --network <network name > <backend image name >
 
### to check the logs 
     docker ps
     copy the container id of backend image name 
     docker logs <container id>

### kill the container
    docker kill <container id>

### Theory 
    I ran both the backend project and the database in separate Docker containers. By default, two separate containers cannot communicate with each other. To solve this issue, I created a custom Docker network and connected both containers to it. This allows the containers to communicate with each other seamlessly.

    I also used a Docker volume for the database to ensure data persistence. Without using a volume, the data stored in the database would be lost once the container is stopped or removed.

    Here’s the command I used to create and attach the volume:
    docker volume create volume_database
    docker run -v volume_database:/data/db -p 27017:27017 mongo

     
## some extra commands we constantly used 
   ### building image 
    docker build -t image_name .
    docker images
   ### passing env variables 
    docker run -p 3000:3000 -e DATABASE_URL="database url" image_name
   ### building custom image 
    docker build -t <image_name> .
   ### run that cutsom image
    docker run -p 3000:3000 <image_name>


