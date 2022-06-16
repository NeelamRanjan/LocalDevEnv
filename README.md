# How to run a aws Glue 3.0.0 container on local dev environment  
***
## Steps to create a new Dev Environment using Docker Desktop
### Install Docker Desktop  
* Docker Desktop Installer for Windows 
[Link] (https://docs.docker.com/desktop/windows/install/)
### Prerequisites - Gitbash, Visual Studio Code
* Install Git(Bash), Visual Studio Code and Visual Studio Code Remote Container Extension
[Link] (https://gitforwindows.org/)
[Link] (https://code.visualstudio.com/docs/?dv=win)
[Link] (https://aka.ms/vscode-remote/download/extension)
### Pull the aws glue 3.0.0 image form AWS github repository. 
* Open command prompt and type following command - 
 Docker pull amazon/aws-glue-libs:glue_libs_3.0.0_image_01  

 Check the Docker Desktop if the image is available there. 
### Run the container 
* Open Visual Studio code and open a folder where all other files are kept of the project
* Create a Docker Compose(with .yml extension) file as shown below -    
 ```
    version: '3.6'    
    services:    
      jupyter:    
        container_name: glue_jupyter    
        entrypoint: /home/glue_user/jupyter/jupyter_start.sh    
        environment: 
          - DISABLE_SSL=true
        image: amazon/aws-glue-libs:glue_libs_3.0.0_image_01
        ports:
          - '4040:4040'
          - '18080:18080'
          - '8998:8998'
          - '8888:8888'
        restart: always
        volumes:
          - C:/glue_jupyter_workspace:/home/glue_user/workspace/jupyter_workspace/
```
            
* Make sure you have created a folder in C drive named glue_jupyter_workspace before running this yml file. You can create folder anywhere then give the path in the Volumes section. 
* Now to run this container type the following command in Visual studio terminal - 
  docker compose up -d   
  
  check the Docker desktop to check if the container is running. 
### Open localhost:8888 on your browser where you can see the Jupyter notebook is running.  

 * Here you can run any Glue Job locally. 
