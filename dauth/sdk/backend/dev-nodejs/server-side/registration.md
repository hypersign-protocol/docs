# Registration

{% hint style="warning" %}
Make sure you have created a schema in the developer dashboard portal before proceeding.
{% endhint %}

To implement the registration form, you need to implement two APIs in the server-side:

* **Register API:** Analogous to register the user but not yet activated and to be called when user press "Register" button on the registration form.
* **Credential API:** Analogous to activate user and to be called from the wallet app.

### Register API

```javascript
// Implement /register API: 
// Analogous to register user but not yet activated
app.post('/hs/api/v1/register', hypersign.register.bind(hypersign), (req, res) => {
     console.log('Register success');
     // You can store userdata (req.body) but this user is not yet activated since he has not 
     // validated his email.
     res.status(200).send({ status: 200, message: "Success", error: null });
})
```

### Credential API

```javascript
// Implement /verify API: 
// Analogous to activate user
app.get('/api/v1/auth/verify', hypersign.issueCredential.bind(hypersign), (req, res) => {
    const { hypersign } = req.body;
    const { data } = hypersign;
    res.status(200).send({ ...data });
})
```
