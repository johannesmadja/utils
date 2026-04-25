### Avoir l'addresse IP de l'hôte invité (Fedora)
````cmd
ip a
```` 
Regarger `enpOs3 > inet`

### Concernant le ssh
* vérifier l'état de démarrage
```cmd 
systemctl status sshd
```

* Démarrer 
```cmd 
systemctl start sshd
```

* Configurer une activation au démarrage 
```cmd 
systemctl enable sshd
```

### Changer d'utilisateur -> superuser 
```cmd 
sudo su -
```

### Arborescence des dossiers 
* **BIN** : Fichiers exécutables communs à tous les users comme les commanandes
* **BOOT** : Fichiers de démarrage 
* **DEV** : Fichiers des périphériques
* **ETC** : Fichiers de configurations (contient les fichiers de configuration des différentes applications installé sur le serveur/système)
* **HOME** : Répertoires personnels des users. Un dossier pas utilisateur crée dans le système
* **LIB** : Les librairies ou bibliothèques nécessaires aux programmes 
* **PROC** : Informations systèmes 
* **ROOT** : Dossier personnel du root
* **SBIN** : Les exécutables systèmes
* **TMP** : ficihiers temporaires 
* **VAR** : fichiers variables comme les logs

### Afficher les partitions du disque
```bash
df -h
```

### Préfixe des fichiers 
* **r** : fichier 
* **d** : Répertoire 
* **l** : lien symbolique 
* **c** : Fichier caratère (qui ne dure pas, pas sauvegarder)
* **b** : Fichier block (dont le contenu est sauvegarder)
* **s** : Socket

### Les liens symbolique vers un fichier 
* Créer  
```cmd 
ln -s [nom_du_fichier] [nom_du_lien]
```
* Supprimer
```cmd 
unlink [nom_du_lien]
```

### Pipe 
* Créer 
```bash
mkfifo [nom_du_pipe]
```

### Rechercher un fichier 
* find 
```cmd
find [emplacement] "[critère_de_recherche]"

Ex1 : find . -name "file1" (case sensible)
Ex2 : find . -iname "File1" (case insensible)
```

* Locate 
```cmd 
updatedb 
locate file
```
La première commande est pour mettre à jour la base de donnée du locate et la seconde pour faire la recherche

* grep
```cmd 
grep "warning" *
```
Trouve un ou plusieurs fichiers où se trouve l'occurence qu'on lui passe en paramètre  
Sors moi le/les fichiers où tu trouves le mot clé warning

* which 
```cmd 
which file1
```
Renvoie le chemin relatif où se trouve le fichier

### Les users et droits 
* Groupe \
Il existe trois groupes majeurs \
1- Root : l'utilisateur root \
2- Guess : pour les users \
3- System : pour les processus system

* Droits \
r : 4 \
w : 2 \
x : 1

* Commande \
1 - sudo : exécuter un commande nécessitant le droite administrateur \
2 - adduser / useradd : ajouter un utilisateur \
3 - addgroup / groupadd : ajouter un groupe \
4 - deluser / userdel : supprimer un utilisateur \
5 - delgroup / groupdel : supprimer un groupe \
6 - usermod : modifier les attributions d'un utilisateur \
7 - chgrp : modifier groupe \
8 - chown : modifier le propriétaire \
9 - chmod : attribuer des droits \
10 - passwd : changer le mot de passe \

```bash
usermod -g root ulrich 
```
Modifier le groupe d'un utilisateur

```bash 
chgrp root fichier
```
Changer le groupe d'appatenance d'un fichier 

```bash
chown root:ulrich fichier
```
Changer le owner et le groupe du fichier

```bash
chmod 777 fichier1
```
Donner tous les droits à tout le monde 

```bash
chmod a+x fichier1
```
Donner les droits d'exécution à tous 

### Editeur de texte 
* nano
```bash 
nano -miA fichier.txt
```
Pour activer la souris et la fonction d'indentation

```bash
/etc/nanorc
```
Contient le fichier le configuration global pour tous les users. Uniquement modifiable par le root

```bash 
home/user/.nanorc
```
Contient le fichier de configuration pour uniquement le user courant

* vi / vim
```cmd
    :syntax on/off
```
Activer la coloration syntaxique

```cmd
    :vsp/ :sp
```
Spliter l'écran en plusieur. On navigue avec ( ctrl + w ) x 2

```cmd
   :set mouse 
```
Activer la souris 

```cmd
   :set number 
```
Activer la numérotation des lignes

```cmd
   :!ls 
```
Faire un ls dans le directory

Pour copier, placer son cursor et taper `y` deux fois. Et pour coller, taper `p` \
u : supprimer dernière modifie (équivalent de ctrl + Z) \
ctrl + r : ramener la suppresion

```cmd
   :s/Jean/Paul 
```
Remplace Jean par Paul


### Les dépôts de packages 
* Debian (/etc/apt/sources.list)
* CentOS (/etc/yum.repos.d)

### Les commandes de filtrage
#### grep 

```cmd
grep -i "warn" syslog 
```
Rechercher en ignorant la casse 

```cmd
grep -n "warn" syslog
```
Afficher les numéro de lignes trouvées 

```cmd
grep -v "warn" syslog
```
Inverser la recherche. Les lignes qui ne contiennent pas "warn" dans le fichier syslog

```cmd
grep -r "warn" syslog
```
Recherche récursive dans les répertoires

```cmd
grep -E "[wW]arn" syslog
```
Utilisation des Regexp

```cmd
grep -ni "warn" syslog
```
Recherche insensible à la casse



#### cut

```cmd
cut -d: -f 1,5 syslog
```
L'option `-d` est le délimiter et l'option `-f` est pour spécifier les colonnes concernées

```cmd
cut -d: -c 1,5 syslog
```
L'option `-c` est pour désigner l'intervalle de caratère à afficher


### Les flux de redirection 
 `>` redirige la sortie dans un fichier et écrase s'il existe déjà 
 `>>` redirige à la fin d'un fichier et le créé s'il n'existe pas 
 `2>` redirige les erreurs dans un fichier (s'il existe déjà, il sera écrasé)
 `2>>` redirige les erreurs à la fin d'un fichier (s'il n'existe pas,il sera créé)
 `2>&1` redirige les erreurs au même endroit et de la même façon que la sortie standard
 `<` envoie le contenu d'un fichier à une commande 
 `<<` passe la console en mode saisie au clavier, ligne par ligne. Toutes ces lignes seront envoyées à la commande lorsque le mot clée de fin aura été écrit 
 `|` permet de chainer plusieurs commandes

 ```cmd 
 sort -n << STOP
 ```
 Fais moi le trie jusqu'à ce que tu tombes sur le mot-clé "STOP"

### Les Jobs et processus
`SystemV, upstart, SystemD` : Ce sont les gestionnaires de services/  daemon 
`&` : se met à la fin des commandes, le job s'arrête lorsque le user se déconnecte ou on ferme la console 
`nohup` : se met en début de commande, le job continue de tourner malgré l'arrête de la console
`ctrl + Z` : pour mettre en pause un programme et récupérer l'invite de commande 
`bg` : (background) pour que le processus continue à tourner en arrière plan 
`fg` : (foreground) reprendre un processus au premier plan. Ex : `fg%10`
`at` : exécuter une commande plus tard, en one shot 
`sleep` faire une pause
`crontab` : exécuter à une fréquence régulière 
`anacron` : similaire à crontab, idéal pour les machines qui ne tournent pas 24h/24. les commandes sont exécutées dès que le période est atteinte ou dépassé 
`Les timers systemd` : similaire à cron, à terme, remplacera probablement cron

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

