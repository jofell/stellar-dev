---
layout: page
title:  "Using the Core SDK"
categories: android-sdk
---

In this document we will provide the steps on how to build your Stellar API Data Driven Android Application using the Core SDK. As mentioned in the [Introduction]({{site.baseurl}}/android_sdk/pages/00_introduction.html), the Core SDK is a custom HTTP client for doing Stellar API calls and its usage will be described here in detail.

## Sample Workflow
 
The simplified image below illustrates the sample workflow for your application:

![]({{site.baseurl}}/img/sdk/android/sample_workflow.png)

This document describes **Steps 1, 2 and 4** using the Core SDK. 

**Step 3** Present Data will be covered in the next document [Using the UI SDK]({{site.baseurl}}/android_sdk/pages/03_ui_sdk.html).


## Building your Data Driven Application

As with any other API, we first need to **Login** to the API before querying data.

#### Login Methods

The `StellarSdk` provides a few options to **Login** to the API:

* Regular Email Login - requires an **email** and **password**
* Login via Facebook - requires the **access token** from Facebook API (w/ "email" permission)
* Login via Google Plus - requires the **access token** from Google Plus API

Sample calls for Email and Facebook Login are shown below:

![]({{site.baseurl}}/img/sdk/android/login_apis.png)

After a **Login** attempt by the SDK, the appopriate callback method will be called from the `LoginListener`. 

![]({{site.baseurl}}/img/sdk/android/login_listener.png)

After a *successful* **Login**, the Core SDK will do the handling of the current user's identity for you (user data persistence, refreshing of access token, etc.).

NOTE: There are some cases where you want to determine first if a user is currently logged in before showing your Login UI, a helper method `isLoggedIn(context)` is provided for this use case.

#### Querying Data from the API

The `StellarSdk` provides GET methods for querying data from the API. Each call requires a corresponding listener, which depends on the data that you want to query. So be sure to call the appropriate method and listener when querying data from the API.

![]({{site.baseurl}}/img/sdk/android/get_profile.png)

The methods for querying data has two types:

![]({{site.baseurl}}/img/sdk/android/get_vs_refresh.png)

If you want to make sure that your Data is fresh, call the REFRESH method. Else, use the GET method. The rules for **cache-control** are described in the `CacheControlInterceptor` class.

Each GET method in `StellarSdk` has a corresponding REFRESH method, some examples:

* `getProfile(...)` vs. `refreshProfile(...)`
* `getOffer(...)` vs. `refreshOffer(...)`
* `getOffers(...)` vs. `refreshOffers(...)`

#### Stellar Module Class Diagram

The Stellar API is divided into logical components which are called **modules** and can be viewed in detail on the [API Documentation](http://loyalsphere.github.io/StellarAPI/) site. These modules, called **StellarModules** from hereon, contain the JSON data which is converted to Java Objects (POJO) by the Core SDK. A sample UML class diagram for the StellarModule is shown below:

![]({{site.baseurl}}/img/sdk/android/stellar_module_class_diagram.png)

The image above shows the class hierarchy of two sample Stellar Modules, namely `StellarProfile` and `StellarOffers`. The definition of some of the components are as follows:

* Controller - contains the required components for querying data via HTTP
* Listener - the base listener method for after a successful query of data
* Model/Data - the Data obtained from the API

When querying Data from the API, the following steps take place:

1. StellarSdk calls the appropriate StellarModule GET or REFRESH method via the **Controller**.
2. After each request, the appopriate callback method will be called via the **Listener**.
3. The **Data** is returned via the `success()` method, else an Error Message via `failure`.

Each `accessor` method for the Data is public and can be obtained by using Android Studio's auto-complete feature.

For more information regarding the other **Stellar Modules**, visit `com/stellarloyalty/android/sdk/core/modules/` package.

#### Logging Out

After a user session has ended, you need to logout the current user and remove *ALL* cached response. The `logout()` method lets you do just that without the need for a listener.

![]({{site.baseurl}}/img/sdk/android/logout.png)


--------

**Next:** [Using the UI SDK]({{site.baseurl}}/android_sdk/pages/03_ui_sdk.html)