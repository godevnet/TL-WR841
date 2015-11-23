# TL-WR841

## Pages officielles

* http://www.tp-link.com/lk/products/details/?model=TL-WR841ND#spec
* http://wiki.openwrt.org/toh/tp-link/tl-wr841nd
* http://www.amazon.fr/dp/B0019EQ1RW/ref=wl_it_dp_o_pC_S_ttl?_encoding=UTF8&colid=3U2BD7X6Y9Y31&coliid=I2SCI8P495BZJX

## Matériel nécessaire
* une station de travail
* une connexion Internet
* un routeur TL-841ND v9.0
* le firmware correpsondant


## Mise à jour vers OpenWRT

Remplacer le firmware TP-Link original par celui d’OpenWRT (version Trunk) et réaliser une configuration minimale. L’activité peut prendre 30 minutes. L’intérêt est de manipuler le matériel réseau avec un OS ouvert, évolutif, stable et facile à prendre en main.

### Procédure

#### Etape 1
* Vérifier la version Hardware au verso du matériel.
* Se procurer le Firmware (Version Trunk pour TL-841ND v9.0) à l’adresse suivante
http://downloads.openwrt.org/snapshots/trunk/ar71xx/openwrt-ar71xx-generic-tl-wr841n-v9-squashfs-factory.bin
* Se procurer le Firmware (Version Trunk pour TL-841ND v8.2)
http://downloads.openwrt.org/snapshots/trunk/ar71xx/openwrt-ar71xx-generic-tl-wr841n-v8-squashfs-factory.bin

#### Etape 2

* Connectique : connexion de la station de travail à un port LAN (jaune) et l’Internet sur le port WAN (bleu). 
* Allumer le routeur. 
* Le routeur offrira par défaut des adresses IP dans la plage 192.168.0.0/24 sur son interface LAN.

#### Etape 3

* Mise à jour du firmware. Le routeur est accessible par défaut en HTTP sur l’adresse 192.168.0.1.
* Ouvrir un navigateur Web et se rendre à l’adresse http://192.168.0.1/  (admin:admin)
* Aller dans le menu System Tools/Firmware Upgrade, choisir le fichier du firmware et appuyer sur le bouton “Upgrade”.
* Patienter plusieurs minutes le temps du redémarrage.

#### Etape 4

Après la mise à jour, le routeur dispose d’une nouvelle adresse IPv4 en 192.168.1.1. L’adresse de la station de travail a changé également de manière dynamique. 

Pour installer l’interface graphique.

* A partir de la station de travail, se connecter avec le logiciel putty en Telnet sur l’adresse du routeur 192.168.1.1
* Mettre à jour la liste des paquetages : `opkg update`
* Installer l’interface Web graphique : `opkg install luci`
* Lancer le serveur Web à chaque redémarrage : `/etc/init.d/uhttpd enable`
* Démarrer le serveur Web : `/etc/init.d/uhttpd start`

#### Etape 5

* Configuration minimale à réaliser.
* Définition du mot de passe : ********
* Configuration du Hostname : LAB-AABBCC où “AABBCC” sont les 24 derniers bits d’une des interfaces du routeur (voir verso du routeur) ou via commande ifconfig eth1.
* Activation NTP client.

## B. Mise à jour à partir d’un OpenWRT déjà installé.

* Choisir une version “Sysupgrade” du firmware, pour la version hardware 8.2 : http://downloads.openwrt.org/snapshots/trunk/ar71xx/openwrt-ar71xx-generic-tl-wr841n-v8-squashfs-sysupgrade.bin
* Réaliser la mise à jour System/Backup via le menu.

## C. Mode sans échec

* http://wiki.openwrt.org/fr/doc/howto/generic.failsafe
