:::success
**TP1_B2_LINUX** 

:::
:::info
**Connexion SSH**
ssh root@192.168.1.11

et 

ssh root@192.168.1.12

résultat:   **root@node2 
            root@node1**
:::

:::info
Après configuration du nom des réseaux des 2 machines grâce aux commandes:

nano /etc/hostname

*modification du fichier*

vérification avec la commande *hostname*

résultat de la commande: 

**node1.tp1.b2**

(Et vice-versa)

**node2 ping node1 par son nom**
cmd: **ping node1.tp1.b2**
:::

:::info
***node1 ping node2 par son nom***
cmd: **ping node2.tp1.B2**
:::

:::info
Partition des VM:

**Volume physique:** pvcreate /dev/sdb

**Volume Groupe:** vgcreate data /dev/sdb

**Logical Volumes:** lvcreate -L 2G data **et** lvcreate -l +100%FREE data

**Dossiers pour le montage:** mkdir /srv/site1 /srv/site2

**Formatage des partitions:** mkfs.ext4 /dev/data/lvol0 **et** mkfs.ext4 /dev/data/lvol1

**Montage des partitions:** mount /dev/data/lvol0 /srv/site1 **et** mount /dev/data/lvol1 /srv/site2

**Mount auto au démarrage:** nano /etc/fstab ->  **ajout des lignes**: /dev/data/lvol0 /srv/site1 ext4 defaults 0 0 **et** /dev/data/lvol1 /srv/site2 ext4 defaults 0 0 dans /etc/fstab
 
**Check:** mount -av 
**Résultat:**

/                : ignored
/boot            : already mounted
swap             : ignored
/srv/site1       : already mounted
/srv/site2       : already mounted


:::

:::info
***Configuration du firewall afin de bloquer toutes les connexions***


Info firewall: **man firewall-cmd**

Cmd nécéssaire: **firewall-cmd --set-default-zone block** -> bloque les connexions.

Puis: **firewall-cmd --reload** -> relance le firewall pour enregistrer les modifications et les vérifier par la suite.

Vérification: **firewall-cmd --list-all**

Résultat: ***block (active)***

Tentative de ping de **node1** vers **node2**: 
Aucun ping reçu par node2

Tentative de ping de **node2** vers **node1**: ping réussi
:::


:::info
***Installation de NGINX après récupération de epel-release***
Réussie. sur node1
:::

:::info
**Ajout d'un sudo user car j'ai oublié lol**
cmd: **sudo visudo** puis modification du fichier etc/sudoers.d en rajoutant: 

**node1    ALL=(ALL)    ALL**
:::

:::info
Setup du serveur NGINX: 
Création des dossiers **site1** et **site2**
    **mkdir site1**
    
Création des fichiers index.html
    **touch index.html**
    
Difficultés rencontrées lors du paramétrage du serveur NGINX demandé dans l'exercice.
    
