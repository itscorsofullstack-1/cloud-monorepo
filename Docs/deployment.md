# Documentazione di Deployment

## Descrizione del Progetto

il progetto crea un'infrastruttura containerizzata pronta all'uso per eseguire un sito WordPress utilizzando Docker e Docker Compose, con un database MySQL come backend per memorizzare i dati del sito. 

## Creazione del Branch personale

Per creare un branch personale, utilizzare il seguente comando git nel terminale:

```bash
git checkout -b feature-nomecognome
```

## Creazione della Directory project-cms

Per creare la directory project-cms, utilizzare il comando mkdir nel terminale:

```bash
mkdir project-cms
```

## Creazione dell'Ambiente Containerizzato di WordPress

Per creare l'ambiente containerizzato di WordPress, è necessario un file docker-compose.yml all'interno della directory
project-cms.

```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress
    ports:
      - "8000:80"  # Mappa la porta 80 del container di WordPress alla porta 8000 del host
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: password
      WORDPRESS_DB_NAME: wordpress
   depends_on:
      - mysql 
  db:
    image: mysql:8
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: password
      MYSQL_ROOT_PASSWORD: rootpassword
```

Per avviare i container, utilizzare il comando `docker-compose up` nel terminale.  

## Verificare i container funzionanti

Per verificare se i container funzionano o meno utilizziamo i comandi su bash:

```bash
docker ps
```

Per verificare direttamente le caratteristiche di un singolo container

```bash
docker inspect <container_id>
```

## Configurazioni del File docker-compose.yml
Il file docker-compose.yml contiene le configurazioni per i servizi WordPress e MySQL. Il servizio WordPress utilizza l'immagine ufficiale di WordPress e il servizio MySQL utilizza l'immagine ufficiale di MySQL 8.0. Entrambi i servizi sono configurati per riavviarsi sempre. Il servizio WordPress è esposto sulla porta 8080, mentre il servizio MySQL non è esposto su nessuna porta perché comunica con il servizio WordPress attraverso una rete interna.