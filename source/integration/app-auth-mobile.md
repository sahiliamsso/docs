# App-Auth (Mobile)

## Overview

AppAuth for iOS/Android and macOS is a client SDK for communicating with OAuth 2.0 and OpenID Connect providers. It strives to directly map the requests and responses of those specifications, while following the idiomatic style of the implementation language. In addition to mapping the raw protocol flows, convenience methods are available to assist with common tasks like performing an action with fresh tokens.

## Auth Flow

AppAuth supports both manual interaction with the Authorization Server where you need to perform your own token exchanges, as well as convenience methods that perform some of this logic for you. This example uses the convenience method which returns either an XXXAuthState object, or an error.

XXXAuthState is a class that keeps track of the authorization and token requests and responses, and provides a convenience method to call an API with fresh tokens. This is the only object that you need to serialize to retain the authorization state of the session.

## Configuration

First, we need to do dynamic client registration, for that go to - https://ce-dev.gluu.org/oxauth-rp/home.htm
On the top enter https://ce-dev.gluu.org as OpenID Connect Discovery url:

![discovery_url](../img/app-auth/discovery_url.png)
