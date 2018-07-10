Czyszczenie:
```
sudo docker service rm $(sudo docker service ls -q)
```
Uruchamianie Ranchera:
```
sudo docker run -d --restart=unless-stopped -p 8080:8080 rancher/server
```
Wejdz na:
```
http://manager01:8080
```
