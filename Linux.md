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

- Ajouter un fichier supplémentaire à une archive existante
```cmd
tar -rvf mon_archive.tar archive_additionnelle
```

- Extraire les fichiers de l'archive 
```cmd
tar -xvf mon_archive.tar
```

### COMPRESSION / DECOMPRESSION 
* Compression 
```cmd 
gzip -k mon_archive.tar
```

```cmd 
bzip2 -k mon_archive.tar
```

* Décompression 
```cmd 
gunzip -k mon_archive.tar
```

```cmd 
bunzip2 -k mon_archive.tar
```


### ARCHIVAGE - COMPRESSION 
* gzip 
```cmd 
tar -zcvf mon_archive.tar.gz mon_dossier_a_archiver/
```

* bzip2
```cmd 
tar -jcvf mon_archive.tar.bz2 mon_dossier_a_archiver/
```

### DEARCHIVAGE - DECOMPRESSION 

* gzip
```cmd 
tar -zxvf mon_archive.tar.gz 
```

* bzip2
```cmd 
tar -jxvf mon_archive.tar.bz2 mon_dossier_a_archiver/
```


### Ajouter un user à un group 
```cmd
sudo usermod -aG nom_du_groupe nom_utilisateur
```


### CONFIGURATION DE L'IP
* IP, masque réseau, gateway et routes réseaux\
1 - Debian `/etc/network/interfaces`\
2 - Redhat `/etc/NetworkManager/system-connections/` <-- mise à jour

* Dns : `/etc/resolv.conf` 
```txt
IMPORTANT : 
Toutes modifications du serveur DNS devra se faire via le NetworkManager accessible via `nmtui`
```
* Résolution dns interne au serveur : `/etc/hosts`
* Hostname de la machine : `/etc/hostname`

Deux outils pour gérer les configuration 
* nmtui : NetworkManager Text Ui
```cmd 
sudo dnf install NetworkManager-tui
sudo nmtui
```
* nmcli 
```
nmcli connection show

sudo nmcli con mod eth0 ipv4.addresses 192.168.1.50/24 ipv4.method manual
sudo nmcli con up eth0
```

1. L'Interface Réseau (La "Porte")
Une interface réseau est la représentation logicielle d'un port physique (ta carte Ethernet) ou virtuel.

Le nommage : Tu verras souvent des noms comme ``eth0``, ``ens33``, ou ``wlp2s0``.

``eth`` ou ``ens`` : Indique généralement une connexion filaire (Ethernet).

``wlp`` ou ``wlan`` : Indique souvent une connexion Wi-Fi.

``lo`` (Loopback) : C'est une interface spéciale. Elle représente ton ordinateur qui parle à lui-même. C'est indispensable pour que le système fonctionne (par exemple, pour qu'une base de données locale écoute les requêtes internes).

2. L'IP, le Masque et la Passerelle (L'adresse et la sortie)
C'est le "triptyque" indispensable pour qu'une machine communique au-delà de son propre réseau local.

L'Adresse IP (Ex: 192.168.1.10) : C'est l'identité unique de ta machine sur le réseau.

Le Masque de sous-réseau (Netmask) : Il définit la taille du "quartier". Il permet à ton ordinateur de savoir quelles machines sont "à côté" (accessibles directement) et quelles machines sont "au loin" (nécessitant de passer par un routeur).

La Passerelle (Gateway / Default Route) : C'est ton "pont de sortie". Si ton ordinateur veut envoyer un paquet vers Internet (Google.com), il ne sait pas où c'est. Il le donne donc à la Passerelle (généralement ton routeur/box internet), qui se chargera de le transmettre plus loin.

3. Les outils pour "voir" tout ça
Oublie les vieux outils comme ifconfig (qui ne sont plus installés par défaut). Aujourd'hui, on utilise la suite iproute2. C'est le standard universel sur Linux.

Voici les trois commandes que tout administrateur système connaît par cœur :

``ip addr`` : (ou ``ip a``)

Utilité : Elle te montre toutes tes interfaces et leurs adresses IP actuelles. C'est l'équivalent du "qui suis-je ?" réseau.

``ip route`` :

Utilité : Elle te montre la "table de routage". C'est là que tu verras quelle est ta passerelle par défaut (elle est marquée par le mot-clé default via).

``ip link`` :

Utilité : Elle te montre l'état physique de tes "portes" (si le câble est branché, si l'interface est "UP" ou "DOWN").

4. Le flux logique d'une requête
Quand tu tapes ping google.com dans ton terminal :

Ton PC regarde dans le fichier /etc/resolv.conf pour trouver l'adresse DNS.

Il demande au serveur DNS : "Quelle est l'IP de google.com ?".

