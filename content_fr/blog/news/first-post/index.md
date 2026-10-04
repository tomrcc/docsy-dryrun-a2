---
_schema: default
title: Welcome to the Docsy Starter
linkTitle: Welcome
date: 2026-09-01T00:00:00Z
description: >
  A Docsy site you can edit in CloudCannon — docs, blog and landing pages
  included.
author: The Docsy Starter team
tags:
  - announcements
categories:
  - News
draft: false
resources:
  - src: '**.{png,jpg}'
    params:
      byline: Photo by Peter Xie from Pexels
---
This post is a **page bundle**: a folder holding `index.md` and the images the post uses. Images uploaded while editing this post are saved into the same folder.

![ASD](pexels-polina-tankilevitch.jpg "Test")

## Images with captions

Docsy's image component crops or resizes an image from the post's folder and adds a caption:

{{< imgproc sunset Crop "500x300" >}}
A sunset, cropped to 500×300.
{{< /imgproc >}}

In the Content Editor, select the image card to change the image, the processing (Crop, Fill, Fit or Resize) and the size.