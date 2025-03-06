
# Docker Assignment 1

Containerize a web application using Docker, build a minimal-size Docker image, push it to Docker Hub with multiple tags, and deploy it using containers. Additionally, it verifies container networking by connecting to an nginx container from within the application container.

## Objective

The goal of this assignment is to containerize a simple web application using Docker. 
The steps include:

Creating a web application (or using an existing one) in a programming language of choice.

Writing a Dockerfile (preferably multistage) to containerize the application.

Building the Docker image with an optimized size.

Pushing the image to Docker Hub with at least three different tags.

Running the Docker container and accessing the application from a web browser.

Running another container using the latest nginx image.

Checking connectivity between the application container and the nginx container.

## Prerequisites

Ensure you have the following installed:

**Docker**

**Docker Compose**

**A web application** 

**Docker Hub account**

# Steps

## 1. Create or Use an Existing Web Application

Develop a simple web application using a programming language of your choice. Example: A Python Flask app.


## 2. Create a Dockerfile

### Dockerfile:

FROM node:18-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install 
COPY . .
RUN npm run build

FROM nginx:alpine  
COPY --from=build app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"] 


## 3. Build the Docker Image

Run the following command to build the image:

docker build -t your_dockerhub_username/webapp:latest .

## 4. Tag and Push the Image to Docker Hub

Tag the image with three different tags and push it to Docker Hub:

docker tag your_dockerhub_username/webapp:latest your_dockerhub_username/webapp:v1.0

docker tag your_dockerhub_username/webapp:latest your_dockerhub_username/webapp:stable

docker push your_dockerhub_username/webapp:latest

docker push your_dockerhub_username/webapp:v1.0

docker push your_dockerhub_username/webapp:stable

5. Run the Application Container

docker run -d --name webapp -p 5000:5000 your_dockerhub_username/webapp:latest

Access the application in a browser at: http://localhost:5000

6. Start an Nginx Container

docker run -d --name nginx-server nginx:latest

7. Check Connectivity Between Containers

Access the web application container’s terminal:

docker exec -it webapp sh

Ping the nginx-server container from inside the application container:

ping nginx-server

If the ping is successful, the containers are able to communicate.
