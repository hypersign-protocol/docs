# Registration

{% hint style="warning" %}
Make sure you have created schema in the developer dashboard portal.
{% endhint %}

If you opted to create the schema in the Developer Dashboard, you need to implement the registration functionality. For that you need to implement two APIs in the server side:

* **Register API:**  Analogous to register user but not yet activated and to be called when user press "Register" button on the registration form.
* **Credential API: **Analogous to activate user and to be called from mobile app.

### Register API

```javascript
// Implement /register API: 
// Analogous to register user but not yet activated
app.post('/hs/api/v2/register', hypersign.register.bind(hypersign), (req, res) => {
    try {
        console.log('Register success');
        // You can store userdata (req.body) but this user is not yet activated since he has not 
        // validated his email.
        res.status(200).send({ status: 200, message: "Success", error: null });
    } catch (e) {
        res.status(500).send({ status: 500, message: null, error: e.message });
    }
})
```

### Credential API

```javascript
// Implement /credential API: 
// Analogous to activate user
app.get('/hs/api/v2/credential', hypersign.issueCredential.bind(hypersign), (req, res) => {
    try {
        console.log('Credential success');
        // Now you can make this user active
        res.status(200).send({ status: 200, message: req.body.verifiableCredential, error: null });
    } catch (e) {
        res.status(500).send({ status: 500, message: null, error: e.message });
    }
})
```
