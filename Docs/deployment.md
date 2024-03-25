# Deployment di WordPress con Docker

## Introduzione

Questa guida spiega come deployare un ambiente WordPress con MySQL usando Docker e Docker Compose.

## Prerequisiti

* Docker Desktop installato e configurato.
* Pycharm

## Passo 1: Installare Docker Desktop

1. Scaricare Docker Desktop da [https://www.docker.com/](https://www.docker.com/).
2. Installare Docker Desktop seguendo le istruzioni sullo schermo.

## Passo 2: Clonare il repository remoto
1. Con il terminale posizionarsi sulla directory desiderata
2. Eseguire il comando "git clone URL" per copiare il repository

## Passo 3: Aprire la cartella di progetto su Pycharm
1. Tasto destro sulla cartella di progetto e cliccare su apri con Pycharm

## Passo 4: Creare il file di configurazione Docker Compose

Creare un file `docker-compose.yml` nella tua directory di progetto e incolla il seguente codice:

```yaml
version: '3'

services:
  mysql:
    image: "mysql:8.0"
    environment:
      MYSQL_ROOT_PASSWORD: "password"
      MYSQL_DATABASE: "wordpress"
    volumes:
      - mysql_data:/var/lib/mysql
  wordpress:
    image: "wordpress:latest"
    ports:
      - "80:80"
    volumes:
      - wordpress_data:/var/www/html
    depends_on:
      - mysql

volumes:
  mysql_data:
  wordpress_data:
```

## Passo 5: Avviare il container
1. Eseguire tramite terminale il comando docker-compose up -d
2. Aprire un browser e collegarsi a http://localhost:80.


