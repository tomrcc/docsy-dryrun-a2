---
title: Docsy Starter
description: A documentation site built with Docsy, ready to edit in CloudCannon.
layout: landing
params:
  body_class: td-navbar-links-all-active
content_blocks:
  - _name: blocks/cover
    title: Welcome to the Docsy Starter
    subtitle: ""
    description: Documentation your whole team can edit — in the page, in CloudCannon.
    image: /images/home-background.jpg
    image_anchor: top
    height: full
    below_navbar: true
    color: dark
    buttons:
      - text: Read the docs
        url: /docs/
        color: primary
        icon: ""
        new_tab: false
      - text: Edit this page
        url: /docs/getting-started/
        color: secondary
        icon: fa-solid fa-pen-to-square
        new_tab: false
    link_down: true
    byline: ""
  - _name: blocks/lead
    content: |-
      This page is built from **blocks**. In CloudCannon's Visual Editor, click
      any heading or paragraph to edit it, or open the page's sidebar to add,
      reorder and remove blocks.
    color: white
    height: auto
    below_navbar: false
  - _name: blocks/features
    color: primary
    features:
      - title: Edit in place
        icon: fa-solid fa-i-cursor
        content: Click text on any page to change it. Your edits appear as you type.
        url: /docs/getting-started/
        url_text: How editing works
      - title: Write docs in markdown
        icon: fa-solid fa-book
        content: Docs pages use the Content Editor, with Docsy's alerts, tabs and images as snippets.
        url: /docs/getting-started/writing-docs/
        url_text: See the snippets
      - title: Share the site settings
        icon: fa-solid fa-sliders
        content: Footer text and community links live in *Site data*, so every page stays in step.
        url: /docs/reference/
        url_text: What you can change
  - _name: blocks/section
    content: |-
      Add another block with the **+** button below this one.
    color: white
    height: auto
    below_navbar: false
    centered: true
    large_text: true
---
