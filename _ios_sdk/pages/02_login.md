---
layout: page
title:  "Building the Login Interface"
categories: ios-sdk
---

This is the universal login and signup view you can attach to your view controllers content views. `SLLoginView` also has a view delegate protocol that when used to any object, will be able to subscribe to login or signup events made by this widget.

`SLLoginView` not only has a view for the email and password fields, it also has buttons for select social media login schemes for the following: 

  - [Facebook](http://www.facebook.com)
  - [Google Plus](http://plus.google.com)
  - [LinkedIn](http://www.linkedin.com), and 
  - [Twitter](http://www.twitter.com). 
  
Also, the `SLLoginView` class already has builtin mechanisms to catch login events for both social and regular logins. `SLLoginView` allows this by presenting a swipe view for each kind of login / signups.

#### Signup View ####

![SLLoginView Signup Screen]({{site.baseurl}}/img/sdk/ios/login/SLLoginViewSample1.png)

#### Normal Login View ####

![SLLoginView Signup Screen]({{site.baseurl}}/img/sdk/ios/login/SLLoginViewSample2.png)

#### Social Login / Signup View ####

![SLLoginView Signup Screen]({{site.baseurl}}/img/sdk/ios/login/SLLoginViewSample3.png)

#### Showing Swipe View Between Normal and Social Login / Signup View ####

![SLLoginView Signup Screen]({{site.baseurl}}/img/sdk/ios/login/SLLoginViewSample4.png)



## Before using SLLoginView

SLLoginView needs to be initialized with values for configurations (see [SLConfig](../Helpers/SLConfig.md) and [SLConfigButton](SLConfigButton.md)) as well as social media values like the Google Plus Client ID.

To do this, let's start with the App Delegate and import the necessary classes:

{% highlight objective-c %}
#import <StellarSDK/SLConfig.h>
#import <StellarSDK/SLLoginView.h>
{% endhighlight %}

Then on the `UIApplication`'s delegate, fill in the method `application:didFinishLaunchingWithOptions:`, populate the configs structure and initialize the Google Client ID (if needed) like so:

{% highlight objective-c %}
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Override point for customization after application launch.
    
    // Start populating the config structures
    [SLConfig populateConfigs];

    // Before the app starts, set the google plus client id already, 
    // no need to put this conde if not supporting Google+ Login
    [SLLoginView setGooglePlusClientID:@"<Put here the Google Plus Client ID>"];

    return YES;
}
{% endhighlight %}

Then, add to your delegate a typical UIApplicationDelegate method called `application:openURL:sourceApplication:annotation:` and fill it up with the following:

{% highlight objective-c %}
-(BOOL)application:(UIApplication *)application openURL:(NSURL *)url
 sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
  // This code is to listen to any possible social login callback to the app
  // Change this if you must, e.g. if supporting other callbacks other than social
  // media login
    return [SLLoginView handleLoginURL:url sourceApplication:sourceApplication annotation:annotation];
}
{% endhighlight %}

Now that we're finished filling up the delegate, let's proceed to editing your applictaion's info inside XCode. Go to your project's detail view (this can be achieved by clicking on the XCode Project icon on the uppermost part of the project's tree view). Then choose the "Info" tab / label. You should be able to see a screenshot like so:

![SLLoginView Project Info]({{site.baseurl}}/img/sdk/ios/login/SLLoginViewPrep1.png)

#### Adding Facebook Login Support

Add a `FacebookAppID` key under the Custom iOS Target Properties and have its values as your Facebook App ID where your app is supposed to be connected to. Then add another key called `FacebookDisplayName` and put a label on how your app should be labeled inside Facebook. Check the screenshot above to compare what you have done so far.

After adding the two keys, expand the `URL types` tree, and add a new entry with the URL scheme having the following format:

    fb< Your Facebook App ID>
    
Then set the `Role` to `Editor`. No need to provide an `Identifier` nor an `Icon` value for the entry.


#### Adding Google+ Login Support

For Gooogle+ Login, the only entry needed in the Target info is to add a `URL types` entry (same as the instructions on adding a Facebook `URL types` entry), only that you provide the following

- `Identifier` and `URL Scheme` field with the app's `Bundle Identifier` value
- `Role` field with the value `Editor`


## Setup

### Using Storyboard

1. Create a new `UIViewController` class from XCode. Give it an appropriate name. For this documentation's purpose, let's name it as `EXLoginViewController`.
2. Insert a new View Controller on your Storyboard. Make sure you use your just-created View Controller for its class type. See figure below. <br />![SLLoginView Screenshot 1]({{site.baseurl}}/img/sdk/ios/login/SLLoginView1.png)
3. Add a `UIVIew` inside the view controller's content view like in the figure below. Modify its custom class as `SLLoginView` <br /> ![SLLoginView Screenshot 2]({{site.baseurl}}/img/sdk/ios/login/SLLoginView2.png)
4. Create a connection (Ctrl-drag) between the newly-created `UIView` (`SLLoginView`) with the view controller (as shown by the figure below) and assign the `SLLoginView` instance's delegate to the current view controller. <br /> ![SLLoginView Screenshot 2]({{site.baseurl}}/img/sdk/ios/login/SLLoginView3.png)
5. Assign the `SLLoginView` instance as an outlet of the view controller, and name it appropriately. For the purposes of this documentation, let's name the outlet as `loginView`. Don't forget to import `<StellarSDK/SLLoginView.h>` on your view controller's header file.
6. Set which login interfaces should be used in the `SLLoginView` instance. You can set it to the following values:
    - `SLLoginConfigRegular` which gives you the regular login interface
    - `SLLoginConfigSignup` which gives you the signup interface (complete with email, password and name fields)
    - `SLLoginSocialFacebook` which gives you default FB Login button
    - `SLLoginSocialGoogle` which gives you default Google+ Login button
    - `SLLoginSocialLinkedIn` which gives you default LinkedIn Login button
    - `SLLoginSocialTwitter` which gives you default Twitter Login button
    - `SLLoginConfigDefault` which gives you default Regular, FB, and Google+ Logins as well as the signup widget <br/>

7. You can set the login configurations by assigning the `logConfig` attribute to the `loginView` outlet, like so:

{% highlight objective-c %}
// If you just want a normal and a Facebook login only
self.loginView.logConfig = SLLoginConfigRegular | SLLoginSocialFacebook; 

// If you just want a signup and a Google+ login only
self.loginView.logConfig = SLLoginConfigSignup | SLLoginSocialGoogle; 

// You can also combine more. The widget will manage the arrangement autimatically
self.loginView.logConfig = SLLoginConfigRegular | SLLoginConfigSignup | SLLoginSocialGoogle | SLLoginSocialFacebook; 

// This is the same as the above
self.loginView.logConfig = SLLoginConfigDefault
{% endhighlight %}

8. Proceed to handling events from the delegate methods. (Check [Handling Events](#handling-events-using-slloginviewdelegate-methods))


### Using Objective-C code

From your `UIViewController` instance, you can follow through creating a normal view like so under the `viewDidLoad:` method:

{% highlight objective-c %}
- (void)viewDidLoad {

  [super viewDidLoad];
  
  // Do any additional setup after loading the view.
  
  // Instantiate a SLLoginView object. You can set different frame settings
  self.loginView = [[SLLoginView alloc] initWithFrame:self.view.bounds];
  
  // Set the configurations. Check the documentation
  self.loginView.logConfig = SLLoginConfigDefault;
  
  // Don't forget to set the delegate to the current view controller
  self.loginView.delegate = self;
  
  [self.view addSubview:self.loginView];
}
{% endhighlight %}

You can set it to the following values:

  - `SLLoginConfigRegular` which gives you the regular login interface
  - `SLLoginConfigSignup` which gives you the signup interface (complete with email, password and name fields)
  - `SLLoginSocialFacebook` which gives you default FB Login button
  - `SLLoginSocialGoogle` which gives you default Google+ Login button
  - `SLLoginSocialLinkedIn` which gives you default LinkedIn Login button
  - `SLLoginSocialTwitter` which gives you default Twitter Login button
  - `SLLoginConfigDefault` which gives you default Regular, FB, and Google+ Logins as well as the signup widget <br/>

This is true with the following assumptions:

1. The `UIViewController` instance extends the protocol `SLLoginViewDelegate`
2. The `UIViewController` instance contains a property called `loginView` of type `SLLoginView`
3. The view controller's content view is not populated yet (although the `SLLoginView` object can be placed anywhere within the view controller's content view by setting the `SLLoginView`'s frame)
    

## Handling Events Using SLLoginViewDelegate methods

Once the `SLLoginView` object / instance has been set, we are now supposed to wait for whatever event happens after the user taps the buttons within the widget. You may notice that after setting up the `SLLoginView` instance that it automatically lays out all the necessary widgets in a swipe view container, thus making it a lot more accommodating for different kinds of login or signup combinations.

After assigning the holding view controller as the delegate of the `SLLoginView` instance (**NOTE:** The delegate should extend the protocol `SLLoginViewDelegate`), create a method called `loginView:didLoginWithResults:andError:` within your view controller, like so:

{% highlight objective-c %}
-(void)loginView:(SLLoginView *)logView didLoginWithResults:(NSDictionary *)results
        andError:(NSError *)error
{
    // This method gets triggered when something happens in the login view
    
}
{% endhighlight %}

To handle the results of the login (however the method, whether it's via regular login, a signup, or a social media login), just check whether the results give you a success value of true or whether the error is nil. Usually I go the latter:

{% highlight objective-c %}
-(void)loginView:(SLLoginView *)logView didLoginWithResults:(NSDictionary *)results
        andError:(NSError *)error
{
    // This method gets triggered when something happens in the login view
    if (error == nil)
    {
        // Celebrate this momentous event by popping an alert view
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Success!"
                                                          message:@"I finally made SLLoginView work!"
                                                         delegate:nil
                                                cancelButtonTitle:@"OK"
                                                otherButtonTitles:nil];
         [alert show];
    }
    
}
{% endhighlight %}

The results dictionary bears the following structure:

{% highlight objective-c %}
    @{
        @"sucess"        : @YES,
        @"access_token"  : @"<access token retrieved from Stellar Loyalty OAuth Service>"
    }
{% endhighlight %}

## Related Classes

- [SLConfig](../Helpers/SLConfig.md)
- [SLConfigButton](SLConfigButton.md)