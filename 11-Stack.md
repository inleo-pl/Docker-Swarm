Zrzucamy konfig konenera:
```
sudo docker service inspect viz > viz.inspect
```
Czyścimy:
```
sudo docker service rm $(sudo docker service ls -q)
```
Tworzymy plik yml:
```
vi viz.yml
```
Do pliku wpisz:
```
version: '3.1'

services:
  viz:
    image: dockersamples/visualizer
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints:
          - node.role==manager 
```
Uruchamiamy stack!
```
sudo docker stack deploy -c viz.yml viz
sudo docker service ls
sudo docker service ps viz_viz
sudo docker stack ls
sudo docker stack services viz
sudo docker stack ps viz
```
Aktualizujemy stack, ale na początku edytujemy plik yml:
```
vi viz.yml
```
Plik zmieniamy następująco:
```
version: '3.1'

services:
  viz:
    image: dockersamples/visualizer
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    ports:
      - "8090:8080"
    deploy:
      placement:
        constraints:
          - node.role==manager
```
Aktualziacja jest wykonywana poprzez redeployment:
```
sudo docker stack deploy -c viz.yml viz
sudo docker service ls
```
Usuwanie stack:
```
sudo docker stack rm viz
```
Dorzucanie replik:
```
vi viz.yml
```
Edycja pliku yml:
```
version: '3.1'

services:
  viz:
    image: dockersamples/visualizer
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    ports:
      - "8090:8080"
    deploy:
      replicas: 2
      placement:
        constraints:
          - node.role==manager      
sudo docker stack deploy -c viz.yml viz
```
Sprzątanie:
```
sudo docker service ls
sudo docker stack rm viz
```
