# IRIS-Docker-micro-Durability
allow small durability for demo and developent

During development of a container based demo I found the need to access a fresh docker   
instance of IRIS image (e.g intersystems/iris-community:2020.2.0.199.0) over and over.   
To bypass setting passwords and loading my code repeatedly I developed this workaround.

It is a reduced variant of  "Docker - light weight durability"   
https://community.intersystems.com/post/docker-light-weight-durability

I want   
- passwords without need to change  
- my classes, routines, globals  without repeated reload  

The base facts:  
- docker offers external volumes  (eg. needed for the license) 
- iris-main allows to run scripts before IRIS starts  

OK so far! 
I have a directory for external data in docker.  
It contains  
- an IRIS.DAT  (with my code and my globals)  
- an adapted iris.cpf  
- - refers to my IRIS.DAT as Database, mount required at startup  
- - replaces the DB for namespace USER to the new DB  
- - maps routine ^%ZSTART also to the new DB  
- - - ^%ZSTART cleans the property for PasswordChange for some accounts  
- a script to copy iris.cpf into my container  

Once the script is executed  
- IRIS starts  
- ^%ZSTART is executed  
and I'm ready to work.  

Important:  
The external directory should allow *rwx* access (chmod 777) as the docker image  
is just a nobody to your local system. But it wants to write his iris.lck file  

Shutdown requires no action as your DB is already outside the docker image located   
and next time you have a virgin IRIS __system__ again with your USER DB unchanged.  

You may say: It's dirty.  
But I can confirm my development speed and fun was significantly increasing.   
And a got rid of the boring acts with virgin container images. 

How to use:  
Have a docker instance for IRIS >>>  iris-community:2020.2.0.199.0      
Download and untar the archiv __micro-durability.tar.gz__    
chmod 777 to direcory demo/  
run your container:  

docker run --name iris1 --init -it \  
-p 52773:52773 -p 51773:51773 \  
-v __$(pwd):/external__ \  
--rm \   
__intersystems/iris-community:2020.2.0.199.0__ \   
-b __/external/pre.copy__  


_Late warning. always check the version of your image!   
I just fell into  intersystems/iris-community:2020.2.0.__204__.0_

__NOTICE: ALL SCRIPTS ARE FOR LINUX ONLY !__
