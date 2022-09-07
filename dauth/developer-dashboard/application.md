# Application

Click on `Apps` button on the navbar to go to the application page to create an app.

Click on `Create App` button to open app configuration sidebar.

![](<../../.gitbook/assets/image (23).png>)

Here, enter AppName and Service endpoint URL fields.

* AppName: Name of your app. i.e. PetShop App
* Service Endpoint: Url at which your app is running.

{% hint style="info" %}
Make sure your mobile app is also connected to the same network as the mobile app need to hit the service endpoint url.
{% endhint %}

If you are not planning to develop registration page then skip the "Advance configuration" section and hit `Create` button to create an app, else read the next section for advance configuration.

![Basic app configuration](<../../.gitbook/assets/image (21).png>)

Choose the schema (i.e PetShop Credential) from the dropdown and fill mail server configurations. Finally, hit `Create` button to create an app

![Optional advance app configuration](<../../.gitbook/assets/image (22).png>)

Upon successful creation, you will be download `hypersign.json` file which is the configuration file which you need to use in SDK. Optionally you can read the next section to understand what contains in the `hypersign.json` file and do they mean.

![](<../../.gitbook/assets/image (26).png>)

Now that you have created the configuration file, you are ready to implement SDK. Read the SDK section for implementing SDK of your choice.
