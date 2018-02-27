---
layout: post
title: JS Snippet - Endswith
categories: js
description: Snippet for string ends with
---

From: [http://stackoverflow.com/questions/280634/endswith-in-javascript](http://stackoverflow.com/questions/280634/endswith-in-javascript)

```    
function endsWith(str, suffix) {
    return str.indexOf(suffix, str.length - suffix.length) !== -1;
}
```