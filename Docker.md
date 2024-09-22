## Why use a container engine( Docker, [Podman](https://docs.podman.io/en/latest/index.html) ) **instead of** traditional Virtual Machine( via VMWare, Virtualbox) ?
**=>**
Goal: Seperate the different concerns of a project (front-end, backend, database).
![image](https://github.com/user-attachments/assets/27d67b70-8ccb-48b4-8767-bd5536cf4a05)
In traditional approach each app needs a seperate guest-os, meaning more overhead, resource-lock etc. (todo)
But in Containers approach, a 'container engine' seperates the concerns such as 'each app and its package' can be seperated and still can have what it needs(abstractions, api calls)



 
