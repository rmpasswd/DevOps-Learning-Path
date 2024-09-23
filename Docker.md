## Why use a container engine( Docker, [Podman](https://docs.podman.io/en/latest/index.html) ) **instead of** traditional Virtual Machine( via VMWare, Virtualbox) ?
**=>**
Goal: Seperate the different concerns of a project (front-end, backend, database).
![image](https://github.com/user-attachments/assets/27d67b70-8ccb-48b4-8767-bd5536cf4a05)
In traditional approach each app needs a seperate guest-os, meaning more overhead, resource-lock etc. (todo) <br>
But in Containers approach, a 'container engine' seperates the concerns such as 'each app and its package' can be seperated and still can have what it needs(abstractions, api calls)



`docker run nginx`

=> this will _start_ an nginx server(default port 80). But in browser _localhost:80_ will not work. We need to forward ports from inside Docker instance _to_ our host machine.

`docker run -p 5000:80 nginx`  
connect host's local port 5000 to the exposed internal port 80

`docker run -it -p 1880:1880 -v node_red_docker_data:/data --name noderedd nodered/node-red`  
- Here the image is _nodered/node-red_ (downloaded from docker hub)
- the container is given a name _noderedd_.
- The data is mounted to a volume named _node-red_docker_data_. The named volume is found here: **\\wsl$\docker-desktop\mnt\docker-desktop-disk\data\docker\volumes** !
![image](https://github.com/user-attachments/assets/7007e1ff-2d05-4313-9bac-5ce1c73f4751)


`docker ps`  
this is a 'task manager' for docker. Shows running instances.

`docker ps -a`  
Shows history of previously run container apps...

```mermaid
flowchart TD
    A(Docker file) --> B(Docker Image);
    B -->C(Docker Container 1);
    B -->D(Docker Container 2);
    B -->E(Docker Container 3);

```
