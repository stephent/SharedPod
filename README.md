# SharedPod
Demo project for StackOverflow question relating to sharing a pod between an app and an embedded framework.

## Scenario

I have an iOS app (MyApp) and a CocoaTouch Framework (MyFramework). MyApp embeds MyFramework (under Embedded Binaries in the MyApp Target General screen).

The project uses CocoaPods to manage dependencies.

Both MyFramework and MyApp need some common pod dependencies.

## Problems Encountered

### Duplicate symbols
When the app is run, it appears that the shared pods are linked twice. Xcode shows the following output:

```
objc[38118]: Class PLBuildVersion is implemented in both /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/System/Library/PrivateFrameworks/AssetsLibraryServices.framework/AssetsLibraryServices (0x11361e998) and /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/System/Library/PrivateFrameworks/PhotoLibraryServices.framework/PhotoLibraryServices (0x11339d880). One of the two will be used. Which one is undefined.
objc[38118]: Class FIRAAppEnvironmentUtil is implemented in both /Users/stephen/Library/Developer/Xcode/DerivedData/SharedPod-dmfilgmzenswfqfubfkmrncnprxs/Build/Products/Debug-iphonesimulator/MyFramework.framework/MyFramework (0x10eaf7860) and /Users/stephen/Library/Developer/CoreSimulator/Devices/28281A7F-3A00-4E1D-86E5-BE1E80016FCF/data/Containers/Bundle/Application/146D17D0-08A4-485E-9661-CE97A00CAEA2/MyApp.app/MyApp (0x10b58fa10). One of the two will be used. Which one is undefined.
objc[38118]: Class FIRAAppDelegateProxy is implemented in both /Users/stephen/Library/Developer/Xcode/DerivedData/SharedPod-dmfilgmzenswfqfubfkmrncnprxs/Build/Products/Debug-iphonesimulator/MyFramework.framework/MyFramework (0x10eaf78b0) and /Users/stephen/Library/Developer/CoreSimulator/Devices/28281A7F-3A00-4E1D-86E5-BE1E80016FCF/data/Containers/Bundle/Application/146D17D0-08A4-485E-9661-CE97A00CAEA2/MyApp.app/MyApp (0x10b58fa60). One of the two will be used. Which one is undefined.
```

### Cocoapods warning
On running `pod install`, the following warning output is generated:

```
[!] The Podfile contains framework targets, for which the Podfile does not contain host targets (targets which embed the framework).
If this project is for doing framework development, you can ignore this message. Otherwise, add a target to the Podfile that embeds these frameworks to make this message go away (e.g. a test target).
```

## Question

How can I change the Podfile and/or project settings so as to avoid the problems described above?



