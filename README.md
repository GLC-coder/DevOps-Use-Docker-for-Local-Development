## Use Docker for local development

This app shows a simple user profile app set up using

- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

### Technologies used:

Docker, Node.js MongoDB, MongoExpress,HTML, CSS, JavaScript

### Project Description:

1- Create Dockerfile for Nodejs application and build Docker image.

2- Run Nodejs application in Docker container and connect to MongoDB database container locally.

3- Run MongoExpress container as a UI of the MongoDB database.

### With Docker

#### To start the application

Step 1: Pull mongo and mongo-express images with latest version from public repository Docker hub

    docker pull mongo
    docker pull mongo-express

Step 2: Create an isolated docker network

    docker network create mongo-network

Step 3: Create and start mongodb container from mongo image and add it to created isolated docker network

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=username -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --network mongo-network mongo

Step 4: Create and start mongo-express container from mongo-express image and add it to created isolated docker network

    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=username -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --network mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express

Step 5: open mongo-express from browser

    http://localhost:8081

Step 6: create `user-account` _db_ and `users` _collection_ in mongo-express UI from the browser.

Step 7: Go to `app` directory of project

    cd app

Step 8: Add a " .env" file into the app directory of project and fill the environment variable
![Alt text](app/images/envfile.png?raw=true)

Assign "user-account" to DATABASE in .env file
Assign "users" to COLLECTION in .env file

Step 9: Start your nodejs application locally inside the app directory.

    npm install
    node server.js

Step 10: Access you nodejs application UI from browser

    http://localhost:3000

Step 11:To build a docker image from the application

    docker build -t users-app:1.0 .

Step 12: To re-tag the created image

    docker tag users-app:1.0 jason8746/users-app:1.0

Step 13: Push an image to public repository Docker hub

    docker push jason8746/users-app:1.0

![Alt text](app/images/users-app-image_docker.png?raw=true)

Step 14: Pull the created users-app image from Docker hub

    docker pull jason8746/users-app:1.0
