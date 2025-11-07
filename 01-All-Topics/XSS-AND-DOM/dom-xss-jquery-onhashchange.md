# DOM XSS in jQuery selector sink using a # hashchange event 

![Screenshot1](/04-Screenshots/dom-xss-jquery-onchange.png)

Let's analyze the following script:

- 1: window.location.hash → returns # plus the hash.

- 2: window.location.hash.slice(1) → returns the hash starting at position 1 (removes the #).

- 3: window.onhashchange → fires an event when the hash changes.

The event triggered when the hash changes

It gets the title of the section.blog-list, strips the #, and calls scrollIntoView.

**Workflow**

We need to send the target one hash value plus a variation containing our XSS to trigger the onhashchange event. In other words:

- 1: First we make them go to the home page.

- 2: Then we induce an error and add our XSS payload (which triggers the onhashchange event).

```html
<iframe src="<IP>/#" onload="this.src +='<img src=1 onerror=print()>'" hidden="hidden"></iframe>
```

Result:

- 1 call: <IP>/#
- 2 call <IP>/# + `<img src=1 onerror=print()>` = TRIGGER onhashchange 