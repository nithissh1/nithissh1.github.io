---
title: "XSS testing"
date: 2020-06-08T08:06:25+06:00
description: Shortcodes sample
menu:
  sidebar:
    name: Shortcodes Sample
    identifier: shortcodes
    weight: 40
mermaid: true
---

Hi this testing for XSS

```html
<img src=x onerror=confirm(document.domain)>
```
