Czyścimy:
```
sudo docker service rm $(sudo docker service ls -q)
```
Gramy w ping-pong:
```
sudo docker service create -d --name ping --network backend --replicas 3 alpine sleep 1d
sudo docker service create -d --name pong --network backend --replicas 3 alpine sleep 1d
sudo docker service ls
sudo docker container ls
sudo docker container exec -it [ID] sh
  ping pong
```
