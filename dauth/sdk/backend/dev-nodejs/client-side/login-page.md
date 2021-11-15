# Login Page

Now that server-side code is implemented, we can go ahead to implement client-side code in order to display QR code on the login page. For sake of simplicity, we will use HTML and Jquery for this purpose. You can surely use any other frameworks, like Vue, React etc, to design your login page and to show QR code. So let's get started.

### Adding HTML code to display QR

At first, we will add a `div` with id `qrcode` in our `login.html` page.

```markup
<!DOCTYPE html>
<html>
    <head>
        <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/jquery.qrcode@1.0.3/jquery.qrcode.min.js"></script>
    </head>
    <body>
        <div align="center">
            <h1>Login With QR Code</h1>
            <div id="qrcode"></div>
        </div>  
    </body>
</html>
```

### Implementing script to communicate with WebSocket

Then implement WebSocket communication code in the script tag to display the QR code.

```javascript
<script>
$(document).ready(function() {
    let ws = new WebSocket(<WEBSOCKET_URL>);
    ws.onmessage = function({data }) {
        let messageData = JSON.parse(data);
        $("#qrcode").html("");
        if (messageData.op == 'init') {
            $("#qrcode").qrcode({ "width": 300, "height": 300, "text": JSON.stringify(messageData.data) });
        } else if (messageData.op == 'end') {
            ws.close();
            $("#qrcode").hide();
            const authorizationToken = messageData.data.token
            // You can now call 'protected' resource using authorizationToken
        }
    };
});
</script>
```

`<WEBSOCKET_URL>`: The WebSocket URL is nothing but your `Service Endpoint` URL but with `ws` protocol. For example, if your node server is running on the port `4000` then your WebSocket URL would be, `ws://<YOUR_NODE_SERVER_IP_ADDRESS>:4000`

We have to implement two operations in `onmessage` callback.

**`init`**

* The moment a user browse the login.html page in the browser, a new socket connection request goes to the server.
* The server accepts the connection and sends the following information:
  * `Schema`: A data model required to authenticate a user. Think of this, "_This website needs name and email from a user!_".
  * `Authentication API endpoint`: The authentication API endpoint which we exposed in server will contain a new challenge in the query. Example, `<YOUR_NODE_SERVER_HOSTNAME>/hs/api/v2/auth?challenge=XXXXXXX`
  * `SupportedCredentialType: `The supported credential type by this website. By default, it would be `HypersignAuthCredential`.
* The browser displays the QR with the above information. Look at line number 7.

![QR code on login page.](<../../../../../.gitbook/assets/image (14).png>)

**`end`**

* The end user now scans the QR code using **Hypersign Idenitty Wallet** and sends the required credential to the server using the authentication API endpoint.
* Upon successful verification of user credential by the server, the server notifies the browser (client) via WebSocket with an Authorization token. The browser will receive an authorization token in this operation. The browser is now ready to access any "protected" resource, say a home page.

### Calling protected resources using the Authorization token

Once user has successfully authenticated using the Hypersign Identity Wallet, the browser will receive an `Authorization token` from its server. The browser can now make use of that token to access any protected resource.

{% swagger baseUrl="http://localhost:4006/protected" path="" method="post" summary="Request" %}
{% swagger-description %}
Post resource protected by Hypersign
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="false" %}
Bearer
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="http://localhost:4006/protected" path="" method="get" summary="Request" %}
{% swagger-description %}
Get resource protected by Hypersign
{% endswagger-description %}

{% swagger-parameter in="query" name="token" type="string" required="false" %}
\<Authorization token>
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

* Demo implementation of client-side code is present [here](https://github.com/hypersign-protocol/hypersign-auth-js-sdk/blob/master/demo/public/index.html) \[source code].
* [Full implementation of this demo.](https://github.com/hypersign-protocol/hypersign-auth-js-sdk/tree/master/demo) \[source code]
