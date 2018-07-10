Zapoznajmy sie z komendą:
```
sudo docker secret --help
sudo docker secret ls
```
Dodajemy nasz secret:
```
sudo echo cmentarnapolka | sudo docker secret create mysql_root_password -
```
Stwórzmy plik z definicją stacka:
```
vi mysql.yml
```
Wprowadźmy do niego:
```
version: '3.1'
services:
  mysql:
    image: mysql
    environment: 
      MYSQL_USER: wordpress
      MYSQL_DATABASE: wordpress
      # MYSQL_ROOT_PASSWORD: root
    secrets:
      - mysql_root_password
    deploy:
      placement:
        constraints:
          - node.role==manager
secrets:
  mysql_root_password:
    external: true
```
Uruchommy stack:
```
sudo docker stack deploy -c mysql.yml mysql
sudo docker stack ps mysql
```
Sprawdźmy co się stało, że stack się nie uruchomił:
```
sudo docker service logs mysql_mysql
```
Edytujjmy plik yml:
```
vi mysql.yml
```
Dorzucamy zmienną:
```
version: '3.1'
services:
  mysql:
    image: mysql
    environment: 
      MYSQL_USER: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_ALLOW_EMPTY_PASSWORD: "yes"
      # MYSQL_ROOT_PASSWORD: root
    secrets:
      - mysql_root_password
    deploy:
      placement:
        constraints:
          - node.role==manager       
secrets:
  mysql_root_password:
    external: true
```
Aktualizujemy stack:
```
sudo docker stack deploy -c mysql.yml mysql
sudo docker stack ps mysql
```
Dostęp do secret w kontenerze:
```
sudo docker ps
sudo docker exec -it [ID] bash
  cd run
  cd secrets
  ls
  cat mysql_root_password
  exit
```
Finalna rekonfiguracja MySQL:
```
vi mysql.yml

version: '3.1'
services:
  mysql:
    image: mysql
    environment: 
      MYSQL_USER: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_ROOT_PASSWORD_FILE: "/run/secrets/mysql_root_password"
    secrets:
      - mysql_root_password
    deploy:
      placement:
        constraints:
          - node.role==manager       
secrets:
  mysql_root_password:
    external: true
```
Aktualizacja stack i podłączenie się do konteneraz z mysql:
```
sudo docker stack deploy -c mysql.yml mysql
sudo docker ps
docker exec -it [ID] bash
  mysql -u root -p
    show databeses;
    exit
  exit
```
