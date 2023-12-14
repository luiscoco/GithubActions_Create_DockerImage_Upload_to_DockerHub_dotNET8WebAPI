# GitHub Actions: how to create .NET 8 Web API Docker image and Upload it to Docker Hub

## 0. Prerequisite

Create a new account in Docker Hub or if you already have an account Sign in

https://hub.docker.com/

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/db16e305-f8a4-469f-9537-2c141595322e)

Create a new repository in Docker Hub for storing your Docker image

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/a4365704-5c10-4dc4-b4cf-044815e2ff61)

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/dd261708-5b37-4b03-a32c-70d6dc7ddeb3)

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/bb10cd18-4dee-41d4-9fd2-be41baa17bb0)

See your new Docker Hub repo in the list 

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/148d70ba-cda5-4fbd-8cc9-90e2f5e13b43)

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

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/35662d72-fae8-484b-bfdb-bf37520b31c8)

## 2. Create a Github repository in Visual Studio 2022 Community Edition

We select the "Git Changes" tab and press the "Create Git Repository..." button 

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/fd0b9970-83b6-49b8-aca6-db76b285ec93)

We input the repository name

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/c1e91d1b-94d7-4de0-a76a-f2a1d47e312c)

## 3. Create the Github Action Workflow for creating the Docker image and Upload it to Docker Hub

## 3.1. Create the Docker Hub secrets in Github

We navigate to the "**settings**" option inside our Github repository

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/89779712-e7bd-4b8c-b02b-ae1cf654156e)

We now select the "**Secretas and variables**" menu option

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/def4b2de-b60f-4cc2-9390-3bf4e0fe9484)

Select the "**Actions**" option for creating a new repository secret

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/8b167fde-acd0-46d8-baa0-abf315c407ef)

Create two secrets, one of them for storing the Docker Hub user name, and the other one for storing the Docker Hub password.

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/3d093d3d-507e-4268-a6b7-d91363a3bfb5)


## 3.2. Create the Github Action Workflow

In our new Github repo we press in the "Actions" button for creating a new Github Action Workflow

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/b0b4d6e7-66ee-4a4a-9f9a-6e25d1f279a4)

The we selec the option "set up a workflow yourself"

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/9306faa1-bc90-44e8-9234-319f5ace9b0d)

We input the workflow yml file source code

```yml
name: Docker Image CI

on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Log in to Docker Hub
      uses: docker/login-action@v1
      with:
        registry: docker.io
        username: ${{ secrets.DOCKER_HUB_USERNAME }}
        password: ${{ secrets.DOCKER_HUB_PASSWORD }}

    - name: Build and push Docker image
      run: |
        IMAGE_ID=docker.io/luiscoco/webapidotnet8
        # Build the Docker image
        docker build . --file Dockerfile --tag $IMAGE_ID:latest
        # Push the image to Docker Hub
        docker push $IMAGE_ID:latest
```

This code represents a **GitHub Actions workflow** defined in a **YAML** format. 

It is used to automate the build and deployment of a **Docker image** to **Docker Hub** when changes are pushed to the "**master**" branch or when a pull request is opened against the "master" branch in a GitHub repository.

### Workflow Name and Trigger Events:

The **workflow** is named "**Docker Image CI**"

It is **triggered** by two **GitHub events**:

**push event** on the "**master**" branch: This means the workflow will run whenever changes are pushed to the "master" branch.

**pull_request** event on the "**master**" branch: This means the workflow will also run when a pull request is opened against the "master" branch.

```yaml
name: Docker Image CI
on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]
```

### Jobs:

The workflow defines a single job named "build" that will run on an "**ubuntu-latest**" runner (a **virtual machine** provided by GitHub Actions).

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

### Job Steps:

The job consists of several steps that will be **executed sequentially**.

The first step is to checkout the repository's source code using the **actions/checkout@v3** action.

```yaml
steps:
- uses: actions/checkout@v3
```

### Logging in to Docker Hub:

The second step is named "Log in to Docker Hub," and it uses the docker/login-action@v1 action.

It logs in to Docker Hub using the provided Docker Hub username and password stored in **GitHub secrets**: DOCKER_HUB_USERNAME and DOCKER_HUB_PASSWORD

Secrets are a way to securely store sensitive information.

```yaml
- name: Log in to Docker Hub
  uses: docker/login-action@v1
  with:
    registry: docker.io
    username: ${{ secrets.DOCKER_HUB_USERNAME }}
    password: ${{ secrets.DOCKER_HUB_PASSWORD }}
```

### Building and Pushing Docker Image:

The third step is named "Build and push Docker image."

It runs a series of Docker commands in a shell script:

**VERY IMPORTANT**! It sets the IMAGE_ID variable with the **Docker Hub repository name (docker.io/luiscoco/webapidotnet8)**.

It builds a Docker image using a Dockerfile from the repository, tags it as "latest," and assigns it the image ID.

It then pushes the Docker image to Docker Hub using the same image ID.

```yaml
- name: Build and push Docker image
  run: |
    IMAGE_ID=docker.io/luiscoco/webapidotnet8
    # Build the Docker image
    docker build . --file Dockerfile --tag $IMAGE_ID:latest
    # Push the image to Docker Hub
    docker push $IMAGE_ID:latest
```

In summary, this GitHub Actions workflow is designed to automate the building and pushing of a Docker image to Docker Hub when changes are made to the "master" branch of the associated GitHub repository or when pull requests are opened against the "master" branch.

It ensures that the Docker image is kept up to date and is available for deployment.

## 3.3. Verify the docker image was uploaded to Docker Hub

If we press on the Actions button we can verify the workflow builds were successfully

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/2cd1a47b-5b88-4feb-971a-e49d07e16246)

Finally, we can log in to Docker Hub and navigate to our repository and check the image was uploaded a few minutes ago

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/ee2e7e57-cfd6-47fa-bc73-f1f6cbb6fb2b)

We also can enter in the repo to see the docke image details

![image](https://github.com/luiscoco/GithubActions_Create_DockerImage_Upload_to_DockerHub_dotNET8WebAPI/assets/32194879/e997baac-231c-4b9d-b78a-c8de4237df1d)






