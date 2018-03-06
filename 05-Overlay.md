Towrzymy sieć overlay:
```
sudo docker network create -d overlay --subnet=10.0.192.0/24 backend
sudo docker network ls
sudo docker network inspect backend
```
Dodajemy do niej kontener:
```
sudo docker service create -d --name web --network backend --replicas 2 alpine sleep 1d
sudo docker service ls
sudo docker network inspect backend
```
