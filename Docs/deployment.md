# Documentazione di Deployment

## Descrizione del Progetto

Questo progetto riguarda la creazione di un ambiente containerizzato per un CMS WordPress, utilizzando Docker e Docker
Compose. L'ambiente include anche un database MySQL 8.x.

## Creazione del Branch di Lavoro Dedicato

Per creare un branch di lavoro dedicato, utilizzare il seguente comando git nel terminale:

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
version: '3.1'

services:
  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress-cms
      WORDPRESS_DB_PASSWORD: wordpress-cms
      WORDPRESS_DB_NAME: wordpress-cms

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: wordpress-cms
      MYSQL_USER: wordpress-cms
      MYSQL_PASSWORD: wordpress-cms
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
```

Per avviare i container, utilizzare il comando `docker-compose up` nel terminale.  

## Configurazioni del File docker-compose.yml
Il file docker-compose.yml contiene le configurazioni per i servizi WordPress e MySQL. Il servizio WordPress utilizza l'immagine ufficiale di WordPress e il servizio MySQL utilizza l'immagine ufficiale di MySQL 8.0. Entrambi i servizi sono configurati per riavviarsi sempre. Il servizio WordPress è esposto sulla porta 8080, mentre il servizio MySQL non è esposto su nessuna porta perché comunica con il servizio WordPress attraverso una rete interna.