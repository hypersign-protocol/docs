---
description: Developer documentation to implement Hypersign authentication in projects
---

# Introduction

The Hypersign protocol can be implemented in projects in multiple ways.

{% tabs %}
{% tab title="Without Registration page" %}
The easiest and the quickest way to implement Hypersign is by implementing ONLY login page and NOT the registration page. This way of implementation has the following advantages:

* Reduces user onboarding time drastically.
* No development time is required for implementing registration forms and its management.
* No recovery feature needs to be implemented.
* Websites get **VERIFIED** user-data like email, phone number etc. no further verification is required.
* Users need not go through the pain of filling the lengthy registration form which often leads them to back off the system.

On the flip side it has the following limitations:

* The end-user uses `Hypersign Auth Credential` to login into the website; meaning the website TRUST on Hypersign authentication server, who is acting as an issuer.
* The user has to use the same credential on every website which might be questionable from the security standpoint.

> _**Website acts as an verfier!**_
{% endtab %}

{% tab title="With Registration page" %}
The probably be the ideal way for developers to implement authentication in websites. In this case,  the websites need to implement the registration form page. In order to implement the registration page, the developer needs to first create **SCHEMA** in the [developer dashboard](https://hsdev.netlify.app). More about developer dashboard and its use can be read in the next section. This way of implementation has the following advantages:

* The website can now issue a credential to its user.&#x20;
* The website does not have to trust on `Hypersign Auth Credential` which was issued by Hypersign authentication server.
* Each and every website can now issue their own credential, making the system highly secure and scalable.&#x20;
* The website does not have to worry about their user being tracked or traced by Hypersign :)

On the other side:

* The website needs to manage mail servers for sending email and verifying their users.
* The registration page UI implementation might take some time to develop.

> _**Website acts as an issuer as well as verfier!**_
{% endtab %}
{% endtabs %}

There is a tradeoff of both the approaches, we let the developers decide which approach suits best for their businesses.&#x20;

Now that you know different ways to implement Hypersign protocol, let us go ahead and learn how to implement it. One can implement Hypersign protocol using our SDKs, currently available for Nodejs but soon be available for Java and Python as well. These SDKs need a configuration file called,`hypersign.json` which can be generated from the **Developer Dashboard**. Read the next section to learn how to use the developer dashboard to generate the configuration file.







