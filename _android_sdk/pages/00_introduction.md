---
layout: page
title:  "Introduction"
categories: android-sdk
---

The Stellar Android SDK is divided into two components: the **Core** and **UI** Android Library Projects. The core is a stand-alone library project which communicates directly to the Stellar API, while the UI library project is composed of ready-made view objects that relies on the core for its data.

![]({{site.baseurl}}/img/sdk/android/ui_core_diagram.png)
## Core SDK

The **Core SDK** is a custom HTTP client for doing Stellar API calls easily via Android. It is currently powered by the following open-source libraries:

* [Retrofit](http://github.com/square/retrofit) - a modern, type-safe, Java annotation based HTTP client
* [OkHttp](https://github.com/square/okhttp) - an HTTP + SPDY client which automatically handles things like interceptors and caching
* [Gson](https://github.com/google/gson) - Json to Java Objects conversion

The main entry point for the **Core SDK** is via the `StellarSdk` class which will be discussed in detail via the [Getting Started]({{site.baseurl}}/android_sdk/pages/01_getting_started.html) document.

## UI SDK

The **UI SDK** tries to leverage on the latest Android Support Libraries for ensuring that the UI components is compatible with future releases of the Android SDK. Aside from the Support Libraries, the UI SDK also supports most of the UI use cases that are needed to be able to build Stellar Loyalty applications in no time.

Some of the libraries included in the UI SDK are:

* [Butterknife](http://jakewharton.github.io/butterknife/) - a neat Field and Method binding for Android Views
* [Glide](https://github.com/bumptech/glide) - an image loading and caching library for Android
* [ZXing](https://github.com/zxing/zxing) - an open-source library for multi-format 1D/2D barcode images

## Getting Access

To get access to the Android SDK please contact [Stellar Loyalty, Inc](http://stellarloyalty.com/).

--------

**Next:** [Getting Started]({{site.baseurl}}/android_sdk/pages/01_getting_started.html)
