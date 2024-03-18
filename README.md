## Inhaltsverzeichnis

1. **[KN01](#kn01)**
   - [A) Instalation](#a-instalation)
   - [B) Docker Command Line Interface](#b-docker-command-line-interface)
     - [NGINX IMAGE](#nginx-image)
2. **[KN02](#kn02)**
   - [A) Dockerfile 1](#a-dockerfile-1)
     - [Notwendige Docker Befehle](#notwendige-docker-befehle)
     - [Screenshot vom Docker Desktop](#screenshot-vom-docker-desktop)
   - [B) Dockerfile 2](#b-dockerfile-2)
     - [Telnet Befehl](#telnet-befehl)
     - [Dockerfile für DB Container](#dockerfile-für-db-container)
       - [DB: docker build und docker run Befehle für Ihren DB-Container](#db-docker-build-und-docker-run-befehle-für-ihren-db-container)
       - [Screenshort info.php](#screenshort-infophp)
       - [Screenshort db.php](#screenshort-dbphp)
     - [Dockerfile für den Web Container](#dockerfile-für-den-web-container)
       - [Web: docker build und docker run Befehle für Ihren Web-Container](#web-docker-build-und-docker-run-befehle-für-ihren-web-container)
3. **[KN03](#kn03)**
   - [Befehle zur Erstellung und Verwaltung von Docker-Netzwerken](#befehle-zur-erstellung-und-verwaltung-von-docker-netzwerken)
   - [Beschreibung der Konfiguration und Interaktion von Containern in verschiedenen Netzwerken](#beschreibung-der-konfiguration-und-interaktion-von-containern-in-verschiedenen-netzwerken)



[Alle verwendeten Befehle](https://github.com/Rubenizz/M347/blob/main/KN01.txt)


# M347
Modul 347 - Nussle

## KN01
### A) Instalation
<img width="1167" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/df764993-1687-4364-99e2-94ffd2e8e1f5">

### B) Docker Command Line Interface

### NGINX IMAGE

<img width="1169" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/718a2143-e301-48ca-9f3c-0cac34e766f7">

<img width="363" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/b6df44af-0d90-4e51-8744-94025da6f817">

<img width="1078" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/f9a8b198-e6ea-4032-93d4-b834f9637e26">


### C) Registry und Repository

<img width="1168" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/c1ded503-0432-4fe1-90fa-c5805837f2bc">

### D) Privates Repository

<img width="1136" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/c3af30df-6569-47f1-a7fa-3dea3c87df5f">


## KN02

## A) Dockerfile 1
[Dokumentiertes Dockerfile](https://github.com/Rubenizz/M347/blob/main/Dokumentiertes_Dockerfile.txt)

[Dockerfile](https://github.com/Rubenizz/M347/blob/main/Dockerfile)

### Notwendige Docker Befehle
- docker tag kn02a rubenkpt/m347:kn02a
- docker build -t rubenkpt/m347:kn02a .
- docker push rubenkpt/m347:kn02a
- docker run -p 8888:80 rubenkpt/m347:kn02a

### Screenshot vom Docker Desktop

<img width="1162" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/f96864f4-b63d-4f1a-926b-540a2f526a34">

### Screenshot vo der Hello World Seite 

<img width="1168" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/40c10f6f-cae5-401b-bd89-2faa4aafc1bf">

## B) Dockerfile 2
### Telnet Befehl
<img width="672" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/4afba2fd-b109-4926-aae6-75b5e3c98638">

### Dockerfile für DB Container:
FROM mariadb:latest

ENV MARIADB_ROOT_PASSWORD="123"

EXPOSE 3306
### DB: docker build und docker run Befehle für Ihren DB-Container
- docker build -t kn02b-db .
- docker run -d -p 3306:3306 --name kn02b_db kn02b-db

### Screenshort info.php
<img width="1165" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/90e050fc-8456-4dbf-82b2-d2f1a428763d">

### Screenshort db.php
<img width="1131" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/25af196f-35ca-4e13-9e8a-22b766583e3f">

### Dockerfile für den Web Container
FROM php:8.0-apache
 
RUN docker-php-ext-install mysqli
 
COPY info.php /var/www/html/
COPY db.php /var/www/html/
 
EXPOSE 80

### Web: docker build und docker run Befehle für Ihren Web-Container

- docker build -t kn02b-web .
- docker run -d -p 80:80 --name kn02b_web --link kn02b_db kn02b-web


https://github.com/Rubenizz/M347/blob/main/db.php
https://github.com/Rubenizz/M347/blob/main/info.php


## KN03

```docker network create tbz```

```docker pull busybox:latest```

```docker run --name=busybox1 -it --network=tbz busybox```

```docker run --name=busybox2 -it --network=tbz busybox```

```docker run --name=busybox3 -it --network=bridge busybox```

```docker run --name=busybox4 -it --network=bridge busybox```

### 1)
busybox1:
- Ip:172.21.0.2
- Gateway:172.21.0.1
  
usybox2:
- Ip:172.21.0.3
- Gateway:172.21.0.1
  
busybox3:
- Ip:172.17.0.2
- Gateway:172.17.0.1
  
busybox4:
- Ip:172.17.0.3
- Gateway:172.17.0.1

### 2)

<img width="308" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/1c2a6faf-73c5-4581-a6d5-66f1119aaa32">

<img width="320" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/95e29fd8-2de8-483a-87ab-ad19b69cb090">

Die Befehle: ```ping busybox2``` und ```ping IP-von-busybox2``` funktionieren, da diese den gleichen Default-Gateway haben wie busybox1 (172.21.0.1)

### 3)

<img width="341" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/d4effb57-b983-488b-a649-c8a9e933a155">

Der Befehl ```ping IP-von-busybox4``` funktioniert. (Gateway: 172.17.0.1)


In Kn02 befanden sich die beiden Docker Container im Bridge Netzwerk. Sie konnten zusammen über den Link kommunizieren.
Sie kommunizieren zusammen über den Server und brauchen keinen link mehr.
