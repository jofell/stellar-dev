---
layout: page
title:  "Getting Started"
categories: android-sdk
---

The Stellar Android SDK source is currently deployed via [Github](https://github.com/LoyalSphere/stellar-android-sdk). To get access to the Android SDK please contact [Stellar Loyalty, Inc](http://stellarloyalty.com/).


## Setting up on Android Studio

This guide will help you **import** the Stellar Android SDK in [Android Studio](http://developer.android.com/tools/studio/index.html).

1. Download the repository:
	
	`git clone https://github.com/LoyalSphere/stellar-android-sdk`
2. On your Android Studio Project, import the Android SDK Library Project as a ***Module***:

	![]({{site.baseurl}}/img/sdk/android/android_studio_import_module.png)
	
	Once prompted with the *wizard*, select the Library Project that you want to include (either **'sdk-core'** or **'sdk-ui'**)
	
	![]({{site.baseurl}}/img/sdk/android/android_studio_import_module_directory.png)

3. Add the API Endpoint via ***strings.xml***:

	![]({{site.baseurl}}/img/sdk/android/api_endpoint_strings.png)

4. Initialize the SDK on the ***Activity***:

	The **`StellarSdk`** requires three parameters, an Android `Context`, a `StellarEndpoint`, and a `boolean` debug flag.
	
	Use the string resources created from the previous step to instantiate a `StellarEndpoint` for starting up the SDK. This is where all the API calls will be directed to after initialization.
	
	![]({{site.baseurl}}/img/sdk/android/sdk_init_oncreate.png)
	
	*Congratulations!* The SDK is now initialized and ready for use.
	
## Stellar SDK Class

The **`StellarSdk`** class is your main entry point for querying objects via the Stellar API. All your HTTP requests (`GET`, `POST`, `PUT`, `DELETE`, etc.) are routed to this class.

A screenshot of some methods of the **`StellarSdk`** is shown below:

![]({{site.baseurl}}/img/sdk/android/stellar_sdk_class_structure.png)

The screenshot shows a variety of *asynchronous* `GET` methods. Each method requires the caller to pass in a `Listener` which is just a [Callback](http://square.github.io/retrofit/javadoc/retrofit/Callback.html) at its core.

## Sample API Call

The following example shows a Sample API call via the **`StellarSdk`** class:

![]({{site.baseurl}}/img/sdk/android/stellar_sdk_get.png)

After a successful `GET` request, the `StellarProfile` object may be retrieved via the `success()` method. Else, an *error message* will be returned via the `failure()` method.

![]({{site.baseurl}}/img/sdk/android/stellar_sdk_listener.png)



--------

**Next:** [Calling the Stellar API]({{site.baseurl}}/android_sdk/pages/02_calling_stellar_api.html)