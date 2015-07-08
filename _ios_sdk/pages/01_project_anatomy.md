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

After finishing steps involving cocoapod setup, an XCode Workspace file is created. The cocoapod-generated `.xcworkspace` includes your previously-created iOS Application Project (for example, `MyLoyalty` from above screenshots). This project is your Main Application XCode Project.

You can create your own views, controllers, and even respond to application events using your own Application Delegate from the files within here. The Main Application XCode Project can be treated as a regular iOS App Workspace.

> The Main Application XCode Project can be treated as a regular iOS App
> Workspace.

Similarly, if the main project depends on existing iOS 3rd-party libraries, such libraries can be checked if they are supported or can be installed from [cocoapods.org](http://cocoapods.org).

## The Pods Compilation XCode Project