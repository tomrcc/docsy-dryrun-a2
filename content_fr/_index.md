---
_schema: default
title: Docsy Starter
linkTitle: ''
description: Un site de documentation construit avec Docsy, prêt à être modifié
  dans CloudCannon.
layout: landing
menu:
  main:
    weight: 50
params: {}
content_blocks:
  - _name: blocks/cover
    title: Bienvenue sur le Docsy Starter TE$T TOM
    subtitle:
    description: Une documentation que toute votre équipe peut modifier —
      directement dans la page, dans CloudCannon.
    image: /images/home-background.jpg
    image_anchor: top
    height: full
    below_navbar: true
    color: dark
    buttons:
      - text: Lire la documentation
        url: /docs/
        color: primary
        icon: ''
        new_tab: false
      - text: Modifier cette page
        url: /docs/getting-started/
        color: secondary
        icon: fa-solid fa-pen-to-square
        new_tab: false
    link_down: true
    byline: ''
  - _name: blocks/lead
    content: Cette page est construite à partir de **blocs**. Dans le Visual Editor
      de CloudCannon, cliquez sur un titre ou un paragraphe pour le modifier, ou
      ouvrez la barre latérale de la page pour ajouter, réorganiser et supprimer
      des blocs.
    color: white
    height: auto
    below_navbar: false
  - _name: blocks/features
    color: primary
    features:
      - title: Modifier sur place
        icon: fa-solid fa-i-cursor
        content: Cliquez sur le texte de n'importe quelle page pour le changer. Vos
          modifications s'affichent au fil de la saisie. CHANGED HERE! re-render
        url: /docs/getting-started/
        url_text: Comment fonctionne la modification
      - title: Rédiger la documentation en markdown
        icon: fa-solid fa-book
        content: Les pages de documentation utilisent le Content Editor, avec les
          alertes, onglets et images de Docsy sous forme de snippets.
        url: /docs/getting-started/writing-docs/
        url_text: Voir les snippets
      - title: Partager les réglages du site
        icon: fa-solid fa-sliders
        content: Le texte du pied de page et les liens de la communauté se trouvent dans
          *Site data*, pour que toutes les pages restent cohérentes.
        url: /docs/reference/
        url_text: Ce que vous pouvez modifier
  - _name: blocks/section
    content: Ajoutez un autre bloc avec le bouton **\+** sous celui-ci.
    color: white
    height: auto
    below_navbar: false
    centered: true
    large_text: true
---
