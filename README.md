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


# creating CI/CD pipelines using github actions

the pipeline will be triggered upon pushing my code to dev branch, you can configure this the way that you want.

for this to work, you need to have the below:
- Azure account
- Azure subscription
- Azure container registry service and an app service within the same resource group.

the below CI/CI pipeline will execute the below commands:
- login to your azure account
- login to your azure container registry 
- re-build and push your docker image to your azure container registry
- deploy your updated docker image to your azure app service


<strong>this needs to reside inside on the root of your project inside like this: .github/workflows/file-name.yml </strong>

```
name: Docker CI/CD to Azure

on:
  push:
    branches:
      - dev
    paths:
      - 'backend/**'

env:
  ACR_REGISTRY: ACR-LOGIN-SERVER-HERE
  IMAGE_NAME: my-backend-image
  APP_SERVICE_NAME: APP-SERVICE-NAME-HERE
  RESOURCE_GROUP: RESROUCE-GROUP-NAME-HERE

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Login to Azure
      uses: azure/login@v1
      with:
        creds: '{"clientId":"${{ secrets.AZURE_CLIENT_ID }}","clientSecret":"${{ secrets.AZURE_CLIENT_SECRET }}","subscriptionId":"${{ secrets.AZURE_SUBSCRIPTION_ID }}","tenantId":"${{ secrets.AZURE_TENANT_ID }}"}'

    - name: Login to ACR
      uses: azure/docker-login@v1
      with:
        login-server: ${{ env.ACR_REGISTRY }}
        username: ${{ secrets.ACR_USERNAME }}
        password: ${{ secrets.ACR_PASSWORD }}

    - name: Build and push Docker image
      working-directory: ./backend
      run: |
        docker build -t ${{ env.ACR_REGISTRY }}/${{ env.IMAGE_NAME }}:latest .
        docker push ${{ env.ACR_REGISTRY }}/${{ env.IMAGE_NAME }}:latest

    - name: Deploy to Azure App Service
      uses: azure/webapps-deploy@v2
      with:
        app-name: ${{ env.APP_SERVICE_NAME }}
        images: ${{ env.ACR_REGISTRY }}/${{ env.IMAGE_NAME }}:latest
```


<strong>secret variables need to be stored inside your github repository secrets (Settings -> Secrets and Variables -> Actions) <strong>