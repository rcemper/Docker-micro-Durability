# IRIS-Docker-micro-Durability
Allow limited durability for demo and development
  IRIS-Docker-micro-Durability
During development of a container based demo I found the need to access a fresh docker   
instance of IRIS image (e.g intersystems/iris-community:2020.2.0.199.0) over and over.   
To bypass loading my code repeatedly I developed this workaround.

It is a reduced variant of [Docker - light weight durability](https://community.intersystems.com/post/docker-light-weight-durability)

## Docker support  
The principle of a persitent IRIS database outside the container is unchanged.    
But now the whole setup is moved into Dockerfile and docker-compose.yml
### Prerequisites  
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.   
### Installation   
Clone/git pull the repo into any local directory  
```
  git clone https://github.com/rcemper/SSH-for-IRIS-container.git   
```
Open the terminal in this directory build and run the container:   
```
$ docker-compose up -d   
```
### How to use it
Your container has now an external IRIS.DAT in \</installdir\>/demo/   
It is setup as working DB for Globals and Routines in namespace USER  
*REMEBER: this is just for the content of this namespace*  

[Article to previous version in DC](https://community.intersystems.com/post/iris-docker-micro-durability)
