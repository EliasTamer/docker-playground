# what is this project?

this is my personal docker playground.

# installing docker desktop

you can install docker desktop to visualize your images and your running containers https://www.docker.com/products/docker-desktop/


# docker commands cheatsheet

- build an image from a Dockerfile: <strong>docker build -t {image-name-here} </strong>
- create a container and run a docker image with hot reload implemented: <strong>docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules {image-name-here} </strong>
- list all docker images: <strong>docker images </strong>
