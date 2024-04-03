# Procedura di Deployment del CMS WordPress con Docker Compose

# Prerequisiti:
1. Assicurati di avere Docker e Docker Compose installati sul tuo sistema.
2. Assicurati di avere Pycharm installato sul tuo sistema.
3. Assicurati di avere una repository dove poter creare una nuova branch chiamata feature-nomecognome.

# 1. Creazione della directory "project-cms" e del file "docker-compose.yml"
1. Aprire la repository nella propria branch feature-nomecognome.
2. Entrare nella cartella Docs.
3. Creare la cartella "project-cms".
4. Entrare nella cartella.
5. Creare il file "docker-compose.yml".
6. Modificare il file e salvandolo inserendo questo contenuto:
    ```yaml
   version: '3.8'

   services:
     db:
       image: mysql:8
       restart: always
       environment:
         MYSQL_ROOT_PASSWORD: example_password
         MYSQL_DATABASE: wordpress
         MYSQL_USER: wordpress_user
         MYSQL_PASSWORD: wordpress_password

     wordpress:
       depends_on:
         - db
       image: wordpress:latest
       restart: always
       ports:
         - "8080:80"
       environment:
         WORDPRESS_DB_HOST: db:3306
         WORDPRESS_DB_USER: wordpress_user
         WORDPRESS_DB_PASSWORD: wordpress_password
         WORDPRESS_DB_NAME: wordpress 
    ```
Questo file definisce due servizi:

db: Utilizza l'immagine MySQL 8.x ufficiale. Imposta le variabili d'ambiente per il nome del database, l'utente e la password.

wordpress: Utilizza l'immagine WordPress ufficiale. Dipende dal servizio MySQL (db) e imposta le variabili d'ambiente necessarie per la connessione al database MySQL.

# 2. Avvio dei container Docker

1. Dentro la cartella "project-cms" eseguire ```docker-compose up -d ```
 per avviare i container in background (dato dal comando -d).

# 3. Accesso al CMS WordPress

1. Quando i container sono in esecuzione, apri il tuo browser web.
2. Visita http://localhost:8080 per accedere al CMS WordPress.
3. Segui la procedura guidata di installazione di WordPress per configurare il tuo sito.

# Conclusioni
Hai completato con successo il deployment del CMS WordPress utilizzando Docker Compose. Ora puoi iniziare a creare e gestire il tuo sito web utilizzando WordPress.


