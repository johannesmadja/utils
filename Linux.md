### CRONTAB 
Il existe deux `crontab`. 
- Crontab system : `crontab system` -> `cd etc/cron.d`
```log 
# Run the hourly jobs 
SHELL=/bin/bash 
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root 
01 * * * * root run-parts /etc/cron.hourly
```
---> Fréquence d'exécution - utilisateur pouvant exécuter - commande à exécuter

- Crontab utilisateur : `crontab -e` -> A taper en étant dans son espace utilisateur
```text 
*/2 * * * * echo TEST
```
---> Pas besoin de spécifier l'utilisateur 

### ARCHIVAGE 
```cmd
tar -cvf nom_de_l_archive.tar dossier_a_archirver
```
`-c` : créer une archive tar\
`-v` : afficher le détail des opérations (mode verbeux)\
`-f` : assembler l'archive dans un fichier

- Afficher le contenu de l'archive sans l'extraire 
```cmd
tar -tf mon_archive.tar
```

- Ajouter un fichier supplémentaire à une archive 
```cmd
tar -rvf mon_archive.tar archive_additionnelle
```

- Extraire les fichiers de l'archive 
```cmd
tar -xvf mon_archive.tar
```