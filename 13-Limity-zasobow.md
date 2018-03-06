Stworzym kolejny konfig i plik yml:
```
vi redis.yml
```
Wpisz do pliku:
```
version: '3.1'

services:
  redis:
    image: redis:alpine
    deploy:
      resources:
        limits:
          cpus: '0.50'
          memory: 50M
        reservations:
          cpus: '0.25'
          memory: 20M
```
Zaktualziuj stack i sprawdz konfigurajcę:
```
sudo docker stack deploy -c redis.yml redis
sudo docker inspect redis_redis
```
