---
title: Über den Docsy Starter
linkTitle: Über uns
description: Eine Docsy-Seite, eingerichtet für die Bearbeitung in CloudCannon.
layout: landing
menu: { main: { weight: 10 } }
content_blocks:
  - _name: blocks/cover
    title: Über den Docsy Starter
    subtitle: ""
    description: Ein Ausgangspunkt für Dokumentationsseiten, die Redakteure ohne Programmierkenntnisse ändern können.
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
      Diese Seite verwendet das Hugo-Theme [Docsy](https://www.docsy.dev/). Die Startseite,
      die Seiten „Über uns“ und „Community“ sind aus Blöcken aufgebaut; Dokumentation und Blog sind
      Markdown-Sammlungen.
    color: white
    height: auto
    below_navbar: false
  - _name: blocks/section
    content: |-
      ## Passen Sie sie an

      Ändern Sie den Seitentitel und die Theme-Optionen in `hugo.yaml` und tauschen Sie das Logo
      in `assets/icons/logo.svg` aus. Alles, was ein Redakteur auf der Seite sieht, lässt sich
      in CloudCannon ändern.
    color: light
    height: auto
    below_navbar: false
    centered: false
    large_text: false
---
