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

Steps for mysql database update using docker volume:  
1. Pull mysql:5 container and instantiate it using persistent volume.
Command: docker run -d --name mysql-db-v1 -e MYSQL_ROOT_PASSWORD=password -v mysqldata:/var/lib/mysql mysql:5
2. Add mock data in the database in mysql:5 container  
Command: 
  2.1 Login to container: docker exec -it mysql-db-v1 mysql -u root -p
  2.2 Create database: create database app; use app;
  2.3 Create table users in database app:
    CREATE TABLE users (UserID int, Name varchar(255), City varchar(255));
  2.4 Populate data in table users: 
    INSERT INTO users (UserID, Name, City) VALUES (1, 'Divya', 'Pune');
    INSERT INTO users (UserID, Name, City) VALUES (2, 'Eshita', 'Delhi');
    INSERT INTO users (UserID, Name, City) VALUES (3, 'Bhargavi', 'Mumbai');
    INSERT INTO users (UserID, Name, City) VALUES (1, 'Swaroopa', 'Chennai');
  2.5 Check Data:
    select * from users;
    exit
3. Pull mysql:8 container and add the same mock data to it. 
    docker run -d --name mysql-db-v2 -e MYSQL_ROOT_PASSWORD=password -v mysqldata:/var/lib/mysql mysql:8
    Login to container: docker exec -it mysql-db-v2 mysql -u root -p
    mysql>use app;
    mysql>select * from users;
    
5. Kill the mysql:5 container. 

