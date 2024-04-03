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

## Configurazioni del File docker-compose.yml
Il file docker-compose.yml contiene le configurazioni per i servizi WordPress e MySQL. Il servizio WordPress utilizza l'immagine ufficiale di WordPress e il servizio MySQL utilizza l'immagine ufficiale di MySQL 8.0. Entrambi i servizi sono configurati per riavviarsi sempre. Il servizio WordPress è esposto sulla porta 8080, mentre il servizio MySQL non è esposto su nessuna porta perché comunica con il servizio WordPress attraverso una rete interna.

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
   :qdepends_on:
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

Per fermare un container utilizziamo il comando su bash:

```bash
docker stop <container_id_o_nome>
```

Bisogna elencare tutte le images Docker e per vederli utilizzo questo comando su bash:

```bash
docker images
```
Bisogna cancellare tutte le immagini Docker collegare presenti nel nel sistema ed utilizzo questo comando su bash:

```bash
docker rmi <ID_immagine>
```

Bisogna far ripartire il container e lo rifacciamo con questo comando bash, all'interno della cartella dov'è il docker-compose.yml:

```bash
docker compose-up
```
Vado a creare due cartelle 'nginx' e 'ssl_certificates', dove all'interno della cartella di nginx ci metterò il 'Dockerfile' ed il 'nginx.conf' e nella cartella
'ssl_certificates' andrò a creare il certificato autofirmato

Per generare un certificato SSL ed una chiave privata, per crearo utilizzo questo comando su bash:

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout nginx.key -out nginx.crt
```

Con questo comando si andrà a creare un certificato autofirmato di nome 'nginx.crt' ed una chiave privata 'nginx.key'

Si crea un file di configurazione per Nginx che definisca il reverse proxy e la gestione SSL creando un file nginx.conf:

```bash
vi nginx.conf
```

e lo modifico con:

```bash
vim nginx.conf
```

e ci inserisco questo:

```nginx.conf
server {
    listen 443 ssl;
    server_name xpipe-ecommerce.local;

    ssl_certificate /nginx/nginx.crt;
    ssl_certificate_key /nginx/nginx.key;

    location / {
        proxy_pass http://your_upstream_server;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
