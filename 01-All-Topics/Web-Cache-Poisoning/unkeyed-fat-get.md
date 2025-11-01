# Web cache poisoning via a fat GET request (override function)


In this lab, each request calls the resource `/js/geolocate.js` and triggers the `setCountryCookie` function through the `callback` parameter.

![Screenshot1](/04-Screenshots/unkeyed-fat-get1.png)

The value of this parameter can be modified, and any changes will be reflected in the response.

![Screenshot1](/04-Screenshots/unkeyed-fat-get2.png)

To achieve proper cache poisoning, we take advantage of the fact that the server accepts **GET requests with a body**, which does not affect the cache key (UNKEYED KEY).

Finally, we overwrite the **callback** value.

![Screenshot1](/04-Screenshots/unkeyed-fat-get3.png)

