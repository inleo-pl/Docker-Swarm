Powołanie serwisu:
```
sudo docker service create --replicas 1 --name helloworld alpine ping docker.com
sudo docker service ls
sudo docker service inspect --pretty helloworld
sudo docker service ps helloworld
sudo docker ps
```
Skalowanie:
```
sudo docker service scale helloworld=5
sudo docker service ps helloworld
sudo docker ps
```
Usuwanie:
```
sudo docker service rm helloworld
sudo docker service inspect helloworld
sudo docker ps
```
