---
title: "Let's encrypt"
layout: post
date: "2015-12-12 22:22"
comments: true
tags: 
  - ssl
  - letsencrypt
categories: admin
---

Avoir un site HTTP, c'est has been. Maintenant, il faut que tout soit en HTTPS. Oui, mais voilà, jusqu'à récemment, c'était payant ! Heureusement, avec [Let's Encrypt](https://letsencrypt.org/), c'est maintenant possible d'avoir un certificat SSL gratuitement.

J'ai reçu mon mail d'acceptation à l'open beta il n'y a pas si longtemps, et du coup, j'en profite pour passer mes sites persos en HTTPS.

Pour rappel, je suis sur `Ubuntu 15.10`, j'utilise `nginx` comme serveur web et j'ai déjà `git` d'installé.

## Installation

Il faut simplement récupérer le dépôt par git :

```bash
cd /opt
sudo git clone https://github.com/letsencrypt/letsencrypt.git
cd letsencrypt
./letsencrypt-auto --help
```

Cette dernière commande va lancer `letsencrypt` pour qu'il gère ses dépendances et affichera l'aide


## Configuration

Dans un fichier de configuration (exemple : `/etc/letsencrypt/cfg.ini` )

```ini
# Rallonge la longueur de la clef RSA à 4096 bits
rsa-key-size = 4096

# S'enregistre avec cette adresse (la même que pour la demande de beta)
email = contact@mydomain.com
# Accepte automatiquement les conditions d'utilisation
agree-tos = True

# Utilise une interface purement textuelle à la place de NCurse
text = True

# Utilisez une racine web comme authentifieur
authenticator = webroot
# Le chemin de la racine web
webroot-path = /tmp/letsencrypt-auto
```

## Nginx

Pour que `letsencrypt-auto` puisse s'authentifier automatiquement, il faut que l'on surcharge la configuration de Nginx afin de bypasser certains chemins.

Dans `/etc/nginx/sites-available/monsite` :

```
server {
  listen 80;
  listen [::]:80;
  server_name monsite.fr;

  location '/.well-known/acme-challenge/' {
    root /tmp/letsencrypt-auto;
  }

  location / {
    return 301 https://my_domain.com$request_uri;
  }
}
```

Tant qu'à faire, on fait en sorte de ne passer que par le HTTPS.

Et on recharge la configuration de nginx :

```bash
sudo service nginx reload
```

## Premier certificat

Faisons notre premier certificat manuellement : 

```bash
sudo mkdir -p /tmp/letsencrypt-auto
sudo /opt/letsencrypt/letsencrypt-auto certonly --config /etc/letsencrypt/cfg.ini -d monsite.fr
```

Si tout va bien, vous apercevez maintenant un texte indicant la réussite et que votre nouveau certificat est à l'emplacement `/etc/letsencrypt/live/monsite.fr/fullchain.pem`.

## Configuration le https sur nginx

Retournons à la configuration du site nginx `/etc/nginx/sites-available/monsite` :

```
server {
  listen 443 ssl;
  server_name monsite.fr;

  ssl_certificate        /etc/letsencrypt/live/monsite.fr/fullchain.pem;
  ssl_certificate_key    /etc/letsencrypt/live/monsite.fr/privkey.pem;

  location / {
    root /var/www/monsite;
  }
}
```

Et recharchez la configuration :

```bash
sudo service nginx reload
```

## Automatiser le renouvellement des certificats

Dans un fichier adéquat (ex : `/usr/local/sbin/certrenew.sh`)

```bash
#!/bin/bash
DOMAINS="-d monsite.fr"
DIR=/tmp/letsencrypt-auto
mkdir -p $DIR && /opt/letsencrypt/letsencrypt-auto certonly --renew -c /etc/letsencrypt/cfg.ini $DOMAINS
service nginx reload
```

N'oubliez pas de le rendre exécutable :

```bash
sudo chmod a+x /usr/local/sbin/certrenew.sh
```

Et automatisez son exécution, en ouvrant un crontab :

```bash
sudo crontab -e
```

et rajoutez une ligne :

```
0 0 1 1,3,5,7,9,11 1 bash /usr/local/sbin/certrenew.sh >> /var/log/certrenew.log
```

Cela lancera le script tous les 1ers des mois impairs (janvier, mars, mai, etc.) 

## Références

 * Site officel : [Let's Encrypt](https://letsencrypt.org/)
 * Article de blog : [ramblings](https://overflow.no/blog/2015/12/04/fully-automated-https-with-certificates-from-lets-encrypt/)

