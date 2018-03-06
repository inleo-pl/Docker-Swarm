Co się dzieje gdy dołączamy nowy węzeł? Na początek tworzymy dwa serwisy viz i cadvisor:
```
sudo docker service create \
  --name=viz \
  --publish=8090:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
  
sudo docker service create --mode=global --name=cadvisor \
  --mount type=bind,source=/,target=/rootfs,readonly=true \
  --mount type=bind,source=/var/run,target=/var/run,readonly=false \
  --mount type=bind,source=/sys,target=/sys,readonly=true \
  --mount type=bind,source=/var/lib/docker,target=/var/lib/docker,readonly=true \
  --publish=8080:8080 \
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
