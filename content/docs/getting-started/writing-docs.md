---
_schema: default
title: Writing docs pages
linkTitle: Writing docs
description: The formatting and Docsy components you can use in a docs page.
weight: 1
tags:
  - editing
  - snippets
categories:
  - Guides
draft: false
menu:
  main:
    weight: 50
---
Docs pages are markdown. In CloudCannon's Content Editor, use the toolbar for **bold**, *italic*, ~~strikethrough~~, [links](https://www.docsy.dev/), lists, tables, images and code. Select the **snippet** button to add a Docsy component.

## Components

Components appear as cards in the Content Editor. Click a card to change its options and text.

### Alerts

{{% alert title="Note" color="primary" %}}
Use an alert to call out something the reader mustn't miss.
{{% /alert %}}

{{% alert title="Warning" color="warning" %}}
Colors: `primary`, `secondary`, `success`, `info`, `warning` and `danger`.
{{% /alert %}}

### Page info

{{% pageinfo color="info" %}}
A page info box sits at the top of a page, for status notes like "This page is
a draft".
{{% /pageinfo %}}

### Tabs

{{< tabpane text=true >}}
{{% tab header="macOS" %}}Install with Homebrew: `brew install hugo`{{% /tab %}}
{{% tab header="Windows" %}}Install with winget: `winget install Hugo.Hugo.Extended`{{% /tab %}}
{{< /tabpane >}}

## Tables

| Field | Type | Required |
| --- | --- | --- |
| title | string | yes |
| description | string | no |
| weight | number | no |

## Code

```yaml
title: My new page
description: A short summary.
weight: 10
```

## Images

Upload an image with the toolbar's image button. It is stored in `static/images/`.

![A sunset over the ocean](/images/home-background.jpg)