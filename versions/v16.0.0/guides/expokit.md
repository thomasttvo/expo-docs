---
title: Developing With ExpoKit
---

ExpoKit is an Objective-C and Java library that allows you to use the Expo platform with a
native iOS/Android project.

## Before you read this guide

There are two ways to get an ExpoKit project:

- Create a pure-JS project in XDE, then use [exp detach](detach.html) to add ExpoKit.
- Create an app with [create-react-native-app](https://github.com/react-community/create-react-native-app), then choose "eject with ExpoKit".

Make sure you follow one of the above paths before continuing in this guide. The remainder of the guide will assume you have created an ExpoKit project.

## Setting up your project

By this point you should have a JS app which additionally contains `ios` and `android` directories.

### 1. Check JS dependencies

- Your project's `package.json` should contain a `react-native` dependency pointing at Expo's fork of React Native. This should already be configured for you.
- Your JS dependencies should already be installed (via `npm install` or `yarn`).

### 2. Run the project in XDE or exp

Open the project in XDE. If you were already running this project in XDE, press **Restart**.

If you prefer `exp`, run `exp start` from the project directory.

This step ensures that the React Native packager is running and serving your app's JS bundle for development. Leave this running and continue with the following steps.

### 3. iOS: Configure, build and run

This step ensures the native iOS project is correctly configured and ready for development.

- Make sure you have the latest Xcode.
- If you don't have it already, install [CocoaPods](https://cocoapods.org), which is a native dependency manager for iOS.
- Run `pod install` from your project's `ios` directory.
- Open your project's `xcworkspace` file in Xcode.
- Use Xcode to build, install and run the project on your test device or simulator. (this will happen by default if you click the big "Play" button in Xcode.)

Once it's running, the iOS app should automatically request your JS bundle from the project you're serving from XDE or `exp`.

### 4. Android: Build and run

Open the `android` directory in Android Studio, then build and run the project on an Android device
or a Genymotion emulator.

Once the Android project is running, it should automatically request your development url from XDE
or `exp`. You can develop your project normally from here.

## Continuing with development

Every time you want to develop, ensure your project's JS is being served by XDE (step 2), then run
the native code from Xcode or Android Studio respectively.

## Changing Native Dependencies

### iOS

Your ExpoKit project manages its dependencies with [CocoaPods](https://cocoapods.org). If you encounter third-party libraries with CocoaPods instructions, those instructions should apply.

Many libraries in the React Native ecosystem include instructions to run `react-native link`. These are supported with ExpoKit for iOS, but because `react-native link` is not aware of CocoaPods, it may not do a complete job installing your dependency. If you encounter build issues regarding locating the `<React/*>` headers in a dependency library, you may need to follow these steps:

1. In XCode, go to `{your-project}/Libraries/{some-library}`
2. Click on the file `{some-library}.xcodeproj`
3. In the large middle panel, click on "Build Settings". This is the build settings of that specific library
4. Now that you're on the "Build Settings" tab, look down and double click **Header Search Paths**
5. Click + button to add `$(SRCROOT)/../../../ios/Pods/Headers/Public` and choose `recursive`
6. Click the "play" button in your XCode to rebuild

### Android

Many libraries in the React Native ecosystem include instructions to run `react-native link`. These are supported with ExpoKit for Android.
