---
layout: page
title:  "Project Anatomy"
categories: ios-sdk
---
Every Cocoapods-enabled project will be structured as an XCode Workspace consisting of at least two projects:

1. the Pods compilation XCode Project; and
2. the Main Application XCode Project

![]({{site.baseurl}}/img/sdk/ios/project_anatomy/project_folder_structure.png)

![]({{site.baseurl}}/img/sdk/ios/project_anatomy/project_folder_workspace.png)

## The Main Application XCode Project

As you create your own iOS Application, and named it as such (for example, `MyLoyalty` from above screenshots), there will be a project named so for you to build your custom application. You can create your own views, controllers, and even respond to application events using your own Application Delegate from the files within here.

## The Pods Compilation XCode Project