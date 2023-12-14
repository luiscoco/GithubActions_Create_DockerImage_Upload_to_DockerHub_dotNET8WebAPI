# GitHub Actions: how to create .NET 8 Web API Docker image and Upload it to Docker Hub


## 1. Create a new .NET 8 Web API with Visual Studio 2022 Community Edition

We run Visual Studio 2022

We press the option "Create a new project"

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/40ef38e9-24a0-45ea-8e74-404e31364a9c)

We selec the Web API project template

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/9f4b233d-b329-44dd-a21e-467a0bb1d620)

We set the solution name and location

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/6aedee5e-9acc-41c0-bddf-e012262d74df)

We select the new solution main features: .NET 8 framework, **Docker enable (for creating automatically the Dockerfile)**, etc

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/5b7b66d5-241d-4440-8512-98468fc34eaf)

This is the Solution folders structure:

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/145c2f43-9665-43cb-a64d-fa071e8a9373)

Now if We didn't start yet the Docker Desktop a warning message will appear requesting us to run it.



## 2. Create a Github repository in Visual Studio 2022 Community Edition




## 3. Create the Github Action Workflow for creating the Docker image and Upload it to Docker Hub


## 3.1. Create the Docker Hub secrets in Github





## 3.2. Create the Github Action Workflow





## 3.3. Verify the docker image was uploaded to Docker Hub




