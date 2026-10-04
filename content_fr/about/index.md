---
title: À propos du Docsy Starter
linkTitle: À propos
description: Un site Docsy configuré pour être modifié dans CloudCannon.
layout: landing
menu: { main: { weight: 10 } }
content_blocks:
  - _name: blocks/cover
    title: À propos du Docsy Starter
    subtitle: ""
    description: Un point de départ pour des sites de documentation que les rédacteurs peuvent modifier sans toucher au code.
    image: /images/about-background.jpg
    image_anchor: bottom
    height: auto
    below_navbar: true
    color: dark
    buttons: []
    link_down: false
    byline: ""
  - _name: blocks/lead
    content: |-
      Ce site utilise le thème Hugo [Docsy](https://www.docsy.dev/). Ses pages d'accueil,
      À propos et Communauté sont construites par blocs ; sa documentation et son blog sont
      des collections markdown.
    color: white
    height: auto
    below_navbar: false
  - _name: blocks/section
    content: |-
      ## Adaptez-le

      Modifiez le titre du site et les options du thème dans `hugo.yaml`, et remplacez le logo
      dans `assets/icons/logo.svg`. Tout ce qu'un rédacteur voit sur la page peut être
      modifié dans CloudCannon.
    color: light
    height: auto
    below_navbar: false
    centered: false
    large_text: false
---