Une fois l'IP obtenue, il vérifie sa "table de routage" (ip route).

Si l'adresse est en dehors de ton réseau local, il envoie le paquet à la Passerelle via ton Interface réseau.


### Transfert de donnée via le réseau 
* wget : http, https et stp 
```cmd
wget http://machine_cible/ressource_a_telecharger
wget https://machine_cible/ressource_a_telecharger -O nom_de_renommage_du_fichier_telecharger
```
Il sera utilisé principalement pour les téléchargements de fichier

* curl : http(s), ftp(s), imap(s), ldap(s), smtp(s)
```cmd
curl https://machine_cible/archive.tar --output nom_de_renommage_du_fichier_telecharger
```
Il supporte la plupart des protocoles de transfert de data 

* scp :
> Télécharger
```cmd
scp user@ip_ou_hostname_distant:/chemin/vers/le/fichier/distant /chemin/vers/la/copie_locale
```

> Uploader 
```cmd
scp /chemin/vers/le/fichier_local user@ip_ou_hostname_distant:/chemin/vers/la/copie_distante
```
Tranfert de data via ssh 

* winscp : scp 
```cmd

```
C'est un client graphique pour faire du scp 

* ftp : 
```cmd

```
Transfert avec un serveur ftp. Utilise les ports 20 (data) et 21 (commandes) 

* sftp
```cmd
   sftp user@hostname
   cd change_directory
   ls
   get nom_du_fichier_a_telecharger <-- Télécharger un fichier
   pwd                              <-- afficher le répertoire courant
   put nom_du_fichier_a_uploader    <-- uploader un fichier
   rm                               <-- suppression de fichier
   bye, exit, quit                  <-- Déconnexion
```
Simulé du ftp en utilisant du ssh. Utilise le port 22 (data)

* rsync : 
> synchro local
```cmd
   rsync -arv dossier_source/ dossier_destination/

   a : conservie les métadata du fichier (droits, user, groupe etc...)
   r : synchro récursive sur les sous répertoires 
   v : mode verbeux 
```
> synchro distant
```cmd
   rsync -arv dossier_source/ user@IP_du_serveur:dossier_destination:
```

Pour faire de la synchronisation de fichier


### Analyse du traffic
Les commandes `host` et ``nslookUp`` permettent de requêter le dns pour avoir l'équivalent ip d'un nom de machine ou inversement 

* ``netstat`` : permet d'analyser le flux réseaux 
* `netstat -i` : afficher les stats des interfaces réseau
* `netstat -uta` : lister toutes les connexions ouvertes 
* `netstat -lt` : liste des connexions en état d'écoute 
* `netstat -s` : statistiques résumés

```cmd 
-p : afficher le nom et les pid des processus 
-i : affiche la table de toutes les interfaces réseau 
-u : affiche les connexions udp 
-t : affiche les connexions tcp 
-a : affiche les toutes les connexions quel que soit leur état 
-l : affiche les connexions en écoute
-s : affiche un résumé
-n : affiche les numéros de port
```

Le filtrage des flux se fera au moyen de `iptables`
```cmd
iptables -A(chain) -p(protocole) --dport(port) -j(décision)

chaine : INPUT/OUTPUT/FORWARD
protocole : tcp / udp / icmp / smtp / ldap 
port : le port à configurer (22, 80, 8080)
décision : ACCEPT / REJECT / DROP 
```

Pour accepter les connexions déjà établis 
```cmd
iptables -A INPUT -m state --state ESTALISHED, RELATED -j ACCEPT
```

Supprimer la politique par défaut sur les inputs 
```cmd
iptables -P INPUT DROP
```

Rétabli la politique par défaut 
```cmd
iptables -P INPUT ACCEPT
```

# Comprendre iptables simplement

## 🧠 L’idée générale

iptables est un système de pare-feu sous Linux.

👉 Il inspecte chaque paquet réseau et décide quoi faire :
- accepter
- bloquer
- rediriger

---

## 🧩 Les 3 concepts fondamentaux

### 1️⃣ Table = le type de traitement

👉 Question : *“je veux faire quoi globalement ?”*

| Table   | Rôle                |
|---------|---------------------|
| filter  | Autoriser / bloquer |
| nat     | Rediriger           |
| mangle  | Modifier            |

👉 Pense : **le service utilisé**

---

### 2️⃣ Chaîne (chain) = le moment du contrôle

👉 Question : *“à quel moment j’interviens ?”*

| Chaîne       | Moment |
|-------------|--------|
| INPUT        | Le paquet arrive vers la machine |
| OUTPUT       | Le paquet sort |
| FORWARD      | Le paquet traverse la machine |
| PREROUTING   | Avant routage |
| POSTROUTING  | Après routage |

