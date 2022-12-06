---
sidebar_position: 1
---

# Intro

Let's discover **Uteek Mobile Departement**.

## Getting Started

Get started by **creating new React Native App**.
```bash
npx react-native init uteek_example
```
**Visit the officiel React Native documentation**  **[React Native](https://reactnative.dev/)**.

### What you'll need

- [Node.js](https://nodejs.org/en/download/) version 16.14 or above:
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies.

## App Center

Visual Studio App Center brings together multiple common services into a DevOps cloud solution. Developers use App Center to Build, Test, and Distribute applications. Once the app's deployed, developers monitor the status and usage of the app using the Analytics and Diagnostics services.

This section describes the basic concepts of App Center and ways to manage your account settings.

## Create your first app 

To create an app:

Log in to Visual Studio App Center.
Click the Add new dropdown in the upper-right corner of the page, then choose Add new app.
Populate the panel that appears with information about the new app.

### Release Type

Select one of the suggested release types: Alpha, Beta, Enterprise, Production, or Store. You can also use a custom release type by selecting the 'Custom' field. This custom release type must be a single word, alphanumeric, starting with a capital letter or number, followed by lowercase or numbers.

### Uploading an app icon
Upload an app icon in the Add new app dialog, or in the settings page of your app. Uploading an icon in App Center doesn't change the icon in the app bundle, meaning the icon of the app when viewed on the install portal and installed on devices won't reflect this change.

### Accessing apps
All apps that belong to you can be found in My Apps. When looking for apps owned by organizations you belong to, click on the organization in the left navigation.

### App secrets
App secret is like an API key for your app, it allows events and telemetry to be sent to App Center backend. It doesn't provide any access to your account. It can't be used to invoke App Center REST APIs (like trigger builds). If your code is open source, we recommend you inject the secret at build or in a similar way.
### Add the App Center SDK modules
The default integration of the SDK uses CocoaPods for iOS. If you're not using CocoaPods in your app, you need to integrate the React Native SDK manually for your iOS app.

Open a Terminal and navigate to the root of your React Native project, then enter the following line to add App Center Analytics and Crashes to the app:
```bash
yarn add appcenter appcenter-analytics appcenter-crashes --exact
```
### Integrate the SDK automatically for React Native 0.60
#### Integrate React Native iOS
1. Run 
```bash
pod install --repo-update
``` 
from iOS directory to install CocoaPods dependencies.

2. Create a new file with the name AppCenter-Config.plist with the following content and replace *{APP_SECRET_VALUE} with your app secret value. Don't forget to add this file to the Xcode project (right-click the app in Xcode and click Add files to AppName...).
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "https://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
    <key>AppSecret</key>
    <string>{APP_SECRET_VALUE}</string>
    </dict>
</plist>
```
3. Modify the app's AppDelegate.m file to include code for starting SDK:

* Add these lines to import section above the #if DEBUG or #ifdef FB_SONARKIT_ENABLED declaration (if present):
```Objective-C
#import <AppCenterReactNative.h>
#import <AppCenterReactNativeAnalytics.h>
#import <AppCenterReactNativeCrashes.h>
```
* Add these lines to the didFinishLaunchingWithOptions method
### Integrate React Native Android
1. Create a new file with the name appcenter-config.json in android/app/src/main/assets/ with the following content and replace {APP_SECRET_VALUE} with your app secret value.
```javascript
{
    "app_secret": "{APP_SECRET_VALUE}"
}
```
Note: If the folder named assets doesn't exist, it should be created under "project_root/android/app/src/main/assets"
2. Modify the app's res/values/strings.xml to include the following lines:
```xml
<string name="appCenterCrashes_whenToSendCrashes" moduleConfig="true" translatable="false">DO_NOT_ASK_JAVASCRIPT</string>
<string name="appCenterAnalytics_whenToEnableAnalytics" moduleConfig="true" translatable="false">ALWAYS_SEND</string>
```

