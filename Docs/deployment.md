## Setting iniziale

Clonare la repository tramite il comando bash:

```bash
git clone https://github.com/itscorsofullstack-1/cloud-monorepo.git
```

Andare nella branch `feature-lucapitzoi` e copiare la branch con `git checkout -b soluzione-NomeCognome`

# Windows - aprire prompt come amministratore e poi aprire il file con notepad.exe
# C:\Windows\System32\drivers\etc\hosts

aggiungendo all'indirizzo 127.0.0.1	cms.sindriaschool.org tramite modifica

Navigare nella cartella `IaC/project-cms`.

```bash
cd IaC/progetto-cms
```

Aggiornare il file `.env` con le impostazioni locali, se necessario. Il file contiene le variabili d'ambiente per l'applicazione, come le credenziali del database, il dominio dell'applicazione e la configurazione della rete.


## Docker Compose

Questo progetto utilizza Docker Compose per gestire ed eseguire i contenitori Docker. Il file `docker-compose.yml` nella cartella principale definisce i servizi, le reti e i volumi per l'applicazione.

I servizi includono:

- `app`: È l'applicazione WordPress.
- `db`: È il database MySQL per l'applicazione WordPress.
- `ingress`: È il controller di ingress Nginx.


## Esecuzione dell'applicazione

1. Dalla cartella `IaC/project-cms`, avviare i contenitori Docker con Docker Compose.

```bash
docker-compose up -d
```

## Modifica del file wp-config.php di WordPress

Per modificare il file `wp-config.php` all'interno del container Docker, è possibile utilizzare il comando `docker exec` per eseguire un comando all'interno del container. In questo caso, si può utilizzare un editor di testo come `vim` o `nano` per modificare il file.

Ecco i passaggi:

1. Identificare il nome del container Docker in cui è in esecuzione l'applicazione WordPress. Puoi farlo utilizzando il comando `docker ps` e cercando il container con il nome `project-cms`.

2. Esegui il comando `docker exec` con il nome del container e il comando per aprire l'editor di testo. Ad esempio, se stai utilizzando `nano` e il nome del container è `project-cms`, il processo sarebbe:

```bash
docker exec -it project-cms bash
```

3. Una volta all'interno del container, esegui il comando `apt update` per aggiornare i pacchetti.

```bash
apt update
```

4. Installa l'editor di testo `nano` con il comando:

```bash
apt install nano
```

5. Infine, modifica il file `wp-config.php` con l'editor di testo `nano`.

```bash
nano /var/www/html/wp-config.php
```

6. Modifica le righe seguenti per consentire a WordPress di utilizzare il dominio corretto:

```php
define('WP_SITEURL', 'http://' . $_SERVER['HTTP_HOST']);
define('WP_HOME', 'http://' . $_SERVER['HTTP_HOST']);
```

7. Salva le modifiche e esci dall'editor di testo. Se stai utilizzando `nano`, puoi farlo premendo `Ctrl+X`, poi `Y` per confermare il salvataggio, e infine `Enter` per uscire.


## Accesso all'applicazione

1. Aprire un browser web e navigare su `https://cms.sindriaschool.org` per accedere all'applicazione WordPress.


## Certificati SSL

I certificati SSL per l'applicazione sono memorizzati nella cartella `IaC/project-cms/ingress/certs`. I file `self.crt` e `self.key` sono certificati autofirmati che possono essere usati per lo sviluppo locale. Per la produzione, sostituirli con i propri certificati SSL validi.


## File Hosts

Il file `hosts` contiene il dominio locale dell'applicazione. Aggiungete la voce di questo file al file hosts del vostro sistema per consentire al sistema di risolvere il dominio.

- Sui sistemi Unix, il file hosts si trova in `/etc/hosts`.
- Nei sistemi Windows, il file hosts si trova in `C:\Windows\System32\drivers\etc\hosts`.