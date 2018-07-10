Ingress przykład jedna instancja:
```
sudo docker network inspect ingress
sudo docker service create -d --name web2 --network backend --replicas 1 -p 8080:80 nginx
sudo docker service inspect web2 --pretty
```
Wejdz na stronę i zobacz jak działa serwis poprzez ingress routing:
```
http://manager01:8080
http://worker02:8080
```
Usuwamy:
```
sudo docker service rm web2
```
Ingres dowolne rozkładanie ruchu pomiędzy węzłami klastra:
```
sudo docker service create --mode=global --name=cadvisor \
  --mount type=bind,source=/,target=/rootfs,readonly=true \
  --mount type=bind,source=/var/run,target=/var/run,readonly=false \
  --mount type=bind,source=/sys,target=/sys,readonly=true \
  --mount type=bind,source=/var/lib/docker,target=/var/lib/docker,readonly=true \
  --publish=8080:8080 \
  google/cadvisor:latest
sudo docker service ls
```
Wejdz na stronę:
```
http://manager01:8080
http://worker01:8080
```
Zmiana z ingress na host:
```
sudo docker service update --publish-rm=8080 cadvisor
sudo docker service inspect cadvisor
sudo docker service update --publish-add mode=host,published=8080,target=8080 cadvisor
sudo docker service inspect cadvisor
```
Random port:
```
sudo docker service create --name random -p target=80 nginx
sudo docker service ps random
sudo docker service inspect random --pretty
sudo docker service create --name random2 -p target=80 nginx
sudo docker service inspect random2 --pretty
```
