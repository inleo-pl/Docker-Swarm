Tworzymy plik yml:
```
vi calc.yml
```
Wpisujemy do niego:
```
version: '3.1'

services:
  calc:
    image: swarmgs/calc
    ports:
      - "8080:80"
    deploy:
      placement:
        constraints:
          - node.role==manager
```
Startujemy stack:
```
sudo docker stack deploy -c calc.yml calc
```
Tutaj możemy sprawdzić czy aplikacja działa:
```
http://manager01:8080/calc/iseverythingok
```
A tu można ją zepsuć:
```
http://manager01:8080/calc/divide?numerator=4&denumerator=2
```
Usuńmy uszkodzony serwis:
```
sudo docker service rm calc_calc
```
Uruchommy go jeszcze raz:
```
sudo docker stack deploy -c calc.yml calc
```
Następnie zmieńmy plik z konfiguracją:
```
vi calc.yml
```
Dopusjemy do niego sekcję healthcheck:
```
version: '3.1'

services:
  calc:
    image: swarmgs/calc
    ports:
      - "8080:80"
    healthcheck:
      test: curl -f -s -S http://localhost/calc/iseverythingok || exit 1
      interval: 5s
      timeout: 5s
      retries: 3
    deploy:
      placement:
        constraints:
          - node.role==manager
```
Aktualizujemy stack:
```
sudo docker stack deploy -c calc.yml calc
```
Sprawdzamy aplikację i ją psujemy:
```
http://manager01:8080/calc/iseverythingok
http://manager01:8080/calc/divide?numerator=4&denumerator=2
```
Teraz poczekaj kilka sekund i...
```
http://manager01:8080/calc/iseverythingok
```
