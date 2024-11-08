## Why use a container engine( Docker, [Podman](https://docs.podman.io/en/latest/index.html) ) **instead of** traditional Virtual Machine( via VMWare, Virtualbox) ?
**=>**
Goal: Seperate the different concerns of a project (front-end, backend, database).
![image](https://github.com/user-attachments/assets/27d67b70-8ccb-48b4-8767-bd5536cf4a05)
In traditional approach each app needs a seperate guest-os, meaning more overhead, resource-lock etc. (todo) <br>
But in Containers approach, a 'container engine' seperates the concerns such as 'each app and its package' can be seperated and still can have what it needs(abstractions, api calls)



`docker run nginx`

=> This will download(if not found in local cache) **nginx image** from docker hub, **create and run a new container** . This will _start_ an nginx server(default port 80). But in browser _localhost:80_ will not work. We need to expose our local machine's port that will point to Docker instance.

`docker ps`  
this is a 'task manager' for docker. Shows _running_ instances.

`docker ps -a`  
Shows history of all container apps...  
![image](https://github.com/user-attachments/assets/38e4af3b-4b6f-4acc-b7ec-1561be5864c2)

`docker logs NAME` or `docker logs -f NAME`  
=> This will output the logs of a running container named NAME. Use -f flag to stream the logs continuously.

`docker run -p 5000:80 nginx`  
Connect host computer's port 5000 to the exposed internal port 80 (from nginx' docs, we know its port is 80)

**Most Used**
`docker run -it nodered/node-red --name noderedd -p 1880:1880 -anotherHostPort:anotherInternalPort -v node_red_docker_data:/data  `  
- _--name noderedd_ : the container is given a name
- Here the image is _nodered/node-red_ (downloaded from docker hub)
- -v node_red_docker_data:/data => The _data_ folder inside the container is mounted to a folder named _node-red_docker_data_. The named volume is found here: **\\wsl$\docker-desktop\mnt\docker-desktop-disk\data\docker\volumes** !
![image](https://github.com/user-attachments/assets/7007e1ff-2d05-4313-9bac-5ce1c73f4751)
![image](https://github.com/user-attachments/assets/e782b65e-1ee6-4d73-af00-2bbdaff405d1)  

- **-it flag**
    >-i or --interactive:  
    When you type docker run -i this means that your terminal will transfer your input to container (app in container) until you press ctrl-D (leave container). For example, if some app works in container that waits for user input you can type something and that will be forwarded to the app.  
    -t or -tty (Pseudo-TTY):  
    If you add this flag, your container's output is attached to your terminal. Seems it mostly about formatting output (for bin/bash, for example - try ls with and without -t flag), but sometimes is more important because some apps change their behaviour depending on being launched via terminal or not (text editors, for example, or mechanism of masking password with * implemented by terminal).  

**Stop, Remove Image and Container**
**To remove a container, first we have to stop it:**
`docker kill NAME` or `docker stop NAME`  
=>Forcefully shuts down Immediately(SIGKILL signal) **or** stop gracefully(SIGTERM, 10sec later SIGKILL) the container with name NAME.
We have to run `docker ps` and know its NAME(far-right) column.  

`docker ps -a`                  
Lists containers (and tells you which images they are spun from)

`docker images`                 
Lists images 
`docker rm <container_id>`  
Removes a stopped container

`docker rm -f <container_id>`  
Forces the removal of a running container (uses SIGKILL)

`docker rmi <image_id>`  
Removes an image. Will fail if there is a running instance of that image i.e. container

`docker rmi -f <image_id>`  
Forces removal of image even if it is referenced in multiple repositories, i.e. same image id given multiple names/tags.  
Will still fail if there is a docker container referencing image




**Real Life Use Case**  
When developing a node.js application of which we expose a port when writing the express.js code, for example `app.listen(3000)`,  
we can deploy our existing code-base and run in docker, a **node** image is available in Docker Hub.

```mermaid
flowchart TD
    A(Docker file) --> B(Docker Image);
    B -->C(Docker Container 1);
    B -->D(Docker Container 2);
    B -->E(Docker Container 3);

```
