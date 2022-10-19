## demo app - developing with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

#### To start the application

Step 1: Create docker network

    docker network create mongo-network 

Step 2: start mongodb 

docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --network mongo-network mongo  

Step 3: start mongo-express
    
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb--net mongo-network --name mongo-express   mongo-express

NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_

Step 4: open mongo-express from browser

http://localhost:8081

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express

Step 6: Start your nodejs application locally - go to `app` directory of project 

cd app
npm install 
node server.js
    
Step 7: Access you nodejs application UI from browser

http://localhost:3000

#### start the application with Docker Compose

Step 1: start mongodb and mongo-express, my-app

docker-compose up
    
Note: You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       

Step 4: access the nodejs application from browser 

http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:[tag] .       
    
The dot "." at the end of the command denotes location of the Dockerfile.
