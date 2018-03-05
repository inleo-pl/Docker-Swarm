Wejdz na stronę:
```
https://github.com/dockersamples/docker-swarm-visualizer
```
Stwórz serwis:
```
sudo docker service create \
  --name=viz \
  --publish=8090:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
sudo docker service ls
sudo docker container ls
```
Wejdz na adres, aby sprawdzić czy działa:
```
http://manager01:8090
```
