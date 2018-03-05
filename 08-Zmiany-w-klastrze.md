Co się dzieje gdy dołączamy nowy węzeł? Na początek czyścimy:
```
sudo docker service rm $(docker service ls -q)
```
Następnie tworzymy dwa serwisy viz i cadvisor:
```
sudo docker service create \
  --name=viz \
  --publish=8090:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
sudo docker service create --mode=global \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --volume=/dev/disk/:/dev/disk:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  google/cadvisor:latest
```
Testujemy:
```
http://manager01:8090
http://manager01:8080
```
Ddajemy węzeł do swarm. Na weźle manager01:
```
sudo docker info
sudo docker node ls
sudo docker swarm join-token worker -q
```
Na węźle worker02:
```
sudo docker swarm join --token [token] [IP]:2377
```
Co się stanie jak wyłączonymy worker02?
```
sudo halt
```
Czyszczenie niedziałających węzłów klastra:
```
sudo docker node ls
sudo docker node rm worker02
```
