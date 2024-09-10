### Comand Docker ###

## install Docker ##
```bash
curl https://get.docker.com > /tmp/install.sh
cat /tmp/install.sh

chmod +x /tmp/install.sh
/tmp/install.sh

sudo apt-get update
sudo apt-get install \
 ca-certificates \
 curl \
 gnupg \
 lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker --version

sudo usermod -aG docker $USER 

sudo service docker start
sudo service docker stop
sudo service docker restart
sudo service docker status

```
```bash
docker build
docker run
docker commit
docker tag <image_ID> <my_tag>


docker build .                            # Build conteiner in work dir
docker image ls
docker ps -a
docker stop <mycontainer>
docker start <mycontainer>
docker rm <mycontainer>
docker log <mycontainer>
docker exec -it <mycontainer> /bin/bash

docker inspect mycontainer
docker rename mycontainer newname
docker cp mycontainer:/path/in/container /path/on/host

docker container prune                    # delete all stop conteiners
docker image prune                        # delete unused image
docker system prune                       # delete all unused data docker (conteiners, images, networks)

```
## Using Docker image ##

```bash
docker run debian echo "Hello World"

docker run -i -t debian /bin/bash


docker inspect <myconteiner>
docker inspect <myconteiner> | grep IPAddress
```
```bash
docker diff <myconteiner>
A (Added): File or directory was added.
C (Changed): File or directory has been changed.
D (Deleted): File or directory has been deleted.
```
```bash
docker log <myconteiner>
```
### delete conteiner ###
```bash
docker rm -v $(docker ps -aq -f status=exited)
docker container prune                    # delete all stop conteiners
docker image prune                        # delete unused image
docker system prune                       # delete all unused data docker (conteiners, images, networks)

```
### convertation Docker container in image ###
```bash
docker commit cowsay test/cowsayimage
```
### 
```bash
sudo service docker stop
systemctl stop docker
Metod 1
ps -ef | grep -E 'docker(d| -d| daemon)\b' | grep -v grep

sudo dockerd -H tcp://0.0.0.0:2375

docker -H tcp://<your host's ip>:2375 <subcommand>

Metod 2
docker run -d -i -p 1234:1234 --name daemon ubuntu:14.04 nc -l 1234

telnet localhost 1234
telnet> q

docker logs daemon

docker rm daemon
```
### docker run--restart
```bash
docker run--restart
no                     = Не перезапускать при выходе контейнера
always                 = Всегда перезапускать при выходе контейнера
unless-stopped         = Всегда перезагружать, но помнить о явной остановке
on-failure[:max-retry] = Перезапускать только в случае сбоя [количество перезапусков]
```
### Перемещение Docker в другой раздел
```bash
dockerd -g /home/dockeruser/mydocker
```