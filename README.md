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
4. **[KN04](#kn04)**



  


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


## KN04

<img width="913" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/a4110c04-15ed-4b05-97f3-3d7238bb3ac6">

### Info.php

<img width="1170" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/a4fe3757-d1b2-4c4d-9268-a31d1019db52">

### db.php

<img width="1170" alt="image" src="https://github.com/Rubenizz/M347/assets/112400838/951974ce-0e87-46e9-ab5f-a14ee9b33918">

https://github.com/Rubenizz/M347/blob/main/Dockerfile

https://github.com/Rubenizz/M347/blob/main/docker-compose.yml

### Teil b)
### info.php

![image](https://github.com/Rubenizz/M347/assets/112400838/5ed1f421-be81-4f90-a17c-c57f0d56cb07)

### db.php

![image](https://github.com/Rubenizz/M347/assets/112400838/96e0d61a-bb95-40c7-b76d-3fbff02bc2c2)

### Docker compose file
```
version: '3.8'
services:
  database:
    image: rubenkpt/m347:kn02db
    container_name: m347-kn04a-db
    environment:
      MYSQL_ROOT_PASSWORD: example
    networks:
      kn04-network:
        ipv4_address: 172.10.5.2
  web: 
    image: rubenkpt/m347:kn02web
    container_name: m347-kn04a-web
    ports:
      - "5600:80"
    depends_on:
      - database
    networks:
      kn04-network:
        ipv4_address: 172.10.5.3

networks:
  kn04-network:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 172.10.0.0/16
          ip_range: 172.10.5.0/24
          gateway: 172.10.5.254
```

Der Fehler tritt auf, weil wir die Werte für den Datenbank Login fest codiert haben. Dadurch können wir keine einfache Verbindung herstellen. Eine Lösung könnte darin bestehen, in der Docker-Compose-Datei eine Umgebungsvariable zu definieren und in der Datei "db.php" die Werte dieser environment variablen zu verwenden. Auf diese Weise ist es wesentlich einfacher, Einstellungen anzupassen.

## B)

![image](https://github.com/Rubenizz/M347/assets/112400838/12f73804-fa3c-44d7-8a16-05bf7d7df942)

![image](https://github.com/Rubenizz/M347/assets/112400838/f17b8a4a-4a3c-4d63-b536-1a4575191e22)

![image](https://github.com/Rubenizz/M347/assets/112400838/309c1cb6-c3e0-401e-b8e4-89c866c20dc2)

#### cloud init Datei

```
#cloud-config
# source: https://gist.github.com/syntaqx/9dd3ff11fb3d48b032c84f3e31af9163
users:
  - name: ubuntu
    sudo: ALL=(ALL) NOPASSWD:ALL
    groups: users, admin
    home: /home/ubuntu
    shell: /bin/bash
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCUBo+qnNu5xxM9vfz4C04M36FHxHNrEMdm5TkFj1/SfVtqunlUOeMpu7nFCZZKnX8HYwf/MkjcBiTYAgncxku8grwl6XuW/pcvmb6/ghSIaw4xtRRSzit7omqJ5d8kXB3+Nd1aaMHsjfly4nkaqswhySVXQqr8Hw6DbWVw8jLLVKEE+5NZHY33hJkhJwK4blCllsGpmQaKi1qxjsN0hZOWNK01iJAydwD8t2xJ0NOYbq8Qas5IyPnRN7SPxvEhIP6WLQ6Ym6Dmf8FwNW1cHLTKabgjzt5f/HKUkKS89dPd3fn4nnFli1BOMECGUIvVlOw2pQNri7+04OOfn2FGlqr5  teacher
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClTwSwEolWaVuXiakhYqehF1X9dOi8iwNCS/PPIgisSd7dToLsD74+fOcUrocbLZMIwBJWDKComo8a0VKOVXug0RqXOIkOliIHNsaXurkkBuc3WtVtz2SQZJEkGnCbmHp2NBGutEfJqTTEfrQxaj3MW20hQRxi+PDhvagH1h5KlIwCEiL3ObJR/8DR8Pq4QDyoBosCHm3BoPKvHoEZ8wh1ohL7K+uD0Yo/R7iNEQpmTrdqPzYv8rSPQCVheoMlMu2QykQwtEUpM1IZmYgAkz1oDhaI8Pv0tyFB4XMcjs8WcroNBavD4WxoVuabWd9Sv03zXAX2Q6ZtyylDRnT+4AOz ruben
ssh_pwauth: false
disable_root: false
package_update: true
package_upgrade: true
groups:
  - docker
system_info:
  default_user:
    groups: [docker]
packages:
  - apt-transport-https
  - ca-certificates
  - curl
  - gnupg
  - lsb-release
  - unattended-upgrades
final_message: "The system is finally up, after $UPTIME seconds"
write_files:
  - path: /home/ubuntu/src/db.php
    permissions: "0644"
    content: |
      <?php
        //database
        $servername = "m347-kn04a-db"; // Private IP Adresse des DB Server
        $username = "root";
        $password = "example";
        //$dbname = "example-database";

        // Create connection
        $conn = new mysqli($servername, $username, $password);//, $dbname);
        // Check connectionsa<
        if ($conn->connect_error) {
          die("Connection failed: " . $conn->connect_error);
        }
        $sql = "select Host, User from mysql.user;";
        $result = $conn->query($sql);
        while($row = $result->fetch_assoc()){
          echo($row["Host"] . " / " . $row["User"] . "<br />");
        }
        //var_dump($result);
      ?>
  - path: /home/ubuntu/src/info.php
    permissions: "0644"
    content: |
      <?php
        phpinfo();
      ?>
  - path: /home/ubuntu/dockerfile
    permissions: "0644"
    content: |
      FROM php:8.0-apache
      WORKDIR /var/www/html/
      COPY src .
      EXPOSE 80
      RUN ["docker-php-ext-install", "mysqli"]
  - path: /home/ubuntu/docker-compose.yml
    permissions: "0644"
    content: |
      version: '3.8'
      name: kn04-compose
      services:
        database:
          image: mariadb:latest
          container_name: m347-kn04a-db
          ports:
            - "3306:3306"
          environment:
            - MARIADB_ROOT_PASSWORD=example
          networks:
            - kn04-network
        web:
          build: .
          container_name: m347-kn04a-web
          ports:
            - "80:80"
          depends_on:
            - database
          networks:
            - kn04-network
      networks:
        kn04-network:
          driver: bridge
          ipam:
            config:
              - subnet: 172.10.0.0/16
                ip_range: 172.10.5.0/24
                gateway: 172.10.5.254
runcmd:
  - mkdir -p /etc/apt/keyrings
  - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  - echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
  - apt-get update
  - apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
  - systemctl enable docker
  - systemctl start docker
  - cd /home/ubuntu
  - sudo docker compose up -d
```
## KN05

### A) Bind mounts
#### Liste der Befehle:
Docker mit dem bind-mount erstellen: ```docker run -d --name kn05 -v C:\Users\Ruben\TBZ_m347\KN05:/mnt nginx```
![image](https://github.com/Rubenizz/M347/assets/112400838/f2f0e9fc-d0e1-4891-b403-cb82b402090e)


Jetzt ist noch kein File vorhanden

![image](https://github.com/Rubenizz/M347/assets/112400838/52921e6d-dfb6-4128-9777-9952e0d8c91b)

Jetzt ist ein File vorhanden

![image](https://github.com/Rubenizz/M347/assets/112400838/19551573-70eb-48cf-b8a9-ca8e66b1179a)

Inhalt des File: 
```
#!/bin/bash

echo "Ruben Schneebeli Skript"
```

## B)

![image](https://github.com/Rubenizz/M347/assets/112400838/658aeaf0-d73d-4651-bf06-713caa8b35e3)

Commands: 
```
docker run -d --name container1 -v kn05Volume:/data nginx
docker run -d --name container2 -v kn05Volume:/data nginx

docker exec -it container1 bash
echo "Hello from container 1" >> /data/test.txt

docker exec -it container2 bash
echo "Hello from container 2" >> /data/test.txt
```
Im Bash vom zweiten Container
```cat /data/test.txt```

![image](https://github.com/Rubenizz/M347/assets/112400838/39ba44de-2f6a-48af-b055-e3072af50682)

## C) 


![image](https://github.com/Rubenizz/M347/assets/112400838/25fc0f4b-43ee-49ff-892a-7c90005d5efd)


![image](https://github.com/Rubenizz/M347/assets/112400838/40623731-80a9-4097-a2e6-800c7131360d)


docker-compose File
```
version: '3.8'
name: kn05-compose
services:
  container-1:
    image: nginx:latest
    container_name: kn05c-con-1
    volumes:
      - type: volume
        source: ruben-volume
        target: "/var/www/html/"
      - type: bind
        source: "C:/Users/Ruben/TBZ_m347/KN05/compose"
        target: /usr/share/nginx/html
      - type: tmpfs
        target: "/random-dir"
    ports:
      - "2100:80"
  container-2:
    image: nginx:latest
    container_name: kn05c-con-2
    volumes:
      - ruben-volume:/usr/share/nginx/html:rw
    ports:
      - "2200:80"
volumes:
  ruben-volume: {}
```


## KN06
#### Master:

![image](https://github.com/Rubenizz/M347/assets/112400838/e59ebef8-f524-4b6f-a306-47d539b1f5cc)

#### Node1:

![image](https://github.com/Rubenizz/M347/assets/112400838/bde47db1-2b08-4c90-8457-f9e67f132d49)


#### Node2:

![image](https://github.com/Rubenizz/M347/assets/112400838/58f5455e-c4a9-49ba-9fc3-2a5e14b2eab8)

#### Status:

![image](https://github.com/Rubenizz/M347/assets/112400838/b8c0a273-9732-41fa-87c4-b9f52f76d3fd)


Node vom Cluster entfernen:

```microk8s leave```

![image](https://github.com/Rubenizz/M347/assets/112400838/17cc6d4f-eb1e-4e5d-9835-305b4fd10b6c)

#### Node1 (Worker):

![image](https://github.com/Rubenizz/M347/assets/112400838/8f830b0a-4186-451e-9d59-a56d4045fe47)

#### Status:

![image](https://github.com/Rubenizz/M347/assets/112400838/2e29a4c0-d2ec-4cd9-8747-1aa420138752)

Der Unterschied ist, dass wenn nur eine Node existiert ist es kein High-Availability Cluster, da es bei einem Ausfall keine andere Node gibt, welche die Arbeit übernehmen kann. Dazu sieht man die Ip Adressen der verbundenen Nodes.
Es bechreibt den status von kubernetes und zeigt, wer alles verbunden ist und was es für Rolle es nimmt. Es zeigt auch, was für addon wurden dazu gegeben.

mit microk8s bearbeitet man einzelne node in einem Cluster. Mit kubectl bearbeitet man das ganze Kluster, dass mehrere nodes enthaltet. Da muss man microk8s kubectl anschrieben, damit man das Cluster bearbeiten kann.

## KN07

#### Pod / Replica
Ein Pod ist eine Gruppe von einem oder mehreren Containern, die eng zusammenarbeiten und gemeinsame Ressourcen und ein gemeinsames Netzwerk teilen.
Replikas sind Kopien eines Pods, die es ermöglichen, die Verfügbarkeit und Skalierbarkeit einer Anwendung zu steuern, indem sie die Anzahl der laufenden Instanzen eines Pods definieren.

#### Service / Deployment
Ein Deployment beschreibt, wie Pods bereitgestellt und aktualisiert werden sollen, während ein Service einen stabilen Netzwerkzugriff auf eine Gruppe von Pods bereitstellt.

#### Ingress
Ingress löst das Problem des externen Zugriffs auf Dienste innerhalb eines Kubernetes-Clusters, indem es den HTTP- und HTTPS-Routingverkehr basierend auf Regeln an verschiedene Dienste innerhalb des Clusters weiterleitet. Kurz gesagt, Ingress ermöglicht es, dass externe Anfragen über eine einzelne IP-Adresse und einen bestimmten Port auf verschiedene Dienste innerhalb des Clusters geroutet werden können, basierend auf den Anforderungen und Konfigurationen.

#### Statefulset
StatefulSets sind für die Bereitstellung von zustandsbehafteten Anwendungen in Kubernetes geeignet, die eine stabile Netzwerkidentität und/oder persistente Speicherung benötigen.

![image](https://github.com/Rubenizz/M347/assets/112400838/5220f60b-a98e-478c-80ec-45d199fa0ed5)

``` microk8s kubectl describe service webapp-service ```

#### Master:

![image](https://github.com/Rubenizz/M347/assets/112400838/c0df8ce5-f491-409f-b848-c97ce326d876)

#### Node1:

![image](https://github.com/Rubenizz/M347/assets/112400838/7915d2c2-1874-41b5-a2c4-d9c52657444c)

#### Mongo DB service 

![image](https://github.com/Rubenizz/M347/assets/112400838/f93022f8-bb17-4111-a245-632a6e0c5165)

Es zeigt die info der MongoDB service

#### Master

![image](https://github.com/Rubenizz/M347/assets/112400838/c0df8ce5-f491-409f-b848-c97ce326d876)

#### Node1

![image](https://github.com/Rubenizz/M347/assets/112400838/7f581c4c-e0e2-44e9-af83-4003f4e7c70b)

Ich musste nur die Ip adresse ändern zu der öffentlichen Ip von Node 1

Das verbinden zur Datenbank würde nicht gehen, da wir den Port vom AWS nicht eröffnet hat. Das andere Problem wäre, dass wir den Port vom Kubernetes nicht veröffentlichen. mann musste in der db.yml den Port eröffnen und im AWS eröffnen, damit wir verbinden könnten

#### Master mit neuer Ip Adresse

![image](https://github.com/Rubenizz/M347/assets/112400838/f1f593fe-72a7-47dd-a0e3-f7781fd4b4b6)

## KN08

### DB erstellen

#### DB erstellt
![image](https://github.com/Rubenizz/M347/assets/112400838/83b48c4f-06b3-4ed3-84dc-4836c5ec3e97)

#### Connection gemacht
![image](https://github.com/Rubenizz/M347/assets/112400838/d973a5a1-b8d5-4f52-b289-6596a3be310c)

#### Daten reingeladet
![image](https://github.com/Rubenizz/M347/assets/112400838/3eef7496-0aa0-44dd-914c-1679c3cdad07)

#### Frontend starten

![image](https://github.com/Rubenizz/M347/assets/112400838/2a76efab-021d-45c1-9b12-5951390fb4d1)

#### Applikation in Container packen

![image](https://github.com/Rubenizz/M347/assets/112400838/b2931417-85fe-4fc4-8c30-3179ded9bab9)

![image](https://github.com/Rubenizz/M347/assets/112400838/c887d8c7-69f8-47e4-8ef8-a11ff5571f70)

### Swagger

![image](https://github.com/Rubenizz/M347/assets/112400838/f6e5f896-1708-47c0-bb89-2e546aa9932f)

