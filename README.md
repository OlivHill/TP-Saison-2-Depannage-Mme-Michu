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

2. 
