# what is this project?

this is my personal docker playground.

# installing docker desktop

you can install docker desktop to visualize your images and your running containers https://www.docker.com/products/docker-desktop/


# docker commands cheatsheet

- build an image from a Dockerfile: <strong>docker build -t {image-name-here} </strong>
- create a container and run a docker image with hot reload implemented: <strong>docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules {image-name-here} </strong>
- list all docker images: <strong>docker images </strong>
- login to docker: <strong>docker login </strong>
- publishing a docker image: <strong>docker tag {react-app-folder-name} {username}/{image-name}</strong>
- pushing a docker image to your docker hub after publishing: <strong>docker push {username}/{image-name} </strong> 


# dynamic way of initializing docker for multiple services simultaneously

using <strong> docker compose up </strong>, we can intialize docker for multiple services (frontend, backend and database).

once the command is triggered, a <strong>compose.yml</strong> file will be created, afterwards you can configure things to your liking.

use the <strong> docker compose watch </strong> command to make sure that the code changes are being reflected directly when needed. (you need to configure this in the <strong>compose.yml</strong> before using the command).

for extra information related to the configuration, check the <strong>compose.yml</strong> under the mern-docker full stack app.

