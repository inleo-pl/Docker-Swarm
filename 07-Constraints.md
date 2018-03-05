Serwis na nie istniejącym węźle klastra:
```
sudo docker service create --name on-worker02 -p 8237:80 --constraint node.hostname==worker02 nginx
sudo docker service ls
sudo docker service ps on-worker02
sudo docker inspect [ID]
```
