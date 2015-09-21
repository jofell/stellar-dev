---
layout: page
title:  "Sample App Workflow"
categories: android-sdk
---

In this document we will provide examples on how to consume *Stellar Loyalty API Data* via the Stellar Android **Core SDK**.

## Sample Workflow
 
The simplified image below illustrates the sample workflow for your application:

![]({{site.baseurl}}/img/sdk/android/sample_workflow.png)

**Steps 1, 2 and 4** are described in this document.

**Step 3** Present Data will be covered in the next document [Ready-made View Classes]({{site.baseurl}}/android_sdk/pages/03_view_classes.html).


## Building your Data Driven Application

As with any other API, we first need to **Login** to the API before querying data.

#### Login Methods

The `StellarSdk` provides a few options for you to **Login** to the API:

* Regular Email Login - requires an **email** and **password**
* Login via Facebook - requires the **access token** from Facebook API (w/ "email" permission)
* Login via Google Plus - requires the **access token** from Google Plus API

![]({{site.baseurl}}/img/sdk/android/login_apis.png)

After a **Login** attempt by the SDK, the appopriate callback method will be called from the `LoginListener`. 

![]({{site.baseurl}}/img/sdk/android/login_listener.png)

After a successful **Login**, the Core SDK will do the handling of the current user's identity for you (user data persistence, refreshing of access token, etc.).

NOTE: There are some cases where you want to determine first if a user is currently logged in before showing your Login UI, a helper method `isLoggedIn(context)` is provided for this use case.

#### Querying Data from the API

The `StellarSdk` provides **Get** methods for querying data from the API. Each **call** requires a corresponding **listener** which depends on the data that you want to query, so be sure to call the appropriate method when querying data from the API.

![]({{site.baseurl}}/img/sdk/android/get_profile.png)

The methods for querying data has two types:

* **Get** - use cached response if *present*, else get fresh data from the API
* **Refresh** - *remove* cached response, get fresh data from the API

Each **Get** method in `StellarSdk` has a corresponding **Refresh** method, e.g.:

* `getProfile(...)` vs. `refreshProfile(...)`
* `getOffer(...)` vs. `refreshOffer(...)`
* `getOffers(...)` vs. `refreshOffers(...)`

In summary, if you want to make sure that your **Data** is fresh, call the **Refresh** method. Else, use the **Get** method.

#### Logging Out

After a user session has ended, you want to remove all cached responses and logout the current user. The `logout()` method lets you do just that without the need for callback.

![]({{site.baseurl}}/img/sdk/android/logout.png)


--------

**Next:** [Ready-made View Classes]({{site.baseurl}}/android_sdk/pages/03_view_classes.html)