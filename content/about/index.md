---
title: About the Docsy Starter
linkTitle: About
description: A Docsy site set up for editing in CloudCannon.
layout: landing
menu: { main: { weight: 10 } }
content_blocks:
  - _name: blocks/cover
    title: About the Docsy Starter
    subtitle: ""
    description: A starting point for documentation sites that editors can change without touching code.
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
      This site uses the [Docsy](https://www.docsy.dev/) Hugo theme. Its home,
      About and Community pages are page-builder pages; its docs and blog are
      markdown collections.
    color: white
    height: auto
    below_navbar: false
  - _name: blocks/section
    content: |-
      ## Make it yours

      Change the site title and theme options in `hugo.yaml`, and swap the logo
      in `assets/icons/logo.svg`. Everything an editor sees on the page can be
      changed in CloudCannon.
    color: light
    height: auto
    below_navbar: false
    centered: false
    large_text: false
---
