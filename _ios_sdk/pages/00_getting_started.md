---
layout: page
title:  "Getting Started"
categories: ios-sdk
---
The Stellar iOS SDK is built with dependency management in mind. [Cocoapods](http://www.cocoapods.org) is therefore a requirement for developers to be able to incorporate the full-featured Stellar iOS SDK into their projects and build loyalty applications in no time.

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
$ pod repo add stellar-sdk <podspec URL that we will send you>
{% endhighlight %}

From then you can wait until the podspec repository gets synchronized into your machine.

## Enabling Cocoapod into an Application

To get started with making your application Cocoapod-supported (whether existing or new XCode Project):

1. Open Terminal
2. Change to the directory where the .xcodeproj file is located, like so: {% highlight bash %}
$ cd /Users/yourusername/project_folder/where_xcodeproj_is
{% endhighlight %}
3. Invoke the following command to initialize Cocoapod: {% highlight bash %}
$ pod init
{% endhighlight %} This step will yield a file in that same directory named `Podfile`.
4. Modify the `Podfile` to add Stellar Loyalty's SDK by appending the following line at the bottom of the file (you can use the editor of your choice):{% highlight bash %}
pod 'StellarSDK'
{% endhighlight %}
5. Add the following lines at the top of the `Podfile` to make sure it's able to get `StellarSDK` from our source:{% highlight bash %}
source 'https://github.com/CocoaPods/Specs.git'
source '<podspec URL that we will send you>'
{% endhighlight %}
6. Start downloading the Stellar Loyalty iOS SDK by invoking the following command: {% highlight bash %}
$ pod install
{% endhighlight %} Downloading the Stellar Loyalty iOS SDK may take a long while before completion, so please make sure to wait until the command above finishes.

> Please take note that you will not be able to download the `StellarSDK`
> Cocoapod unless you've added the private podspec as stated in the section 
> above. The `StellarSDK` pod is not available in the main Cocoapod line of
> libraries.

After the all of this is done, you can now navigate to the project's folder via Finder, and open the file called `<Project Name>.xcworkspace` by double-clicking on it. Notice that the file extension is now `.xcworkspace`, meaning from this point, you will start using the XCode Workspace file instead of the XCode Project file whenever you're editing files for your iOS App.

After opening the XCode Workspace that is just created, you can learn all [about the project structure by going to this page]({{site.baseurl}}/ios_sdk/pages/01_project_anatomy.html).

## Using Cocoapod to Use the iOS Stellar Loyalty SDK sample 

![]({{site.baseurl}}/img/sdk/ios/project_anatomy/project_folder_stellarsdk_demo.png)

The image above illustrates Stellar Loyalty iOS SDK's Demo App running on a Simulator. It is possible to run this demo application simply by using Cocoapod's `try` feature, which allows developers to run an application and try how the pod, when integrated, works in a full application.

Start by invoking the following command:

{% highlight bash %}
$ pod try StellarSDK
{% endhighlight %}

Wait for the entire SDK and demo application to be downloaded, and then an XCode Workspace should be opened by XCode. Once the Stellar Loyalty SDK Demo Workspace has been opened, invoke `Cmd + R` in XCode and the simulator shows the Stellar Demo app shown above.

As can be seen in the figure, the application demonstrates how each of the Stellar Loyalty iOS SDK features work, and they can be started by tapping on any of the front table view's labels. Features are packaged in view controllers, and more is discussed in the section [Using Ready-made View Controllers]({{site.baseurl}}/ios_sdk/pages/03_view_controllers.html)

But for the meantime, you can play around the application, but make sure to start logging in first.

**Next**: [XCode Workspace Project Anatomy]({{site.baseurl}}/ios_sdk/pages/01_project_anatomy.html)
