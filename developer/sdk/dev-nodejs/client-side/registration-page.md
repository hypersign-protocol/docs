# Registration Page

{% hint style="info" %}
This is optional if you have not opted for Schema configuration for your app, skip to [Login page](login-page.md) section.
{% endhint %}

{% hint style="warning" %}
Make sure you have created schema in the developer dashboard portal.
{% endhint %}

Add form to take inputs from user. Make sure your form must contains input fields as taken in the schema.

Here we are adding a simple HTML form with a button.

```markup
<body>
    <form>
      <input type="text" name="name" placeholder="Enter your name" /><br />
      <input type="text" name="email" placeholder="Enter your email" /><br />
      <input type="text" name="phoneNumber" placeholder="Enter your phone number" /><br />
      <br />
    </form>
    <button onclick="register()">Register</button>
</body>
```

Notice field's \_name \_ attribute are exactly as we have taken in our **PetShop Credential** schema.

Finally, implement \*\*`register()`\*\*in JavaScript and make a call to Register API.

```markup
<script>
    async function register() {
      let data = {};
      const inputs = document.getElementsByTagName("input");
      // Reading input fields and their values to prepare request body
      for (const input of inputs) {
        data[input.attributes.getNamedItem("name").textContent] = input.value;
      }

      // Calling register api with data
      const resp = await fetch(
        `http://${window.location.host}/hs/api/v2/register`,
        {
          method: "POST",
          body: JSON.stringify(data),
          headers: {
            "content-type": "application/json",
          },
        }
      );

      const json = await resp.json();
      alert(
        "Your credential is sent to you in your email, scan the QR code to receive credential in your Hypersign Identity Wallet"
      );
    }
  </script>
```

The SDK will send an email to the user with a QR code. Where user need to scan the QR code to receive the app credential.

Once user has the credential, he can use that credential to login. Read the next section to implement Login page.

\
\
\
