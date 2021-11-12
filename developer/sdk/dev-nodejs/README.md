# Node Js

> In this tutorial, we will see how a developer can integrate Hypersign Authentication protocol in his node js project to provide secure passwordless authentication to his user.

### How does it work?

* The app developer integrates the Hypersign SDK with his nodejs project:
  * [Server Side](server-side/#server-side)
    * Initialise instance of Hypersign using Hypersign Auth JS SDK.
    * Expose Authentication API using `hypersign.authenticate()` middleware.
    * Protect any resource using `hypersign.authorize()`middleware.
  * [Client Side](client-side/)
    * Implement code snippet to display QR code on the login page
* Now the user will download [Hypersign Identity Mobile wallet](https://install.appcenter.ms/orgs/hypermine/apps/hypersign/distribution\_groups/cvv) and register himself.&#x20;
  * Upon registration, he will get `HypersignAuthCredenital` which he can use to login to websites which supports Hypersign authentication.
* For the detailed flow of protocol please visit protocol section.



Watch the demo on Youtube and follow the steps to integrate Hypersign in node js project.

{% embed url="https://www.youtube.com/watch?v=pSCmCZfeQKo&feature=youtu.be" %}



###

##
