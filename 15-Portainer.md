Czyszczenie:
```
sudo docker service rm $(sudo docker service ls -q)
```
Uruchomienie serwisu Portainer w wersji stand alone:
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
Czyszczenie:
```
sudo docker service rm $(sudo docker service ls -q)
```
Uruchomienie serwisu portainer na klastrze Swarm w konfiguracji z agentami:
```
curl -L https://downloads.portainer.io/portainer-agent-stack.yml -o portainer-agent-stack.yml
sudo docker stack deploy -c portainer-agent-stack.yml portainer
```
Aby się do niego dostać wejdz na:
```
http://manager01:9000
```
