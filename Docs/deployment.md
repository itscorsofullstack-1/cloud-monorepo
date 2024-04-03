# Guida completamento esercizio

## Prerequisiti
- Docker
- Docker Compose
- PyCharm

## Configurazione del Progetto
1. Clonare il repository sul proprio sistema locale.

```git clone https://github.com/itscorsofullstack-1/cloud-monorepo.git ```

2. Navigare nella cartella `IaC/project-cms`.

```cd IaC/progetto-cms```

3. Aggiornare il file `.env` con le configurazioni locali, se necessario. Questo file contiene le variabili d'ambiente per l'applicazione, come le credenziali del database, il dominio dell'applicazione e la configurazione della rete.

## Utilizzo di Docker Compose
Questo progetto sfrutta Docker Compose per gestire ed eseguire i contenitori Docker. Il file `docker-compose.yml` nella cartella principale definisce i servizi, le reti e i volumi per l'applicazione.

I servizi includono:
- `app`: L'applicazione WordPress.
- `db`: Il database MySQL per l'applicazione WordPress.
- `ingress`: Il controller di ingresso Nginx.

## Avvio dell'Applicazione
Dalla cartella `IaC/project-cms`, avviare i contenitori Docker utilizzando Docker Compose.

```docker-compose up -d```


## Modifica di wp-config.php di WordPress
Per modificare il file `wp-config.php` all'interno del container Docker, seguire questi passaggi:

1. Identificare il nome del container Docker in cui è in esecuzione l'applicazione WordPress utilizzando il comando `docker ps`.
2. Eseguire il comando `docker exec` con il nome del container e il comando per aprire l'editor di testo desiderato.

```docker exec -it <nome_container> bash```

3. All'interno del container, eseguire `apt update` per aggiornare i pacchetti, quindi installare un editor di testo come `nano`.

```apt update```

```apt install nano```

4. Modificare il file `wp-config.php` con l'editor di testo.

```nano /var/www/html/wp-config.php```

5. Modificare le righe per consentire a WordPress di utilizzare il dominio corretto.

```define('WP_SITEURL', 'http://' . $_SERVER['HTTP_HOST']);```
```define('WP_HOME', 'http://' . $_SERVER['HTTP_HOST']);```

6. Salvare le modifiche ed uscire dall'editor di testo.

## Accesso all'Applicazione
Aprire un browser web e accedere all'applicazione WordPress navigando su `https://cms.sindriaschool.org`.

## Certificati SSL
I certificati SSL per l'applicazione sono memorizzati nella cartella `IaC/project-cms/ingress/certs`. I file `self.crt` e `self.key` sono certificati autofirmati che possono essere usati per lo sviluppo locale. Per l'ambiente di produzione, è necessario sostituirli con i propri certificati SSL validi.

## File Hosts
Aggiungere la voce del dominio locale nel file hosts del sistema per consentire al sistema di risolvere il dominio.

- Nei sistemi Unix, il file hosts si trova in `/etc/hosts`.
- Nei sistemi Windows, il file hosts si trova in `C:\Windows\System32\drivers\etc\hosts`.
