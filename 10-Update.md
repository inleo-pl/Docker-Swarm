Update serwisu:
```
sudo docker service create \
  --replicas 3 \
  --name redis \
  --update-delay 10s \
redis:3.0.6
sudo docker service inspect --pretty redis
sudo docker service update --image redis:3.0.7 --update-delay=20s redis
sudo docker service ps
sudo docker service inspect --pretty redis
```
