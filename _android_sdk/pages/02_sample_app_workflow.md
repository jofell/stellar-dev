---
layout: page
title:  "Sample App Workflow"
categories: android-sdk
---

In this document we will provide examples on how to consume the *Stellar Loyalty API Data* via the Stellar Android **Core SDK**.
## Building your Data Driven Application

As with any other API, we first need to **Login** in to the API before querying data. After logging in, the Core SDK will do the handling of the current user's identity for you (access token persistence, refreshing of access token, etc.).

![]({{site.baseurl}}/img/sdk/android/sample_workflow.png)

1. Login
2. Query Data
	* Get Data - use cache if present, else get new data from server
	* Refresh Data - remove cached copy of request, get new data from server
3. Logout

#### Login Methods

The `StellarSdk` provides a few options for you to **Login** to the API:

* Regular Email Login - requires an **email** and **password**
* Login via Facebook - requires the **access token** from Facebook API (w/ "email" permission)
* Login via Google Plus - requires the **access token** from Google Plus API

![]({{site.baseurl}}/img/sdk/android/login_apis.png)

After a **Login** attempt by the SDK, the appopriate callback method will be called from the `LoginListener`.

![]({{site.baseurl}}/img/sdk/android/login_listener.png)

There are some cases that you want to determine first if a user is currently logged in before showing your Login UI, a helper method `isLoggedIn(context)` is provided.

![]({{site.baseurl}}/img/sdk/android/login_helper.png)


#### Querying Data from the API

#### Logging Out

After a user session has ended, you want to remove all cached responses and logout the current user. The `logout()` method lets you do just that without the need for callback.

![]({{site.baseurl}}/img/sdk/android/logout.png)


--------

**Next:** [View Classes]({{site.baseurl}}/android_sdk/pages/03_view_classes.html)