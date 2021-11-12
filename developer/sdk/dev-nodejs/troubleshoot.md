# Troubleshoot



{% hint style="info" %}
_Make sure your mobile device and node server are connected to the same network._
{% endhint %}

{% hint style="info" %}
_Make sure the service end point in hypersign.json is accessible from mobile device. i.e. use ip address instead of ''localhost_
{% endhint %}

{% hint style="info" %}
_In case you are using SSL with your server, you should use 'wss' protocol instead of 'ws' with`WEBSOCKET_URL.`_
{% endhint %}

> If you face this error:&#x20;

```
TypeError: Cannot destructure property 'challenge' of 'body' as it is undefined.
```

Which means that you have not allowed to parse json body in your express. Make sure to you allow json requests in your express middleware. For example, `app.use(express.json())`



