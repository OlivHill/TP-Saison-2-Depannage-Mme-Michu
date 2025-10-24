# TP-Saison-2-Depannage-Mme-Michu

## Exposé du problème
Madame Michu m'adresse une demande :
"Bonjour, Mon ordinateur ne veut plus démarrer correctement, et quand j’arrive enfin sur le Bureau, mon processeur et ma RAM sont utilisés à 100% (elle est balaise, Mme Michu, pour le pré-diagnostic). En plus, j’ai remarqué que des fichiers dans mon dossier « Images » ont disparu ! Je suis inquiète pour l’état de mes disques durs aussi, il parait qu’ils sont défectueux, pourrais-tu les vérifier aussi ? Merci beaucoup de ton aide !"

Solutions envisagées :
- Démarrage impossible : déterminer la cause de la panne et 
- Faire un diagnostique RAM et Processeur.
- Récupérer les fichiers du fichier Images
- Disques dur: Faire un test de performance CrystalDiskMark puis conseiller la cliente selon l'état de santé constaté


## Résolution

### Démarrage de l'ordinateur

Au démarrage de l'ordinateur, le message suivant apparaît :

<img width="1087" height="589" alt="image" src="https://github.com/user-attachments/assets/9c9b847c-eb49-46e5-8e3a-087cc5067729" />

"An operating system wasn't found. Try disconnecting any drives that don't contain an operating system. Press Ctrl+Alt+Del to restart" apparaît. Il signale que le BIOS/UEFI n’a pas trouvé de système bootable sur les périphériques connectés. Les causes peuvent être les suivantes:
- Ordre de démarrage incorrect dans le BIOS
- Disque système déconnecté ou non reconnu (Câble SATA/USB mal branché, SSD/HDD défectueux, ou port non alimenté).
- Partition système absente ou corrompue (suppression accidentelle, formatage, ou erreur de partitionnement).
- Installation incomplète ou ratée de l’OS

Physiquement, rien n'est signalé dans l'énoncé, je penche donc pour un  problème logiciel.

J'accède au boot devise par F12 au démarrage :
<img width="881" height="588" alt="image" src="https://github.com/user-attachments/assets/9598675f-52b7-4540-9ef4-f3f425187369" />

Je charge un ISO de Windows 10 et je boote depuis le lecteur CD-Rom pour accéder au BootMGR, le gestionnaire de démarrage de Windows de l'environnement Windows RE :
Je clique sur Réparer l'ordinateur et j'accède aux options de dépannage
<img width="1550" height="1042" alt="image" src="https://github.com/user-attachments/assets/4c9fd309-a644-4da8-9d67-19f417d1e0c8" />

1. Je tente la réparation automatique :
<img width="1519" height="950" alt="image" src="https://github.com/user-attachments/assets/ae1252e7-a2b7-4d3a-8a72-8bc517ebb73e" />

<img width="1528" height="949" alt="image" src="https://github.com/user-attachments/assets/50315ac8-fc16-4b0c-af81-7ac295877c0f" />

<img width="1512" height="938" alt="image" src="https://github.com/user-attachments/assets/fbd7d75f-5bd3-4e8a-8048-20604fab40bf" />


Résultat : échec
<img width="1535" height="956" alt="image" src="https://github.com/user-attachments/assets/d10b8549-20ab-4235-890d-04dc8f13fe6d" />

2. Commande Bootrec

<img width="1486" height="937" alt="image" src="https://github.com/user-attachments/assets/63e38742-634b-4846-b66d-bea4e6f09b52" />

Les commandes BootRec possibles sont les suivantes :
<img width="1491" height="1311" alt="image" src="https://github.com/user-attachments/assets/e72577f6-02ef-45c7-b42f-a387fb431a4c" />

En l'espèce, l'erreur étant de type "BootMGR is missing", je tente les commandes:
- ````bootrec \fixmbr````
- ````bootrec \fixboot```` : accès refusé. Je force alors par la commande ````bootsect /nt60 sys````
- ````bootrec \rebuildbcd````

J'effectue l'opération autant sur la partition X: que sur la partition E: (là où se situe Windows)

<img width="999" height="530" alt="image" src="https://github.com/user-attachments/assets/d09dc79c-a5e1-4982-9585-a3b153164190" />


Au redémarrage, il y a du mieux, j'accède à un écran bleu : le winload.exe est corrompu.


<img width="1920" height="1032" alt="VirtualBoxVM_8BeA3YDe7n" src="https://github.com/user-attachments/assets/411a66b5-31c9-4311-93e0-baa9731c00ac" />


L'outil de remarrage systeme auto permet de restaurer Winload.exe et d'accéder à Windows.



### Système ralenti:

En gestionaire des tâches, de nombreux processus tournent en arrière plan
<img width="1920" height="1032" alt="VirtualBoxVM_2N1flUz6Q0" src="https://github.com/user-attachments/assets/c33f828c-93b0-4236-99a0-0d6ae3e4a7fc" />

