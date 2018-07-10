Czyszczenie:
```
sudo docker service rm $(sudo docker service ls -q)
```
Uruchomienie serwisu Portainer:
```
sudo docker service create \
    --name portainer \
    --publish 8080:9000 \
    --constraint 'node.role == manager' \
    --mount type=bind,src=//var/run/docker.sock,dst=/var/run/docker.sock \
    portainer/portainer \
    -H unix:///var/run/docker.sock
```
Aby się do niego dostać wejdz na:
```
http://manager01:8080
```
Uruhamiamy viz aby zobaczyć jak Portainer przedstawia nam infrastrukturę:
```
sudo docker service create \
  --name=viz \
  --publish=8090:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
```
