## Docker installation - Ubuntu Xenial 16.04 (LTS)
source : https://docs.docker.com/engine/installation/linux/ubuntulinux/

- Setup access to Docker repository:
```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

- Open the /etc/apt/sources.list.d/docker.list
- Remove any existing entries and add this:
```
deb https://apt.dockerproject.org/repo ubuntu-xenial main
```

- Prerequisites:
```
sudo apt-get update
sudo apt-get purge lxc-docker
apt-cache policy docker-engine
sudo apt-get install linux-image-extra-$(uname -r)
```

- Installation:
```
sudo apt-get update
sudo apt-get install docker-engine
```

- Setup service to start on boot:
```
sudo systemctl enable docker
```

- Start service:
```
sudo service docker start
```

- Create a Docker group and add yourself into:
You must restart after.
```
sudo groupadd docker
sudo usermod -aG docker ubuntu
```

- Test:
```
docker info
docker run hello-world
```

---
## Install Docker-compose
```
sudo -i
curl -L https://github.com/docker/compose/releases/download/1.7.0/docker-compose-`uname -s`-`uname -m` >  /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
exit
```

---

## Uninstallation
- To uninstall the Docker package:
```
sudo apt-get purge docker-engine
```

- To uninstall the Docker package and dependencies that are no longer needed:
```
sudo apt-get autoremove --purge docker-engine
```

The above commands will not remove images, containers, volumes, or user created 
configuration files on your host.
- Run the following command:
```
rm -rf /var/lib/docker
```
You must delete the user created configuration files manually.

- To uninstall Docker Compose:
```
rm /usr/local/bin/docker-compose
```
