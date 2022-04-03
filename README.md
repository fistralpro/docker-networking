# Docker Networking Primer
docker-compose and network connectivity between services defined in different docker-compose.yml files.  

The following will automatically talk to each other as they are in the same folder  
```
docker-compose -f docker-compose.1.yml -f docker-compose.2.yml up -d
```
As we can see in this example:
```
docker exec -it service_1 ping service_2
```

But in different folders they will not (they generate based on their current folder)    

The trick here is to define a separate network and have the docker containers communicate with this.  
```
docker network create external-example  

docker-compose -f ./compose1/docker-compose.yml -f ./compose2/docker-compose.yml up -d

docker exec -it separate1 ping separate2

docker network ls
```

cleanup
```
docker stop separate1 separate2 service_1 service_2
docker rm separate1 separate2 service_1 service_2
docker network rm external-example
```