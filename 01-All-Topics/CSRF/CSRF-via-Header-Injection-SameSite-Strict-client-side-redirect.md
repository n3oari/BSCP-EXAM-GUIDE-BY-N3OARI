# SameSite-Strict-bypass-via-client--side-redirect(Redirect+Path Traversal+CSRF)

In this case, we encounter the attribute **SameSite=Strict** which blocks cookies in requests to external resources.

![Screenshot1](/04-Screenshots/CSRF-Strict0.png)

In the comments section, we find that when submitting a new comment, we are redirected to  the post where we wrote our comment.

![Screenshot1](/04-Screenshots/CSRF-Strict1.png)

Analyzing the script, we discover that we can control, through the URL input, where we want to be redirected.

![Screenshot1](/04-Screenshots/CSRF-Strict2.png)


**Objetive: Redirect + Path Traversal + CSRF**

Make the victim go to an endpoint that does not require cookies, which then causes a redirect to our target endpoint — thus making it be considered as _same-site_.

```js
<script>
    location="<IP>/post/comment/confirmation?postId=../../my-account/change-email?email=pwnd@pwned.com%26submit=1"
</script>
```