👉 Pense : **le checkpoint**

---

### 3️⃣ Règle (rule) = condition + action

👉 Question : *“si ça correspond, je fais quoi ?”*

Exemple :

```bash
-p tcp --dport 80 -j ACCEPT
```

👉 Traduction :

Si paquet TCP vers port 80 → j’accepte


# Les options iptables expliquées simplement

## 🧠 Structure d’une commande

```bash
iptables [OPTIONS] [CHAÎNE] [CONDITIONS] -j [ACTION]
```
Exemple :

iptables -A INPUT -p tcp --dport 80 -j ACCEPT\

**-A (Append)**
```bash
iptables -A INPUT ...
```
Ajouter une règle à la fin d’une chaîne

**-I (Insert)**
```bash
iptables -I INPUT 1 ...
```
Insérer une règle au début (ou position donnée)


**-D (Delete)**
```bash
iptables -D INPUT ...
```
Supprimer une règle

**-L (List)**
```bash
iptables -L
```
Lister les règles


**-t (table)**
```bash
iptables -t nat ...
```
Choisir la table


🌐 2. Conditions réseau\
> -p (protocol)

👉 Protocole réseau

```bash
-p tcp
-p udp
-p icmp
```

➤ --dport (destination port)

👉 Port destination

--dport 80

⚠️ fonctionne avec -p tcp ou udp

➤ --sport (source port)

👉 Port source

--sport 443
➤ -s (source)

👉 Adresse IP source

-s 192.168.1.10

ou réseau :

-s 192.168.1.0/24
➤ -d (destination)

👉 Adresse IP destination

-d 10.0.0.5
🧩 3. Le fameux -m (match module)

👉 -m = charger un module de conditions avancées

➤ Exemple avec state
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

👉 Traduction :

accepter les connexions déjà établies

➤ Exemple avec conntrack (moderne)
iptables -A INPUT -m conntrack --ctstate NEW -j ACCEPT
➤ Exemple avec multiport
iptables -A INPUT -p tcp -m multiport --dports 80,443 -j ACCEPT

👉 ouvre plusieurs ports en une règle

🎯 4. L’action (-j)

👉 -j = "jump" → quoi faire si ça match

➤ ACCEPT
``-j ACCEPT``

✔ autoriser

➤ DROP
``-j DROP``

✔ bloquer silencieusement

➤ REJECT
``-j REJECT``

✔ bloquer avec réponse (erreur)

➤ DNAT (NAT)
``-j DNAT --to 172.17.0.2:80``

✔ rediriger vers autre IP

➤ SNAT
``-j SNAT --to-source 1.2.3.4``

✔ modifier IP source

🧠 Exemple complet expliqué
```bash
iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to 172.17.0.2:80
```

Traduction :
|Partie	     |Signification|
|-------------|--------|
|-t nat	     |table NAT|
|-A PREROUTING	|avant routage|
|-p tcp	     |protocole TCP|
|--dport 8080	|port 8080|
|-j DNAT	     |redirection|
|--to ...	 |vers conteneur|



🏁 Résumé rapide
|Option	|Rôle|
|-------------|--------|
|-A	|ajouter règle
|-I	|insérer règle
|-p	|protocole
|-s / -d	|IP source / destination
|--dport	|port destination
|-m	|module avancé
|-j	|action


### Connaitre le package installé 
 ```cmd
 which netstat 
 rpm -qf /usr/bin/netstat
 ```

 ### Les Disques Dur
 * 4 partitions principales à cause des 4 descripteurs de fichier MBR. Elles acceptent tout type de FS (file system)
 * Des partitions Etendues ou secondaire qui ont besoin d'une partition principale
 * Une partition active : celle qui contient le système d'exploitation

 > Les partitions 
