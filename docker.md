## Some common Docker commands

##### Show available images
```
sudo docker images
```

##### Show running containers, or all containers
```
sudo docker ps
sudo docker ps -a
```

##### To stop / start a container
```
sudo docker stop <name | id>
sudo docker start <name | id>
```

##### To see info about a container, or specific info
```
sudo docker inspect <name | id>
sudo docker inspect -f '{{ .NetworkSettings.IPAddress }}' <name | id>
```

##### To delete a container
```
sudo docker rm <name | id>
```

##### To delete all containers
```
sudo docker rm -f $(sudo docker ps -a -q)
```

##### To delete an image
```
sudo docker rmi <name | id>
```
