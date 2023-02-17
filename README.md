<div align="center">
<img loading="lazy" style="width:700px" src="./docs/banner.png">
<h1 align="center">ReactJS Hamravesh Docker Template</h1>
<h3 align="center">Sample Project to use hamravesh service provider for reactjs app</h3>
</div>
<p align="center">
<a href="https://nodejs.org/en/" target="_blank"> <img src="https://seeklogo.com/images/N/nodejs-logo-FBE122E377-seeklogo.com.png" alt="nodejs" width="40" height="40"/> </a>
<a href="https://reactjs.org/" target="_blank"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/2300px-React-icon.svg.png" alt="react" width="40" height="35"/> </a>
<a href="https://www.docker.com/" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker" width="40" height="40"/> </a>
<a href="https://www.nginx.com" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" alt="nginx" width="40" height="40"/> </a>
<a href="https://git-scm.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a>
<a href="https://hamravesh.com/" target="_blank"> <img src="https://avatars.githubusercontent.com/u/24360374?s=200&v=4" alt="git" width="40" height="40"/> </a>
</p>

# Guideline
- [Guideline](#guideline)
- [Goal](#goal)
- [Development usage](#development-usage)
  - [Clone the repo](#clone-the-repo)
  - [Build everything](#build-everything)
  - [Note](#note)
  - [Check it out in a browser](#check-it-out-in-a-browser)
- [Testing Usage](#testing-usage)
- [local deployment test](#local-deployment-test)
- [Hamravesh deployment](#hamravesh-deployment)
  - [0- Create an account](#0--create-an-account)
  - [1- Create a repo app](#1--create-a-repo-app)
  - [3- Setup django app](#3--setup-django-app)
    - [1- General info](#1--general-info)
    - [2- Environment Variables](#2--environment-variables)
    - [3- Domain Address](#3--domain-address)
    - [4- Pick a plan](#4--pick-a-plan)
    - [5- wait until its deployed](#5--wait-until-its-deployed)
- [CICD Deployment](#cicd-deployment)
  - [Github CICD](#github-cicd)
  - [Gitlab/Hamgit CICD](#gitlabhamgit-cicd)
- [Bugs](#bugs)


# Goal
the only purpose of this sample is to help you getting started setting up a project for react with docker and docker-compose plus adding the functionality to deploy on hamravesh.

# Development usage
You'll need to have [Docker installed](https://docs.docker.com/get-docker/).
It's available on Windows, macOS and most distros of Linux. 

If you're using Windows, it will be expected that you're following along inside
of [WSL or WSL
2](https://nickjanetakis.com/blog/a-linux-dev-environment-on-windows-with-wsl-2-docker-desktop-and-more).

That's because we're going to be running shell commands. You can always modify
these commands for PowerShell if you want.


## Clone the repo
Clone this repo anywhere you want and move into the directory:
```bash
git clone https://github.com/AliBigdeli/ReactJS-Hamravesh-Docker-Template.git
```


## Build everything

*The first time you run this it's going to take 5-10 minutes depending on your
internet connection speed and computer's hardware specs. That's because it's
going to download a few Docker images and build the Python + requirements dependencies.*

```bash
docker compose up --build
```

Now that everything is built and running we can treat it like any other Django
app.

## Note

If you receive an error about a port being in use? Chances are it's because
something on your machine is already running on port 3000. then you have to change the docker-compose.yml file according to your needs.
## Check it out in a browser

Visit <http://localhost:3000> in your favorite browser.

# Testing Usage
in order to run your tests you can just the following command

```bash
docker-compose exec app sh -c "npm test"
```
# local deployment test
this is just for testing your production base in your local first.
first of all you need to build the image of the project which you can do it by running the following command:
```bash
docker build -t front -f ./dockerfiles/prod/Dockerfile .
```
then for running the built image you can use the following command:
```bash
docker run -p 80:80 front
```
now if you open your browser and head to <http://localhost> you should be able to see the page.

# Hamravesh deployment


## 0- Create an account
in order to deploy your project inside hamravesh first you need to create an account. so please go to the following url and create your account.

<https://console.hamravesh.com/signup>

after that you need to sign in to your console panel. which is going to be like this.
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-console.png"></div>

## 1- Create a repo app
in order to deploy your project you can use repo mode (or منبع گیت) after clicking on the item. you will see a panel like this below:

<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-repo-step1.png"></div>

as you can see you have to provide your github/gitlab/hamgit repo address for deployment. 
in our case the configuration will be as follow:

``` properties
repo_address: https://github.com/AliBigdeli/ReactJS-Hamravesh-Docker-Template.git
# if you are just testing without cicd use main or if you want to use cicd script to delpoy create a prod branch and then add it here
branch_name: main
build_context: .
docker_file_address: ./dockerfiles/prod/Dockerfile
```
Note: as we are going to implement ci/cd and other stuffs we avoid auto deployment or even uploading file.

after your done with the inputs just click on (تنظیمات اپ) and go for next step.


## 3- Setup django app
follow the provided steps to finish this section.

### 1- General info
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-repo-step2-1.png"></div>

in this page you have to provide general information's about the app you are about to create, which in my case are as follows:

```properties
app_name: front-test # name of the app which is going to be called inside the portal
service_port: 80 # which is based on nginx port
```
Note: provided information is just enough to run our program for more details please visit this url 
<https://docs.hamravesh.com/darkube/create/git-repo/settings/general/>

### 2- Environment Variables
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-repo-step2-2.png"></div>

in this section you have to provide the environment variables which are going to be used in the project. you can switch to editor and paste your environments.

Note: provided information is just enough to run our program for more details please visit this url <https://docs.hamravesh.com/darkube/create/git-repo/settings/envs/>

### 3- Domain Address
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-repo-step2-3.png"></div>

pick a name for you app which is going to be accessed through the web and for better security please enable https redirect.
keep in mind that you can give a different dns name through a provider like arvan or cloudflare.(we will provide more details for this matter later)

Note: provided information is just enough to run our program for more details please visit this url <https://docs.hamravesh.com/darkube/create/git-repo/settings/domain-address/>


### 4- Pick a plan 
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-repo-step2-4.png"></div>

for launching purposes you have to pick a plan for resources. based on the scale and traffic of your project you have to pick one.

Note: at the moment we are not using disks and we are just using the static files being served by the Whitenoise.

### 5- wait until its deployed
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-repo-step2-5.png"></div>

now all you have to do is to wait util the project is fully deployed.

after its done you can access the website through the url you picked in stage 3 of the setup.


# CICD Deployment
For the sake of continuous integration and deployment i have provided two samples for github and gitlab/hamgit for you.
but there will be some configurations to be added for building and deploying purposes.

## Github CICD
will be provided soon

## Gitlab/Hamgit CICD
in order to do ci/cd in the sample project for gitlab/hamgit you have to create a duplicate of the ```.gitlab-ci.yml.sample``` but with different name as ```.gitlab-ci.yml``` in the root directory.

after that our pipeline will be always listening to the prod branch. if you commit in this branch it will go through the process.


note that you have to declare 5 or more environment variables in your gitlab/hamgit project repo, which you can add it by going to ```Settings>CI/CD>Variables```, and in this section try to add all the needed variables.

<div align="center" ><img loading="lazy" style="width:700px" src="./docs/gitlab-envs.png"></div>

these variables should be included:
- DARKUBE_APP_ID - ``` which can be found in app info page ```
- DARKUBE_DEPLOY_TOKEN - ``` which can be found in app info page ```
- IMAGE -  ``` registry.hamdocker.ir/<USERNAME>/<APPNAME> ```
- REGISTERY - ``` registry.hamdocker.ir/<USERNAME> ```
- REGISTERY_PASSWORD - ``` registry password ```
- REGISTERY_USER - ``` username like 'bigdeliali3' ```


for having ```DARKUBE_APP_ID``` and ```DARKUB_DEPLOY_TOKEN``` head to the app page and use the following parameters in the picture.

<div align="center" ><img loading="lazy" style="width:700px" src="./docs/hamravesh-app-info.png"></div>
 
for having ```REGISTRY``` and ```REGISTRY_USER``` and ```REGISTRY_PASSWORD``` head to the app page and use the following parameters in the picture.
REGISTRY will be the url like this: ```registry.hamdocker.ir/<USERNAME>```
and for getting the username and passwords just go to the app section and click on docker image. you will see something like this, after that click on registries.
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/docker-app.png"></div>

On top of the page you can find the credentials for registry that you need.
<div align="center" ><img loading="lazy" style="width:700px" src="./docs/docker-registry.png"></div>
after that if everything goes well you can see that the jobs are working.



# Bugs
Feel free to let me know if something needs to be fixed. or even any features seems to be needed in this repo.



