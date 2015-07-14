---
layout: page
title:  "Using Ready-made View Controllers"
categories: ios-sdk
---

View Controllers are a staple in iOS development, and the iOS SDK provide view controllers for modules that Stellar Loyalty exposes.

Before using any view controller, it should be noted first that for these view controllers to work, the user must have logged in already. To learn more about the login view, go to our [previous article detailing about the login process].

## `SLViewController`

All view controllers exposed by the Stellar Loyalty iOS SDK are descendants of a super-class named `SLViewController`. The SLViewContoller provides basic helpers or convenience methods for regular `SLViewController` functionalities. More of this can be seen here: [`SLViewController`]({{site.baseurl}}).

## Anatomy of a Stellar Loyalty View Controller

The image beliow dissects a typical view controller's parts. As you can see, the view controller can be divided into two major components:

- Navigation Bar
- Content View

![]({{site.baseurl}}/img/sdk/ios/view_controllers/view_controller_anatomy.png)

### Navigation Bar

Having a navigation bar inside a Stellar Loyalty View Controller means the basic SDK View Controller depends on an encapsulating Navigation Controller (`UINavigationController`). That means whenever you have an iOS app being developed, either you use a navigation controller as your starting view controller (as illustrated below):

![]({{site.baseurl}}/img/sdk/ios/view_controllers/view_controller_navcontroller.png)

or 