---
title: 🌱 Decode data của wichart
tags:
  - til
date: 2024-02-22
aliases: 
draft: true
---
```javascript
var script = document.createElement('script');

script.src = 'https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.0.0/crypto-js.min.js';

document.getElementsByTagName('head')[0].appendChild(script);

function decrypt(t) {
  var CryptoJS = window.CryptoJS;
  var r = "ZmRvaWFmaGRpc2ZoaWRzZHNoa2RoaW9zZGZoc2E=";
  return JSON.parse(CryptoJS.AES.decrypt(t, r).toString(CryptoJS.enc.Utf8));
}

encrypted-text = "encrypted-text";
data = decrypt(encrypted-text);
```