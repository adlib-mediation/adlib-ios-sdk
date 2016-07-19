# adlib-ios-sdk
AdLib iOS SDK


##AdLib SDK for iOS
###Setup AdLib

1.	There are two Adlib.framework files in this SDK, one for using the iOS Simulator, and one for your device. To test your project on an iOS device and to submit your project to iTunes Connect, use the framework under SDK/Device. To test your project on the simulator, use the framework under SDK/simulator. 

2.	Drag and drop or manually add the according Adlib.framework file under the Embedded Binaries section in your project's target General settings. 


![xcode screenshot](https://github.com/adlib2015/adlib-unity/blob/master/Xcode.png "Xcode")

3.	To initialize Adlib, use the following code and provide the client with your App ID. 

```Objective-C
AdlibClient *adlibClient = [AdlibClient sharedClient];
[adlibClient startWithAppId:@"<Your APP ID>" delegate:self];
```

###Demographic Parameters
AdLib accepts the following demographic parameters, which you should set when available:

```Objective-C
[adlibClient setAge: 21];
[adlibClient setGender: AMAdQueryGenderFemale];
[adlibClient setMaritalStatus: AMAdQueryMaritalStatusSingle];
[adlibClient setZip: @"12345"];
[adlibClient setIncome: 75000];
[adlibClient setLocation: myCLLocation];
[adlibClient setCountry: @"Canada"];
```
You can also request that AdLib capture location updates itself:

```Objective-C
[adlibClient updateLocation];
```

###Banner Ads

1. Add an AMBannerView to your View Controller and initialize it with your Ad Unit ID.

```Objective-C
bannerView.unitId = @"<Your Ad Unit ID>";
bannerView.rootViewController = self;
bannerView.delegate = self;
```
2. To start loading ads, see the following code: 

```Objective-C
[bannerView loadAd];
```

###Banner Ads Delegate

Set an AMBannerViewDelegate to receive a callback when an ad loads, is clicked or receives an error.

```Objective-C
(void)bannerView:(AMBannerView *)bannerView didReceiveBannerWithNetwork:(NSString *)networkName;
(void)bannerViewFailedToLoadBanner:(AMBannerView *)bannerView error:(NSError *)error;
(void)bannerView:(AMBannerView *)bannerView didTapBannerViewWithNetwork:(NSString *)networkName;
```


###Interstitial Ads

1. Add an AMInterstitialView to your View Controller and initialize it with your Ad Unit ID.

```Objective-C
interstitialView.unitId = @"<Your Ad Unit ID>";
interstitialView.rootViewController = self;
interstitialView.delegate = self;
```
2. To load an interstitial ad, use the loadAd function. You must call this function every time you would like to load a new interstitial, as it does not load automatically.

```Objective-C
[interstitialView loadAd];
```

3. To show an interstitial ad, use the showAd function. An interstitial must be loaded before showing an ad, so it may be a good idea to utilize the interstitial delegate function didReceiveInterstitialWithNetwork.

```Objective-C
[interstitialView showAd];
```

###Interstitial Ads Delegate

Set an AMInterstitialViewDelegate to receive a callback when an ad loads, shows, is clicked, is dismissed, receives an error, fails to load, or fails to show.

```Objective-C
(void)interstitialView:(AMInterstitialView *)interstitialView didReceiveInterstitialWithNetwork:(NSString *)networkName
(void)interstitialView:(AMInterstitialView *)interstitialView didShowInterstitialWithNetwork:(NSString *)networkName
(void)interstitialViewFailedToShowInterstitial:(AMInterstitialView *)interstitialView error:(NSError *)error
(void)interstitialViewFailedToLoadInterstitial:(AMInterstitialView *)interstitialView error:(NSError *)error
(void)interstitialView:(AMInterstitialView *)interstitialView didTapInterstitialViewWithNetwork:(NSString *)networkName
(void)interstitialView:(AMInterstitialView *)interstitialView didDismissInterstitialViewWithNetwork:(NSString *)networkName
```
