Pobierz klucz
```
wget https://raw.githubusercontent.com/inleo-pl/Warsztaty-Docker-Swarm/master/Docker_Swarm.pem
```
Nadaj uprawnienia i połącz się:
```
chmod 600 /miejsce/gdzie/jest/Docker_Swarm.pem
ssh -i /miejsce/gdzie/jest/Docker_Swarm.pem ubuntu@manager01
ssh -i /miejsce/gdzie/jest/Docker_Swarm.pem ubuntu@worker01
ssh -i /miejsce/gdzie/jest/Docker_Swarm.pem ubuntu@worker02
```
