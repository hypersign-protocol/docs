# Server Side

### Import

Once the package is installed, you can import the package. You can make use of _import_ keyword for this if you want.

```javascript
const HypersignAuth = require('hypersign-auth-js-sdk')
```

### Initialize

At first, we need to initialize an instance of _HypersignAuth_. The _HypersignAuth_ works on Websocket.  Currently, it uses in-mem storage for managing connections. The in-mem storage is certainly not good for   highly scalable systems. In later versions, we will add configuration for some better storage mechanism like Redis.   &#x20;

Let's initialize an instance of _HypersignAuth_ using _"new"_ keyword and pass the required parameters.

```javascript
const hypersign = new HypersignAuth(server);
```

#### Parameters

* `server`**: **HTTP or HTTPS server object of your node js backend.

### Authenticate API

Once our instance is initialised, we need to implement a POST API for **authentication**. This API will be called from _Hypersign Identity Wallet_ when a user submits his/her credential after scanning the QR code on the login page.&#x20;

```javascript
// Implement /hs/api/v2/auth API 
app.post('/hs/api/v2/auth', hypersign.authenticate.bind(hypersign), (req, res) => {
    try {
        const user = req.body.hsUserData;
        // Do something with the user data.
        res.status(200).send({ status: 200, message: "Success", error: null });
    } catch (e) {
        res.status(500).send({ status: 500, message: null, error: e.message });
    }
})
```

Notice we have used`hypersign.authenticate()`middleware to verify the credential presented by the user.&#x20;

**On successful verification;**&#x20;

* The middleware sends an `Authorization` token to the browser using Websocket connection.
* You get the userdata from`req.body.hsUserData` object which you might want to store it in a database for your future use (see line number 4).
* The Hypersign Identity Wallet gets a `success` response with status code `200`.

**On verification failure;**

* Middleware will sends `Unauthorize` response with status code `401` to the Hypersign Identity Wallet.

{% hint style="info" %}
_Make sure to use the same API endpoint name -** /hs/api/v2/auth** as given in this example. _
{% endhint %}

### Authorize an API

Let's say you have a resource, `/protected` , which you want to protect. All you have to do is add `hypersign.authorize()` middleware to protect the resource. See the code below.&#x20;

```javascript
app.get('/protected', hypersign.authorize.bind(hypersign), (req, res) => {
    try {
        const user = req.body.userData;
        // Do whatever you want to do with it
        // Send a message or send to home page
        res.status(200).send("I am protected by Hypersign authentication");
    } catch (e) {
        res.status(500).send(e.message)
    }
});
```

The browser or the client will send the Authorization token whenever it wants to access any protected resource. The authorization token must be added as a `Bearer authorization token`** **in header. The `hypersign.authorize() `middleware verifies the token and gives access to the resource.&#x20;

**On successful verification;**&#x20;

* The server can give access to the requested resource say, a home page.&#x20;

**On verification failure;**

* The middleware send `Unauthorize` response with status code `403` to the browser.



{% hint style="info" %}
Go to the next section to implement client-side code in order to display QR code on the login page.
{% endhint %}

Demo implementation fo server side code is available [here](https://github.com/hypersign-protocol/hypersign-auth-js-sdk/blob/master/demo/server.js).

