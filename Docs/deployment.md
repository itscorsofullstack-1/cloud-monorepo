# Documentazione di Deployment

## Descrizione del Progetto

Questo progetto riguarda la creazione di un ambiente containerizzato per un CMS WordPress, utilizzando Docker Compose e nginx. L'ambiente include anche un database MySQL 8.x.

## Creazione del Branch di Lavoro Dedicato

Creato un branch di lavoro dedicato, utilizzare il seguente comando git nel terminale:

```bash
git checkout -b feature-nomecognome
```

## Creazione della Directory project-cms

Creata la directory project-cms, utilizzando il comando mkdir nel terminale:

```bash
mkdir project-cms
```

## Creazione dell'Ambiente Containerizzato di WordPress

Creato l'ambiente containerizzato di WordPress con il file docker-compose.yml all'interno della directory project-cms.

```yaml
version: "3.1"

services:
  wordpress:
    container_name: wordpress_container
    hostname: wordpress
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress-cms
      WORDPRESS_DB_PASSWORD: wordpress-cms
      WORDPRESS_DB_NAME: wordpress-cms
    networks:
      - wordpress_network

  db:
    container_name: db_container
    hostname: db
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: wordpress-cms
      MYSQL_USER: wordpress-cms
      MYSQL_PASSWORD: wordpress-cms
      MYSQL_RANDOM_ROOT_PASSWORD: "1"
    networks:
      - wordpress_network

  nginx:
    image: nginx:latest
    container_name: nginx_proxy
    hostname: nginx
    ports:
      - 443:443
    volumes:
      - ./app.conf:/etc/nginx/conf.d/app.conf
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./snippets:/etc/nginx/snippets
      - ./ssl:/etc/nginx/ssl
    networks:
      - wordpress_network

networks:
  wordpress_network:
    driver: bridge

Per avviare i container, utilizzare il comando `docker-compose up` nel terminale.  

## Configurazioni nel File docker-compose.yml
Il file docker-compose.yml contiene le configurazioni per i servizi WordPress e MySQL. 
I servizi WordPress e MySQL 8.0 utilizzano le immagini ufficiali. 
Entrambi i servizi sono configurati per riavviarsi sempre. 
Il servizio WordPress è esposto sulla porta 8080, mentre il servizio MySQL non è esposto su nessuna porta perché comunica con il servizio WordPress attraverso una rete interna.