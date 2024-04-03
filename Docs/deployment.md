## Prerequisiti

- Docker Compose
- PyCharm
- Nginx


## Impostazione del progetto

1. Clonato il repository sulla propria macchina locale.

```bash
git clone https://github.com/itscorsofullstack-1/cloud-monorepo.git
```

2. Entrare nella cartella `IaC/project-cms`.

```bash
cd IaC/progetto-cms
```

3. Aggiornato il file `.env` con le impostazioni locali. Il file contiene le variabili d'ambiente, come le credenziali del database, il dominio dell'applicazione e la configurazione della rete.


## Docker Compose

Utilizzato Docker Compose per la gestione e esecuzione dei containers docker. Il file `docker-compose.yml` nella cartella principale definisce i servizi, le reti e i volumi per l'applicazione.

I servizi includono:

- `app`: applicazione WordPress.
- `db`: database MySQL.
- `ingress`: controller di ingress Nginx.


## Esecuzione dell'applicazione

1. Dalla cartella `IaC/project-cms`, avviati i contenitori Docker con Docker Compose.

```bash
docker-compose up -d
```

## Modifica del file wp-config.php

Modificato il file `wp-config.php` all'interno del container Docker. In questo caso, ho usato `nano` per modificare il file.

Ecco i passaggi:

1. Identificato il nome del container in cui è in esecuzione l'applicazione WordPress tramite il comando `docker ps` e cercato il container con il nome `project-cms`.

2. Eseguito il comando `docker exec` con il nome del container e il comando per aprire l'editor di testo `nano`.

3. Una volta all'interno del container, eseguito il comando `apt update` per aggiornare i pacchetti.

4. Infine, modificato il file `wp-config.php`.

5. Modificate le righe seguenti per consentire a WordPress di utilizzare il dominio corretto:

```php
define('WP_SITEURL', 'http://' . $_SERVER['HTTP_HOST']);
define('WP_HOME', 'http://' . $_SERVER['HTTP_HOST']);
```

## Accesso all'applicazione

1. Aprire un browser web e navigare su `https://cms.sindriaschool.org` per accedere all'applicazione WordPress.


## Certificati SSL

I certificati SSL per l'applicazione sono memorizzati nella cartella `IaC/project-cms/ingress/certs`. I file `self.crt` e `self.key` sono certificati autofirmati che possono essere usati per lo sviluppo locale. Per la produzione, sostituirli con i propri certificati SSL validi.


## File Hosts

Il file `hosts` contiene il dominio locale dell'applicazione. Aggiungete la voce di questo file al file hosts del vostro sistema per consentire al sistema di risolvere il dominio.

- Sui sistemi Unix, il file hosts si trova in `/etc/hosts`.
- Nei sistemi Windows, il file hosts si trova in `C:\Windows\System32\drivers\etc\hosts`.