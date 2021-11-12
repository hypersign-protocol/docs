# OTP is bad

OTP based authentication, at first, seems to be a better solution (widely accepted within the enterprise) when compared to social logins, as it provides some sort of guarantee to service providers that the user actually possesses the phone number or device - the answer to the ‘What you have?’ question (i.e. Proof of Possession) - since it is not viable for a user to share his mobile device with another person. But this guarantee comes with a cost for both the service providers and the end-user.

* Insecure Channel

Security of SMS OTP relies on the confidentiality of SMS messages that successively relies on the safety of cellular networks. Lately, several attacks against GSM, and even 3G networks have shown that the confidentiality of SMS messages cannot necessarily be provided.

* Phone number is not enough

Apart from capturing the phone number, service providers ask users to provide additional personal data in order to build a customer profile in their applications, since OTP authentication only verifies a user’s phone number, but not other details such as email, name, address, geolocation etc.

* Users hesitation in sharing phone numbers

The ‘phone number’ can now be considered as a critical attribute of user identity since it is all linked to bank accounts and other sensitive products and services. If a user wants to try a service in order to check its befitting, the user must share multiple attributes of their identity along with the phone number with an entity with which they might not want to keep a long-term relationship. \


> “The fear that a phone number can be misused by this entity which the user does not trust.”&#x20;

\
Users want to keep their personal data safe and private; especially their phone number and only share it with people and companies whom they fully trust. Once a number gets shared widely, potential problems arise, such as unwanted messages, spam calls, and more.

* OTP is sharable

The ability to share an OTP (even under its “time to live” period) makes it as bad as username and passwords which not only violates the principle of “Proof of possession” but also makes it highly vulnerable for many possible attacks. [According to a recent survey](https://tech.hindustantimes.com/tech/news/26-indians-have-shared-otps-with-others-22-have-shared-bank-details-survey-story-mkOotXpuhdUMPaAoQghLsO.html) by [OLX](https://www.olx.in): 26% of Internet-users said that they have shared sensitive OTPs (one-time pin/passwords) with others.&#x20;







