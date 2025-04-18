                            YOLO APP 

 # Overview

 This project uses Docker Compose to containerize and orchestrate a full-stack YOLO application, including the frontend, backend, and MongoDB database.

 Running the command:

 docker compose up

 from the root directory will build and launch all required containers.

 Architecture

 The docker-compose.yml file defines:

 >Three Services:
 1 yolo-app-frontend - React frontend
 2 yolo-app-backend -Node.js backend
 3 mongo - MongoDB database

> Named Volume:app-mongo-data -Ensure MongoDB data persists.

>Custom networ : yolo-net -bridge network that allow the containers to communicate with each other


Frontend: yolo-app-front-end 

This  container that spins up the front end where users will interact with the site. This container is built from a multi stage docker file to keep the final image lightweight. It is exposed on port 3000

Dockerfile Directives 

FROM : Specifies the base image used (Uses node:14-slim for building and alpine for serving)
WORKDIR: set the working directory inside the container
COPY: Copy files form the host to the container
RUN: Execute commands like "npm install"
EXPOSE: Show the port that the container listens on, in this case port 3000
CMD: Defines the command to run when the container starts ["npm", "start"]


Backend: yolo-app-backend

This is the container that handles the backend logic  i.e connection to the database and is running on port 5000. Similary to the yolo-app-frontend, this container utilizes a multi stage docker file for an optimized final image.

Dockerfile Directives 

FROM: Sets the base images (node:14-slim for build and Alpine for runtime)
WORKDIR : Define the working directory inside the container (/app in this case)
COPY : Copies from the host to the container - first package*.json , then the rest of the code
RUN : Installs dependencies
EXPOSE : Document the port the app will listen on in this case port 5000
CMD : ["npm start"]

Database: Mongo

This service uses the official MongoDB image from Docker Hub. It persists data via the mounted volume app-mongo-data and listens on the default port 27017.

Networking & Volumes

Network : yolo-net -bridge network for internal container communication
Volume: app-mongo-data -ensure mongoDB data is not lost when containers are rebuilt.

