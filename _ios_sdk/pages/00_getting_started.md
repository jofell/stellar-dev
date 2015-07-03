---
layout: page
title:  "Getting Started"
categories: ios-sdk
---
The Stellar iOS SDK is built with dependency management in mind. [Cocoapods](http://www.cocoapods.org) is therefor a requirement for developers to be able to incorporate the full-featured Stellar iOS SDK into their projects and build loyalty applications in no time.

## Setting up Cocoapods

To set up cocoapods, open the Terminal app and invoke the following command:

{% highlight bash %}
$ gem install cocoapods
{% endhighlight %}

If this doesn't work and requires you to have root access, invoke the following instead:

{% highlight bash %}
$ sudo gem install cocoapods
{% endhighlight %}

## Adding the Stellar Loyalty Private Podspec

Cocoapods allow private pods, and Stellar Loyalty's iOS SDK is an example of a private pod. To be able to get access to the iOS SDK, please email us at [developer@stellarloyalty.com](developer@stellarloyalty.com) and request access for our private podspec.

Once you get hold of our private Podspec's repository (a place where all the Stellar Loyalty iOS SDK libraries are enumerated), you can add the URL we will provide to your local pod repositories. You can do so by invoking this command in Terminal:

{% highlight bash %}
$ pod repo add stellar-sdk <podspec URL that we wll send you>
{% endhighlight %}

From then you can wait until the podspec repository gets synchronized into your machine.