* la première lettre indique si le disque est d type `IDE` ou `SCSI` (Il s'agit du type de connexion à la carte mère) : 
 1- IDE         -----------> Lettre H
 2- SCSI(S-ATA ou USB)  ---> Lettre S

* Le seconde lettre est mise pour le disque : `D`
* La troisième représente les différents disque dur connecté au système. On peut en avoir plusieurs connecté de manière physique :
   1- Premier disque dur (HDA) 
   2- Premier disque dur (HDB) 
   3- Premier disque dur (HDC)

Lorsqu'on crééra des partitions, on ajoutera des chiffres représentant les partitions : HDA1, HDA2, HDA3 

* Lister les disques disponible sur l'OS 
```bash 
fdisk -l
``` 

* Créer une partition 
```bash
fdisk /dev/sdb
```

* Next step : 
- Formater les disk `mkfs -t ext4 /dev/sdb1`
- Créer des points de montage : `mkdir -p /mnt/partition1 /mnt/partition2`
- Monter les partitioins : ``mount -t ext4 /dev/sdb1 /mnt/partition1` 
Note : Pour un montage permanent aller dans `/etc/fstab`

### Surveillance des ressources physique du OS 
* Utilisation de la mémoire RAM : 
```bash
free 
free -m 
free -g => valeur en giga
free -ht 
```

* Utilisation du disque : 
```bash
df 
df -h 
df -H
df -m
```

* Le swap 
```bash
cat /proc/swaps
free 
swapon -s
```

* La taille d'un répertoire et son contenu
```bash
du 
du -h
du -m 
du -ks
```

* infos sur le CPU 
```bash
lscpu
cat /proc/cpuinfo
```

* Les interfaces réseau 
```bash
ip a 
ifconfig 
ethtool (package à installer)
```

* Connaitre le type de OS 
```bash
cat /etc/os-release
```

* connaitre l'état des disque 
```bash
fdisk -l
```

* Données sur le temps et la durée d'activité de l'os 
```bash
w
uptime 
who 
date
```

* Afficher les métrique en temps réel 
```bash
top
```

* Avoir plus d'infos que `top` et possède des fichiers journaux (package à installer)
```bash
atop
```

* Analyser les sockets, similaire à `netstat`
```bash
ss 
```

* Afficher les processus en cours 
```bash
ps -ejH
ps -ef
``` 

### Demon SYSTEMD
Remplaçant du `INIT SYSTEM V`. Son rôle est de démarrer tous les autres services de notre serveur

* Les répertoires concernés : 
```bash
/lib/systemd/system
/usr/lib/systemd/system

/etc/systemd/system => pour les configs personnels
```

* Commande pour manipuler les systèmes 
```bash
systemctl <action> <nom_du_service>.service
```

* Démarrer un service 
```bash
systemctl start application.service
```

* Arrêter un service 
```bash
systemctl stop application.service
```

* Redémarrer un service lancé 
```bash
systemctl restart application.service
```

* Recharger les fichiers de configuration d'un service 
```bash
systemctl reload application.service
```

* Lancer un service au démarrage du système 
```bash
systemctl enable application.service
```

* Ne pas lancer un service au démarrage du système 
```bash
systemctl disable application.service
```

* Empêcher l'activation d'un service 
```bash
systemctl mask application.service
```

* Envoyer un signal d'arrêt à tous les processus du service 
```bash
systemctl kill application.service
```

> Avoir les information sur un status 

* Vérifier si le service est démarré ou arrêter
```bash
systemctl status application.service
```

* Voir si le système est actuellement démarrer 
```bash
systemctl is-active application.service
```

* Vérifier si le système sera up au démarrage du système 
```bash
systemctl is-enable application.service
```

* Vérifier s'il y a eu des problème au moment du démarrage 
```bash
systemctl is-failed application.service
```

* Voir tous les services qui ont un problème 
```bash
systemctl --failed -- type=service
```

### Les expression régulières 
* Intervelle 
`[a-d]` : de a - d\
`[ab]` : a ou b\
`[^0-9]` : sans chiffre numérique\

* Ancrage
`^` : Début de ligne\
`$` : Fin de ligne\
`\<` : Début de mot (pour chaque mot de la phrase)\
`\>` : Fin de mot (pour chaque mot de la phrase)\

### sed (Stream editor)
```bash
sed [-n] action [fichier1]
sed [-n] -e action1 [-e action2] [fichier1]
```

### Awk (Aho Weinberger et Kernigan)
```txt
BEGIN 
> section optionnelle 
> traitement avant lecture des données 

COUPLE motif/action
> Traitement des données lues 
> Pour chaque motif correspondant, l'action adéquate est appliquée 

END  
> section optionnelle 
> traitement après lecture des données
```

* Exemple de motifs 
```txt
par comparaison : 
$1 >= 8 {print}

par calcul : 
$2 * $3 > 10 {print $2 + $3} 

par texte : 
$1 == "root"
$1 ~ /^[0-9].*[a-z]$/
$2/^[a-z]/ && $3!~/^[0-9]/
```

* Les variables 
- NF : nombre de champs dans la ligne courante 
- NR : nombre de ligne lues jusque alors 
- $0 : la ligne complète 
- $n le champ n 
- $NF : le dernier champ de la ligne courante 
- FS : Séparateur de champs (espace ou TAB par défaut)
- OFS : Séparateur de champs de sortie

```cmd
awk 'programme' fichier 

awk 'programme'

awk -f programme fichier

awk [-F sep] [-v var=val] fichier
```