Je constate qu'au démarrage un script "Ping" se lance.

Via exécuter je lance shell:startup

Un raccourci appraît et pointe sur le fichier "ping.ps1"; Je le supprime.
<img width="1920" height="1032" alt="VirtualBoxVM_T3bE54JfxV" src="https://github.com/user-attachments/assets/8089dfef-9a35-430e-a9cc-6d0e5f6ce885" />

<img width="1920" height="1032" alt="VirtualBoxVM_inHF22raVl" src="https://github.com/user-attachments/assets/33968db7-0516-4b70-b005-4d1db0fc58e2" />

L'utilisation du processeur et de la RAM est à présent normal :
<img width="1920" height="1032" alt="VirtualBoxVM_wvyHWprdmx" src="https://github.com/user-attachments/assets/75a03a14-593b-4cf4-8fc1-a6a2484cce92" />


 ### Recuperation des images :

Réactiver le disque E qui apparaît hors ligne en gesiton des disques.

<img width="1920" height="1032" alt="VirtualBoxVM_xqzqrwQxVd" src="https://github.com/user-attachments/assets/9e15c1fa-43ab-40b2-9d6e-2f58ba762120" />

<img width="1920" height="1032" alt="VirtualBoxVM_5aXTzkzIks" src="https://github.com/user-attachments/assets/b2215948-35c7-4680-8806-08648a5bdc85" />

le disque E est à présent actif :
<img width="1920" height="1032" alt="VirtualBoxVM_jSOPGcwmFi" src="https://github.com/user-attachments/assets/7d7c2bee-a46e-41be-9a51-6ea8b9a950cf" />

Le dossier image est historisé

<img width="1920" height="1032" alt="VirtualBoxVM_jQ0s7rQ6Op" src="https://github.com/user-attachments/assets/f880bb01-fe23-4413-8902-5a42f27bc702" />

Une fois la restauration effectué, le dossier York apparaît.

<img width="1920" height="1032" alt="VirtualBoxVM_xoXVRgbrGI" src="https://github.com/user-attachments/assets/14d1c6fe-3dfc-4a6a-97e6-e090d8f8ca90" />

# CORRECTION
La VM est un Win10, sur une structure BIOS.
Le message est un message de BIOS.

<img width="1087" height="589" alt="image" src="https://github.com/user-attachments/assets/9c9b847c-eb49-46e5-8e3a-087cc5067729" />

C'est un problème lié à la distribution. Le BIOS initialise les périphériques, des drivers et va chercher dans un endroit s'il y a un operating système (OS)...et il ne trouve rien. Donc soit il n'y a rien, soit il cherche au mauvais endroit.

Pour le démarrage, il y a trois étapes:
- le bootmgr :
  - Il charge le système d’exploitation (comme Windows 10 ou 11) au démarrage de l’ordinateur.
  - Il lit les fichiers de démarrage (comme BCD, le Boot Configuration Data) pour savoir où se trouve Windows et comment le lancer.
  - Généralement, il se trouve sur la partition système réservée ou sur la partition EFI si ton PC utilise le mode UEFI.
  - En cas d'erreur BOOTMGR absent ou corrompu, Windows ne démarre pas. On peut réparer avec un support d’installation (clé USB ou DVD) en utilisant des commandes comme ````bootrec /fixboot````, ````bootrec /rebuildbcd````, ou ````bcdboot````

- le winload
  - 
- le bcd

Ici, on considère que c'est un problème de Boot is Missing. 

On intègre un ISO Win10 ou Win11 pour accéder aux lignes de commande.

Aller en ligne de commande et taper ````notepad````. une fois notepad ouvert, faire Fichier Ouvrir et ça nous donne accès à une interface !!! (on peut faire aussi ````regedit````, etc)

<img width="1920" height="1032" alt="VirtualBoxVM_ywJcZnsQOp" src="https://github.com/user-attachments/assets/4b86f60d-4d96-42bd-ba80-f31805fbddf8" />

Le lecteur Boot (X:) c'est quoi ? Actuellement on est sur le CD-ROM, le système qui tourne est sur le WinRE de ce CDROM.

On peut aller voir les lecteurs :

<img width="1920" height="1032" alt="VirtualBoxVM_dm00F8CCP7" src="https://github.com/user-attachments/assets/30327dcd-a59c-4c2f-bded-74321f0e8a52" />

Dans le lecteur E:, on trouve l'utilisateur Mme Michu, c'est donc l'ordinateur de Mme MICHU. C'est donc sur ce lecteur que se situe les données de Mme.

<img width="1920" height="1032" alt="VirtualBoxVM_VF3748iWBW" src="https://github.com/user-attachments/assets/9268246a-41c9-4d4b-b5b6-dd27d3be703d" />

Le lecteur C: est indiqué "Réservé au système". C'est donc le Windows.

<img width="1920" height="1032" alt="VirtualBoxVM_H91T6m2CZD" src="https://github.com/user-attachments/assets/d623de61-a0bc-4548-b972-d2cce3e8e9b0" />

