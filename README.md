# what is this project?

this is my personal docker playground.

# installing docker desktop

you can install docker desktop to visualize your images and your running containers https://www.docker.com/products/docker-desktop/


# docker commands cheatsheet

- build an image from a Dockerfile: docker build -t <image-name>
- create a container and run a docker image with hot reload implemented: docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules <image-name>
- list all docker images: docker images
