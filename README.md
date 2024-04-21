# DockerMathApp
## Getting started with Docker
Make sure you have Docker (https://www.docker.com/products/docker-desktop/) and .NET 8.0 SDK on your PC

You will need to clone the MathhApp repo for this tutorial (https://github.com/PROG7311-VCDN-2024/MathApp)

Make sure that the MathApp is working on your PC (variables, connection strings, etc)

## Guide for Adding Project to a Docker Container
### STEP 1 
Open the project folder 

Run the following command 
```
dotnet run
```
Go to http://localhost:(Your Port) in a browser to test the app

Use Ctrl+C in the command prompt to stop the app
### STEP 2
Right click on your project > Add > Docker Support

if you are using your VM, you will select Linux as your target OS

Once Complete you will notice a Dockerfile has been created - this file contains 4 distinct name build stages
### STEP 3 
Add container orchestrator support 

Right click on your project > Add > Conatiner Orchestrator Support - this is your docker-compose files.

The docker-compose.yml file references the name of the image that's created when you run the project

* You can read more about this here:
  
https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker?view=aspnetcore-8.0
### STEP 4  
Select docker-compose from the debug drop down menu 

The start Debugging the app

* If you run the following command in PMC you can see a list of images created
```
docker images 
```
* If you run the following command in PMC you can see a which containers are currently running
```
docker ps
```
### STEP 5
Once you have completed developing and debugging your app, change the drop-down from Debug to Release and build your app

An image is now created with the latest tag, this can be pushed to the private registry or Docker Hub

run the docker images command again to take note of the changes 

DEBUG: 
![image](https://github.com/PROG7311-VCDN-2024/DockerMathApp/assets/102237289/ad294aa5-333a-4177-ac37-b1241a0579f6)

RELEASE:
![image](https://github.com/PROG7311-VCDN-2024/DockerMathApp/assets/102237289/3f215481-e144-4103-a129-d19678d580e4)

## Adding SQL DB to Docker
### STEP 1 
Change your connection string from "Server = localhost.." to "Server = sql_server..."
### STEP 2
Run the following line to see the image
```
docker image ls
```
### STEP 3
Inside your docker-compose.yml file add the following lines of code 
```
sql:
    image: "mcr.microsoft.com/mssql/server:2022-latest"
    container_name: sql_server
    ports: 
      - "1433:1433" 
    environment:
      - ACCEPT_EULA=y
      - SA_PASSWORD= P@SSW0RD1
```
### STEP 4
Run the following command 
```
docker-compose up
```


