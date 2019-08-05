---
layout: post
title: "Extraire paquet .deb"
date: 2015-03-20 00:00:50 +0200
categories: proxy
---

Il peut être parfois vital d’extraire le contenu d’un paquet `.deb` pour tester une libraire ou pour effectuer une installation dont les dépendances ne sont plus maintenues voir indisponible dans le repo.

On peut éditer le fichier control, pour par exemple changer les versions de dépendance (ex: dependance2.2.1 en dependance2.2.0), ainsi que le md5sum, puis re-construire le paquet .deb et l’installer avec `dpkg -i`

# Première méthode

Avec la commande `ar`

```sh
ar xv <paquet.deb>
```

# Deuxième méthode

Extraire l’arborescence avec `dpkg-deb` :

```sh
dpkg-deb -x <paquet.deb> <repertoire>
```

Extraire le répertoire DEBIAN contenant les différents fichiers postinst, control, etc:

```sh
dpkg-deb -e <paquet.deb>
```

Pour le refabriquer:

```sh
dpkg-deb -b <repertoire> <paquet.deb>
```
