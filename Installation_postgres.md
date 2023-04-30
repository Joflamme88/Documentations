
## Pour désinstaller PostgreSQL sur Ubuntu sur Windows 11, vous pouvez exécuter les commandes suivantes dans votre terminal

1. Arrêtez le serveur PostgreSQL :

   ```
   sudo service postgresql stop
   ```

2. Supprimez PostgreSQL et ses fichiers de configuration :

   ```
   sudo apt-get --purge remove postgresql\*
   ```

3. Supprimez le dossier de données de PostgreSQL (ceci supprime toutes les bases de données et tous les fichiers associés) :

   ```
   sudo rm -rf /var/lib/postgresql/
   ```

4. Supprimez le groupe et l'utilisateur PostgreSQL :

   ```
   sudo groupdel postgres
   sudo userdel -r postgres
   ```

Une fois ces commandes exécutées, PostgreSQL sera complètement désinstallé de votre système.

## Pour désinstaller une version de Postgres sur Ubuntu, vous pouvez suivre les étapes suivantes

1. Ouvrir un terminal

2. Désinstaller le package correspondant à la version que vous souhaitez désinstaller. Par exemple, pour désinstaller Postgres 12 :

   ```
   sudo apt-get remove postgresql-<version>

   ```

   exemple:

    ```
    sudo apt-get remove postgresql-12
    ```

   3. Si vous souhaitez supprimer complètement les fichiers de configuration et les données, vous pouvez utiliser la commande suivante :

   ```

   sudo apt-get purge postgresql-<version>

   ```

Notez que si vous avez plusieurs versions de Postgres installées sur votre système, vous devrez répéter ces étapes pour chaque version que vous souhaitez désinstaller.

## Installation PostgreSQL : Commandes à exécuter pour installer la dernière version de PostgreSQL sur Ubuntu

1. Mettez à jour votre système Ubuntu :

```
sudo apt-get update
```

```
sudo apt-get upgrade
```

2. Installez le script PostgreSQL :
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
```
sudo apt-get update
```
```
sudo apt-get -y install postgresql
```

3. Vérifiez que PostgreSQL est en cours d'exécution :

```
sudo service postgresql status
```

Si PostgreSQL n'est pas en cours d'exécution, vous pouvez le démarrer avec la commande suivante :

```
sudo service postgresql start
```

4. Vérifiez la version de PostgreSQL installée :

```
psql --version
```

Cette commande affichera la version actuellement installée de PostgreSQL.

5. Pour redémarrer le server PSQL :

```
sudo service postgresql restart
```

Notez que ces commandes installeront la version la plus récente de PostgreSQL disponible dans les dépôts Ubuntu. Si vous souhaitez installer une version spécifique, vous pouvez ajouter le dépôt PostgreSQL correspondant et installer la version souhaitée en utilisant la commande d'installation ci-dessus.

## User : Modifier le mot de passe Postgres avant de changer la methode d'aithentification

   1. Vérifiez que PostgreSQL est en cours d'exécution :

   ```
   sudo service postgresql status
   ```

   2. Si PostgreSQL n'est pas en cours d'exécution, vous pouvez le démarrer avec la commande suivante :

   ```
   sudo service postgresql start
   ```

  3. Ouvrez une session en tant qu'utilisateur "postgres" en utilisant la commande suivante dans le terminal Ubuntu :

     ```
     sudo -i -u postgres psql
     ```

  4. Une fois connecté à la console PostgreSQL, tapez la commande ALTER ROLE suivie du nom du rôle et du nouveau mot de passe :

     ```
     ALTER ROLE postgres WITH PASSWORD 'nouveau_mot_de_passe';
     ```

     Remplacez "nouveau_mot_de_passe" par le nouveau mot de passe que vous souhaitez définir pour le rôle "postgres".
  5. Appuyez sur "Entrée" pour exécuter la commande. Vous devriez voir un message indiquant que la commande a été exécutée avec succès.
  6. Quittez la console PostgreSQL en tapant la commande "exit" ou en appuyant sur "Ctrl + D".



## Pour modifier le fichier `pg_hba.conf` "peer" vers "md5":

1. Ouvrez le terminal Ubuntu.

2. Accédez au répertoire contenant le fichier `pg_hba.conf` en utilisant la commande suivante :

```
cd /etc/postgresql/<version>/main/
```

Assurez-vous de remplacer `<version>` par le numéro de version de PostgreSQL que vous utilisez (par exemple, 15).

3. Ouvrez le fichier `pg_hba.conf` avec un éditeur de texte en utilisant la commande suivante :

```
sudo nano pg_hba.conf
```

4. Trouvez la ligne correspondant à la méthode d'authentification que vous souhaitez modifier (par exemple, "local all all peer"). Modifiez "peer" en "md5".

5. Enregistrez et fermez le fichier en utilisant les touches "CTRL+O" et "CTRL+X".

6. Redémarrez le serveur PostgreSQL en utilisant la commande suivante :

```
sudo service postgresql restart
```

Et voilà, vous avez modifié le fichier `pg_hba.conf` pour passer de l'authentification "peer" à l'authentification "md5". Les utilisateurs devront désormais fournir un mot de passe pour se connecter à PostgreSQL.



## PRG_URL : La syntaxe de l'URL de connexion à PostgreSQL est la suivante :

```
postgresql://<user>:<password>@<host>:<port>/<database_name>
```

Où :

- `<user>` : le nom d'utilisateur pour se connecter à la base de données
- `<password>` : le mot de passe de l'utilisateur (facultatif)
- `<host>` : l'adresse IP ou le nom d'hôte de la machine sur laquelle le serveur PostgreSQL est exécuté => mettre `127.0.0.1`
- `<port>` : le numéro de port sur lequel le serveur PostgreSQL écoute les connexions (vérifier le port dans le fichier `postgresql.conf`)
             (Verifier le PORT utilisé de postgres dans le fichier `/etc/postgresql/<version>/main/postgresql.conf`)
- `<database_name>` : le nom de la base de données à laquelle se connecter

Exemple d'URL de connexion à PostgreSQL :

```
postgresql://myuser:mypassword@127.0.0.1:5432/mydatabase
```
