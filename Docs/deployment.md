# Documentazione per il deployment

> [!WARNING]
> Per fare il deployment di questa branch hai bisogno di:
> - Docker
> - Docker Compose
>
> Se non hai questi programmi, scarica Docker Desktop sul tuo PC.

> [!NOTE]
> Questo branch utilizza i file .env.
> Se non vuoi utilizzare il file .env, elimina i file .env e modifica le voci environment su docker-compose nella directory Iac/project-cms
> ``` yaml
> ## ....
>
> services:
>   db:
>     image: mysql:8.3
>     restart: always
>     environment:
>       MYSQL_DATABASE: wordpress-cms
>       MYSQL_USER: wordpress-cms-user
>       MYSQL_PASSWORD: wordpress-cms-password
>       MYSQL_ROOT_PASSWORD: root-password
>
> ## ....
> ```

Una volta scaricato il codice, segui questi step:

### Step
#### 1. Crea un nuovo file .env  
``` bash
cp .env.local .env
```

#### 2. Fai il build del compose  
``` bash
docker compose build
```

#### 3. Fai partire il compose  
``` bash
docker compose up
```

### Comandi
#### Spegni il compose
``` bash
docker compose down
```


#### Visualizza tutti i container
``` bash
docker ps
```

