# docker-volume

Why Docker Volume?
-> When container is stopped, Data in the container is also lost. So for stateful app and persistent storage, we can use docker volume. 
-> One container cannot access data of other container. To be able to share data, we can use docker volumes. 

Docker Volume: 
-> Storage on Host machine
-> Data is on the host independent of container. So even if container crashes, our data will be saved. We can create a new container and use this docker volume. 
-> Docker volumes are created and managed by docker. We don't have to specify location of volume in host machine. Docker chooses a default location. 
/var/lib/docker

Docker volume commands:

docker volume create myvol
docker volume ls
docker volume rm myvol

To create as well as bind with container use flag -v command while creating container:
docker container run -d -v host_volume_name:container_location image_name

Anonymous Volume: If you don't provide any name. Docker usually created anonymous volume.
Named Volume: If we provide name to the volume. Easy to locate. 

Assignment: Database Upgrade

To Do: 
Upgrade a production mysql database from version mysql:5 to mysql:8 by persisting the data

Steps: 
1. 
