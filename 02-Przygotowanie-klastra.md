Na początek zmień nazwy przydzielonych hostów wskazując ich rolę w klastrze. Pozwoli Ci to uniknąć błędów w kolejnych zadaniach:
```
sudo hostnamectl set-hostname manager01
sudo hostnamectl set-hostname worker01
sudo hostnamectl set-hostname worker01
```

Należy wykonać dla trzech węzłów klastra (manager01, worker01, worker02):
```
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common net-tools
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get -y install docker-ce
sudo docker info
```
Na węźle manager01:
```
ifconfig
sudo docker swarm init --advertise-addr [IP]
sudo docker info
sudo docker node ls
```
Na węźle worker01 (Dodać TYLKO worker01 do klastra!):
```
sudo docker swarm join --token [token] [IP]:2377
sudo docker info
sudo docker node ls
```
Na weźle manager01:
```
sudo docker info
sudo docker node ls
sudo docker swarm join-token manager -q
sudo docker swarm join-token worker -q
sudo docker node inspect self
```
