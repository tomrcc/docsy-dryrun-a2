---
_schema: default
title: Overview
linkTitle: ''
description: How this site is organised in CloudCannon.
weight: 1
tags: []
categories: []
draft: false
menu:
  main:
    weight: 50
---
This site is built with [Hugo](https://gohugo.io/) and the [Docsy](https://www.docsy.dev/) theme. In CloudCannon, its content is split into a few collections, listed in the sidebar.

| Collection | What it holds | Edit it with |
| --- | --- | --- |
| **Pages** | The home, About and Community pages, and any new landing pages | The Visual Editor — pages are built from blocks |
| **Docs** | This documentation, one markdown file per page | The Visual Editor or the Content Editor |
| **Blog** | News and release posts | The Visual Editor or the Content Editor |
| **Site data** | Footer text and the community links | The Data Editor |

## What stays in code

Theme settings — colours, the logo, the search engine and the site title — live in `hugo.yaml` and the `assets/` folder. Ask a developer to change them.