---
title: "Understanding async & defer script tags"
date: 2021-05-29T08:16:08+10:00
draft: false
categories: ["javascript"]
---

There are two `script` tag attributes that we should be aware of: `async` & `defer`. Understanding the behavioural differences can make our code more performant.

#### async

The `async` attribute denotes that the script will be fetched asynchronously and executed when the download is completed. This behaviour is ideal if the executing script has no dependencies and it itself is not a dependency.

`<script src="index.js" async></script>`

#### defer

The `defer` attribute specifies that the script will be fetched asynchronously and executed once the HTML parsing is complete. Essentially, it behaves like placing the `script` tag before the closing `body` tag, with the added benefit that the script is downloaded asynchronously. Bear in mind, not all browsers support this attribute so it's a good idea to check beforehand. 

`<script src="index.js" defer></script>`

To help understand, [this](https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html) is a source that contains diagrams that clearly illustrate the behavioural differences.