Ingress przykład jedna instancja:
```
sudo docker network inspect ingress
sudo docker service create -d --name web --network overnet --replicas 1 -p 8080:80
sudo docker service inspect web --pretty
```
Wejdz na stronę i zobacz jak działa serwis poprzez ingress routing:
```
http://manager01:8080
http://worker02:8080
```
Usuwamy:
```
sudo docker service rm web
```
Ingres dowolne rozkładanie ruchu pomiędzy węzłami klastra:
```
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
sudo docker service ls
```
Wejdz na stronę:
```
http://worker01:8080
```
Zmiana z ingress na host:
```
sudo docker servcie update --publish-rm 8080 cadvisor
sudo docker service inspect cadvisor
sudo docker servcie update --publish-add mode=host,published=8080,target=8080 cadvisor
sudo docker service inspect cadvisor
```
Randrom port:
```
sudo docker service create --name random -p target=80 nginx
sudo docker service ps random
sudo docker service inspect random --pretty
sudo docker service create --name random2 -p target=80 nginx
sudo docker service inspect random2 --pretty
```
