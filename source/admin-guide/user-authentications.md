# User Authentication Introduction

Using the  Gluu Server, you can define the business logic for complex multi-step authentication workflows, providing SSO for people using smart cards, tokens, mobile, or biometric authentication mechanisms. You don't have to chose one multi-factor authentication technology. You can have multiple authentication mechanisms active at the same time--Web or mobile clients can request a certain authentication type by using standard OpenID Connect request parameters.

A number of multi-factor authentication scripts are shipped in the Gluu Server by default, including support for FIDO U2F tokens, Gluu's free mobile two-factor application [Super Gluu](https://super.gluu.org), certificate authentication, and Duo Security. 

!!! Note     
    If you run into issues while configuring or testing authentication mechanisms, e.g. not able to login or facing error pages, please         follow the [FAQ recommendations](./faq.md) to troubleshoot. It is advised to perform tests in an incognito tab or a different browser       to avoid session issues.

