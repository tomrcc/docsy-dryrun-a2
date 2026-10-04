---
_schema: default
title: Vue d'ensemble
linkTitle: ''
description: Comment ce site est organisé dans CloudCannon.
weight: 1
tags: []
categories: []
draft: false
menu:
  main:
    weight: 50
---
Ce site est construit avec [Hugo](https://gohugo.io/) et le thème [Docsy](https://www.docsy.dev/). Dans CloudCannon, son contenu est réparti en quelques collections, listées dans la barre latérale.

| Collection | Contenu | Modifier avec |
| --- | --- | --- |
| **Pages** | Les pages d'accueil, À propos et Communauté, et toute nouvelle page d'atterrissage | Le Visual Editor — les pages sont construites à partir de blocs |
| **Docs** | Cette documentation, un fichier markdown par page | Le Visual Editor ou le Content Editor |
| **Blog** | Actualités et notes de version | Le Visual Editor ou le Content Editor |
| **Site data** | Le texte du pied de page et les liens de la communauté | Le Data Editor |

## Ce qui reste dans le code

Les réglages du thème — couleurs, logo, moteur de recherche et titre du site — se trouvent dans `hugo.yaml` et le dossier `assets/`. Demandez à un développeur de les modifier.
