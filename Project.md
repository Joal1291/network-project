# NSA - You Shal Not Pass

## Virtual machines

Ils nous est demander de créer quatre machines.<br/> <br/>

### Machine Gateway

La machine gateway agira en tant que serveur DHCP sur un réseau privé. La machine attribuera des adresses IP à trois LAN distincts (administration, serveur, employé) avec des plages DHCP spécifiques. Les adresses IP des cartes internes seront statiques. L'objectif est d'établir une communication entre ces LANs tout en appliquant des filtres de paquets pour assurer la sécurité. Les règles de filtrage permettront l'accès spécifique aux serveurs et aux protocoles, tout en autorisant la sortie vers Internet et la récupération d'informations DHCP et DNS à partir de la passerelle. <br/>
Cette machine devras être sous `OpenBSD 7.4`. <br/>

### Machine Serveur

La machine serveur sous `FreeBSD 13` a pour objectif de fonctionner comme un serveur web robuste en hébergeant un site web NGINX avec prise en charge PHP7.4. La configuration inclut l'installation des modules nécessaires pour l'application, la vérification du port approprié, et le déploiement d'une page fournie.<br/>

En outre, la machine doit maintenir une adresse IP statique (192.168.42.70) tout en utilisant le protocole DHCP pour la configuration. La base de données MySQL 8.0 Server sera installée via le port système, avec déploiement de la base de données nsa501. Un utilisateur MySQL spécifique ("backend") sera créé, doté de tous les droits sur la table nsa501 et avec le mot de passe Bit8Q6a6G.<br/>

Le système sera configuré avec une adresse MAC spécifique pour une identification précise dans le réseau. Dans l'ensemble, la machine servira de plateforme robuste pour héberger un site web, gérer une base de données, et assurer la communication efficace avec d'autres parties du réseau.<br/>

### Deux machines clientes

Celles-ci peuvent être installées avec le système de notre choix et avec une interface graphique, la configuration réseau étant récupérée automatiquement via le protocole DHCP. 

## Créons nos machine.

### Clientes

Je commence par le plus facile en créant les deux machine cliente, sous distribution `Linux Mint`.<br/>
Leur allouer 1024mb de mémoire, 1CPU et 20G chacunes de disque dur dynamique.<br/>
Pour le moment je ne touche à rien je vais juste configurer le réseaus en `Accés par pont`. <br/>

![illustation](/img/clients/accéspont.png)

### Serveur web

Iso de `FreeBSD 14` disponible sur [Source ISO](https://download.freebsd.org/releases/amd64/amd64/ISO-IMAGES/14.0/).<br/>

Lançons nous dans l'instalation et la configuration. <br/>

Je la nomme `vm-server-FREEBSD`, je lui aloue 2048mb de mémoire, 2 CPUs et un disque dur dynamique de 16G. <br/>
Et je la configure aussi en accés par pont pour le moment.<br/>

Lançons la!<br/><br/>

![freebsd illustration](/img/server/freebsd.png)

Je fais une configuration par default. Et créer un utilisateur en plus du root.<br/><br/>
On y reviendra plus tard.

### Machines passerelle.

Iso de `OpenBSD 7.4` disponible sur [Source ISO](https://www.openbsd.org/faq/faq4.html#Download). <br/>

C'est parti pour une configuration!

Appelons-la `vm-dhcp-openbsd`, je lui alloue la meme chose que pour la vm serveur.<br/>
Et de même pour l'accés a internet. <br/>

On lance.<br/>

Pour la configuration je me lance un tuto trouver en ligne. [Tuto](https://www.youtube.com/watch?v=4MMr9mDD2cw&t=485s).<br/>
M'y connaissant pas dutout sur openbsd celui-ci ma était d'une grande aide.

Aprés quelque temps a essayer de résoudre un probleme à priori insolvable! J'ai décidr d'installer `openbsd7.2`.<br/>
En suivant exactement le même tuto j'ai pu faire une installation réussi de cette version.<br/><br/>
Maitenant que celui ci est installer avec succées on vas pouvoir commencer la configuration de cette machine qui vas gere le DHCP.

![openbsd](/img/gateway/Openbsd7.4.png)
















