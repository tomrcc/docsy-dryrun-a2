---
title: Docsy Starter
description: Eine mit Docsy erstellte Dokumentationsseite, bereit zur Bearbeitung in CloudCannon.
layout: landing
params:
  body_class: td-navbar-links-all-active
content_blocks:
  - _name: blocks/cover
    title: Willkommen beim Docsy Starter
    subtitle: ""
    description: Dokumentation, die Ihr ganzes Team bearbeiten kann — direkt auf der Seite, in CloudCannon.
    image: /images/home-background.jpg
    image_anchor: top
    height: full
    below_navbar: true
    color: dark
    buttons:
      - text: Zur Dokumentation
        url: /docs/
        color: primary
        icon: ""
        new_tab: false
      - text: Diese Seite bearbeiten
        url: /docs/getting-started/
        color: secondary
        icon: fa-solid fa-pen-to-square
        new_tab: false
    link_down: true
    byline: ""
  - _name: blocks/lead
    content: |-
      Diese Seite besteht aus **Blöcken**. Klicken Sie im Visual Editor von CloudCannon
      auf eine Überschrift oder einen Absatz, um ihn zu bearbeiten, oder öffnen Sie die Seitenleiste,
      um Blöcke hinzuzufügen, neu anzuordnen und zu entfernen.
    color: white
    height: auto
    below_navbar: false
  - _name: blocks/features
    color: primary
    features:
      - title: Direkt bearbeiten
        icon: fa-solid fa-i-cursor
        content: Klicken Sie auf einen Text auf einer beliebigen Seite, um ihn zu ändern. Ihre Änderungen erscheinen während der Eingabe.
        url: /docs/getting-started/
        url_text: So funktioniert das Bearbeiten
      - title: Dokumentation in Markdown schreiben
        icon: fa-solid fa-book
        content: Dokumentationsseiten verwenden den Content Editor, mit den Hinweisen, Tabs und Bildern von Docsy als Snippets.
        url: /docs/getting-started/writing-docs/
        url_text: Snippets ansehen
      - title: Website-Einstellungen teilen
        icon: fa-solid fa-sliders
        content: Fußzeilentext und Community-Links befinden sich in *Site data*, damit alle Seiten einheitlich bleiben.
        url: /docs/reference/
        url_text: Was Sie ändern können
  - _name: blocks/section
    content: |-
      Fügen Sie mit der Schaltfläche **+** unter diesem Block einen weiteren hinzu.
    color: white
    height: auto
    below_navbar: false
    centered: true
    large_text: true
---
