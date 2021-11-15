---
description: Data model for registration page
---

# Schema

A schema is nothing but datamodel for the registration form. When a user fills the registration form and clicks on register button, the website issues an authentication credential to the user which user has to use to login. The authentication credential must have a schema. Hypersign strictly binds a schema with the credential. Meaning, the credential can only contain fields defined in the schema. This is to ensure security and data leak.

> In layman terms, you define data fields for your registration page in the form of schema.&#x20;

Let us say our application is called **PetShop **for which we want to design the registration page. Fill schema name, description and required fields (called attributes) and hit the `Create` button to create a new schema.

![](<../../.gitbook/assets/image (19).png>)

Once schema is successfully create, it will show in the table below.

![](<../../.gitbook/assets/image (20).png>)

Now that our schema has created, we are ready to create our first app.
