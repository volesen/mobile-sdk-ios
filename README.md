![Jumio](docs/images/jumio_feature_graphic.jpg)

![Version](https://img.shields.io/github/v/release/Jumio/Mobile-SDK-IOS?style=flat)
![License](https://img.shields.io/cocoapods/l/JumioMobileSDK.svg?style=flat)
![Platform](https://img.shields.io/cocoapods/p/JumioMobileSDK.svg?style=flat)
[![Pod Version](https://img.shields.io/cocoapods/v/JumioMobileSDK.svg?style=flat)](https://cocoapods.org/pods/JumioMobileSDK)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Swift 3.0-5.x](http://img.shields.io/badge/Swift-3.x,%204.x%20&%205.x-orange.svg?style=flat)](https://swift.org/)

# Table of Contents
- [Overview](#overview)
- [Get Started](#get-started)
  - [ID Verification SDK](docs/integration_guide.md)
  - [Authentication SDK](https://github.com/Jumio/mobile-sdk-ios/blob/v3.9.4/docs/integration_authentication.md)
  - [Document Verification SDK](https://github.com/Jumio/mobile-sdk-ios/blob/v3.9.4/docs/integration_document-verification.md)
- [Quickstart](#quickstart)
- [Basics](#basics)
  - [General Requirements](#general-requirements)
  - [Authentication and Encryption](#authentication-and-encryption)
  - [Permissions](#permissions)
  - [Integration](#integration)
  - [App Thinning and Size Matters](#app-thinning-and-size-matters)
  - [Language Localization](#language-localization)
- [Security](#security)
- [Release Notes](#release-notes)
- [Support](#support)
- [Code Documentation](https://jumio.github.io/mobile-sdk-ios/Jumio/)
- [FAQ](docs/integration_faq.md)
- [Known Issues](docs/known_issues.md)

# Overview
The Jumio Software Development Kit (SDK) provides you with a set of tools and UIs (default or custom) to develop an iOS application perfectly fitted to your specific needs.

Onboard new users and easily verify their digital identities, by making sure the IDs provided by them are valid and authentic. Extract data from ID documents completely automatically and within seconds. Confirm users really are who they say they are by having them take a quick selfie and match it to their respective documents. Jumio uses cutting-edge biometric technology such as 3D face mapping to make sure there is an actual, real-life person in front of the screen.

![Menu Screen](docs/images/images_overview/intro_screen.png)  ![Scan Screen](docs/images/images_overview/menu_screen.png)  ![Confirm Screen](docs/images/images_overview/confirm_screen.png)

Using the Jumio SDK will allow you to create the best possible solution for your individual needs, providing you with a range of different services to choose from.

# Get Started
Please note that [basic setup](#basics) is required before continuing with the integration of any of the following services.

## Jumio ID Verification
ID Verification (formerly known as Netverify) is a secure and easy solution that allows you to establish the genuine identity of your users in your mobile application, by verifying their passports, government-issued IDs and VISA in real-time. Very user-friendly and highly customizable, it makes onboarding new customers quick and simple.

- [Integration ID Verification SDK](docs/integration_guide.md)

## Jumio Authentication
Authentication is a cutting-edge biometric-based service that establishes digital identities of your users, simply by taking a selfie. Advanced 3D face mapping-technology quickly and securely authenticates users and their digital identities.

- [Integration Authentication SDK (3.9.4, deprecated)](https://github.com/Jumio/mobile-sdk-ios/blob/v3.9.4/docs/integration_authentication.md)
- [Transition Guide Authentication SDK (3.9.4, deprecated)](https://github.com/Jumio/mobile-sdk-ios/blob/v3.9.0/docs/transition-guide_authentication.md)

## Jumio Document Verification
Document Verification is a powerful solution that allows users to scan various types of documents quickly and easily in your mobile application. Data extraction is already supported for various document types, such as bank statements.

- [Integration Document Verification SDK (3.9.4, deprecated)](https://github.com/Jumio/mobile-sdk-ios/blob/v3.9.4/docs/integration_document-verification.md)
- [Transition Guide Document Verification SDK (3.9.4, deprecated)](https://github.com/Jumio/mobile-sdk-ios/blob/v3.9.4/docs/transition-guide_document-verification.md)

# Quickstart
 This section provides a quick overview on how to get started with the [iOS sample application](sample) that can be found here on Github. You will require a __commercial Jumio License__ to successfully run any of our examples; for details, contact sales@jumio.com. You will also need a current Xcode version to open and try out the sample project.

Start by downloading the iOS sample application from the Jumio Github repo. You can do this either by cloning the repo (using SHH oder HTTPS) to your local device or simply downloading everything as a ZIP. Once you’ve got the sample application downloaded and unzipped if necessary, open Xcode. You’ll be faced with a couple of options. Choose __Open another project__ in the bottom right corner and navigate to where you’ve saved your sample application. Select the __SampleApp.xcodeproj__ and open it.

You also have the option of simply starting Xcode and choosing the option __Clone an existing project__ in the left-hand menu. In this case, you’ll need to add the URL of the [entire repository on Github](https://github.com/Jumio/mobile-sdk-ios). If prompted, choose __master__ and start cloning to your local device.

When the cloning is done, once again just choose the __SampleApp.xcodeproj__ and open it.

__Note:__ Our sample project on GitHub contains the sample implementation without our frameworks. The project contains a pre-action run script `jumio-sdk-checkout.sh`, which downloads our frameworks automatically during build time.

The iOS sample application contains two packages `CustomUI` and `DefaultUI`, as well as Delegates and the classes `ViewController.swift` and `ResultViewController.swift`. Use the ViewController class to either start CustomUI or DefaultUI by using a valid SDK token and data center.

If you haven't done so already, please refer to the [Authentication and Encryption section](#authentication-and-encryption) for more details on how to obtain your SDK token. Add your individual SDK token instead of the placeholder `""`. The default setting for the data center is `JumioDataCenter.US`.

⚠️&nbsp;&nbsp;__Note:__ We strongly recommend not storing any credentials inside your app! We suggest loading them during runtime from your server-side implementation.

In the `DefaultUI` package, you will find the class `DefaultUI.swift`. In the `CustomUI` package you will find:
* `ViewController` containing several ViewController classes
* `Handling` containing `ControllerHandling.swift`, `CredentialHandling.swift` and `ScanPartHandling.swift`
* `CustomUINavigationController.swift`

In each class, the most important methods for this service is shown and quickly outlined.

Once you start up the sample application, you'll be given the option of trying out the Jumio SDK. Select a service from the action bar at the bottom to try out different services. Your application will also need camera permission, which will be prompted for automatically once you try to start any of services.

# Basics

## General Requirements
The minimum requirements for the SDK are:
- iOS 11.0 and higher
- Internet connection

The following architectures are supported in the SDK:
- ARMv7
- ARM64
- x86_64 works on iOS emulator only

ℹ️&nbsp;&nbsp;__Note:__ Please note that currently, Apple machines using M1 will be able to build Jumio SDK for an actual device. Running on simulator is not possible.  

## Authentication and Encryption
Before starting a session in our SDK, an SDK token has to be obtained. Please refer to out [API Guide](https://github.com/Jumio/implementation-guides/blob/master/api-guide/api_guide.md) for further details. To authenticate against the API calls, an OAuth2 access token needs to be retrieved from the Customer Portal.

Within the response of the [Account Creation](https://github.com/Jumio/implementation-guides/blob/master/api-guide/api_guide.md#account-creation) or [Account Update](https://github.com/Jumio/implementation-guides/blob/master/api-guide/api_guide.md#account-update) API, an SDK token is returned, which needs to be applied to initiate the mobile SDK.

### Basic Authentication (Deprecated)
Previously, Basic Auth credentials were constructed using your API token as the User ID and your API secret as the password. You still can manage API token and secret in the Customer Portal under:
* __Settings > API credentials > API Users__

### Authentication with OAuth2
Your OAuth2 credentials are constructed using your API token as the Client ID and your API secret as the Client secret. You can view and manage your API token and secret in the Customer Portal under:
* __Settings > API credentials > OAuth2 Clients__

Client ID and Client secret are used to generate an OAuth2 access token. OAuth2 has to be activated for your account. Contact your Jumio Account Manager for activation.

#### Access Token URL (OAuth2)
* US: `https://auth.amer-1.jumio.ai/oauth2/token`
* EU: `https://auth.emea-1.jumio.ai/oauth2/token`
* SG: `https://auth.apac-1.jumio.ai/oauth2/token`

The [TLS Protocol](https://tools.ietf.org/html/rfc5246) is required to securely transmit your data, and we strongly recommend using the latest version. For information on cipher suites supported by Jumio during the TLS handshake see [supported cipher suites](https://github.com/Jumio/implementation-guides/blob/master/netverify/supported-cipher-suites.md).

ℹ️&nbsp;&nbsp; Calls with missing, incorrect or suspicious headers or parameter values will result in HTTP status code __400 Bad Request Error__ or __403 Forbidden__

#### Request Access Token (OAuth2)
```
curl --request POST --location 'https://auth.amer-1.jumio.ai/oauth2/token' \
    --header 'Accept: application/json' \
    --header 'Content-Type: application/x-www-form-urlencoded' \
    --data-raw 'grant_type=client_credentials' \
    --basic --user CLIENT_ID:CLIENT_SECRET
```

#### Response Access Token (OAuth2)
```
{
  "access_token": "YOUR_ACCESS_TOKEN",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

#### Access Token Timeout (OAuth2)
Your OAuth2 access token is valid for 60 minutes. After the token lifetime is expired, it is necessary to generate a new access token.

### Workflow Transaction Token Timeout
The token lifetime is set to 30 minutes per default. It can be configured via the [Jumio Customer Portal](https://github.com/Jumio/implementation-guides/blob/master/netverify/portal-settings.md) and can be overwritten using the API call (`tokenLifetime`). Within this token lifetime the token can be used to initialize the SDK.

As soon as the workflow (transaction) starts, a 15 minutes session timeout is triggered. For each action performed (capture image, upload image) the session timeout will reset, and the 15 minutes will start again.

After creating/updating a new account you will receive a `sdk.token` (JWT) for initializing the SDK. Use this SDK token with your iOS code:
```
sdk = Jumio.SDK()
sdk.token = "YOUR_SDK_TOKEN"
sdk.dataCenter = jumioDataCenter
```

## Permissions
The app’s Info.plist must contain the `NSCameraUsageDescription` key with a string value explaining to the user how the app uses this data. Example: *“This will allow <your-app-name> to take photos of your credentials."*

## Integration
Check the [Xcode sample project](sample) to learn the most common use. Make sure to use the device only frameworks for app submissions to the AppStore. Read more detailed information on this here: [Manual integration](/README.md#manually)

### Via Cocoapods
Jumio supports CocoaPods as dependency management tool for easy integration of the SDK. You are required to use **Cocoapods 1.11.0** or newer.

If you are not yet using Cocoapods in your project, first run:
```
sudo gem install cocoapods
pod init
```
Then update your local clone of the specs repo in Terminal to ensure that you are using the latest podspec files using:
```
pod repo update
```
Adapt your Podfile and add the pods according to the product(s) you want use. Check the following example how a Podfile could look like, with a list of all available Jumio pods:
```
source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '11.0'
use_frameworks! # Required for proper framework handling

pod 'Jumio/Slim', '~>4.0.0' # Use JumioSDK with manual capturing
pod 'Jumio/LineFinder', '~>4.0.0' # Use JumioSDK with manual capturing and linefinder functionality
pod 'Jumio/MRZ', '~>4.0.0' # Use JumioSDK with manual capturing and MRZ functionality
pod 'Jumio/Barcode', '~>4.0.0' # Use JumioSDK with manual capturing and barcode functionality
pod 'Jumio/Jumio', '~>4.0.0' # Use JumioSDK with all available scanning methods

pod 'Jumio/SlimLiveness', '~>4.0.0' # Use JumioSDK with manual capturing and liveness functionality
pod 'Jumio/LineFinderLiveness', '~>4.0.0' # Use JumioSDK with manual capturing, linefinder and liveness functionality
pod 'Jumio/MRZLiveness', '~>4.0.0' # Use JumioSDK with manual capturing, MRZ and liveness functionality
pod 'Jumio/BarcodeLiveness', '~>4.0.0' # Use JumioSDK with manual capturing, barcode and liveness functionality

pod 'Jumio/Liveness', '~>4.0.0' # Use JumioSDK with all available scanning methods and liveness functionality
```

#### Certified Liveness Vendor
Jumio uses Certified Liveness technology to determine liveness.
Please make sure to add the following post-install hook to your Podfile if you are using Jumio's liveness provider iProov:

```
pod 'Jumio/xxxLiveness'

# mandatory for all functionalities that include liveness (iProov)
post_install do |installer|
  installer.pods_project.targets.each do |target|
    if ['iProov', 'Socket.IO-Client-Swift', 'Starscream'].include? target.name
      target.build_configurations.each do |config|
          config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
      end
    end
  end
end
```

Install the pods to your project via Terminal:
```
pod install
```

### Via Carthage

##### ⚠️&nbsp;&nbsp;__Note:__ Please be aware that Carthage integration is not yet supported for SDK 4.0.0, but will be available for upcoming releases.  

Jumio supports Carthage as dependency management tool for easy integration of the SDK.

Adapt you Cartfile and add the JumioMobileSDK dependency. Check the following example how a Cartfile could look like:

```
binary "https://raw.githubusercontent.com/Jumio/mobile-sdk-ios/master/Carthage/JumioMobileSDK.json" == 4.x.x
```

Update you Carthage dependencies via Terminal:
```
carthage update
```

## App Thinning and Size Matters
App thinning (app slicing, bitcode and on-demand resources) is supported within the SDK. For app slicing, the image resources are placed within a xcassets collection. For ID Verification, some resource files (e.g. images) are loaded on demand.

In case you experience a build error when building your app in Debug configuration and aim to run it on a device, we advise to temporarily disable the build setting "Enable Bitcode" in your Xcode project.

### Manually
Download our frameworks manually via [ios-jumio-mobile-sdk-4.0.0.zip](https://mobile-sdk.jumio.com/com/jumio/ios/jumio-mobile-sdk/4.0.0/ios-jumio-mobile-sdk-4.0.0.zip).

__Using iProov (manually):__
* iProov.xcframework
* Starscream.framework (iProov dependency)
* SocketIO.framework (iProov dependency)

ℹ️&nbsp;&nbsp;__Note:__ Our sample project on GitHub contains the sample implementation without our frameworks. The project file contains a “Run Script Phase” which downloads our frameworks automatically during build time. In case your application uses ZoOm as a liveness vendor, please contact [Jumio support](https://support.jumio.com) or your account manager directly.

The Jumio Mobile SDK consists of several dynamic frameworks. Depending on which product you use, you'll have to add the right frameworks to your project.

Please see [Strip unused frameworks](docs/integration_faq.md#strip-unused-frameworks) for more information.

The framework binaries are available with support for device and simulator architecture. Make sure to remove the simulator architecture from our frameworks for app submissions to the AppStore. If this step is not performed, your submission will be rejected by Apple. Add the following code snippet as run script build phase to your app project and ensure that it is executed after the frameworks are embedded. Please see the required setup in our sample project.

ℹ️&nbsp;&nbsp;__Note:__ The simulator architecture is automatically removed if using Cocoapods via "[CP] Embed Pods Frameworks" build phase.

```shell
if [[ "$CONFIGURATION" == "Release" ]]; then
  $PROJECT_DIR/remove-simulator-architecture.sh
fi
```
Code snippet source: https://stackoverflow.com/questions/30547283/submit-to-app-store-issues-unsupported-architecture-x86

Add the following linker flags to your Xcode Build Settings:  
ℹ️&nbsp;&nbsp;__Note:__ Added automatically if using CocoaPods.
- "-lc++"
- "-ObjC" (recommended) or -all_load

Make sure that the following Xcode build settings in your app are set accordingly:

| Setting | Value |
| :--- | :---: |
| Link Frameworks Automatically | YES |

## Language Localization
Our SDK supports localization for different languages. All label texts and button titles can be changed and localized using the `Localizable-Jumio.strings` file. Just adapt the values to your required language, add it to your app or framework project and mark it as Localizable. This way, when upgrading our SDK to a newer version your localization file won't be overwritten. Make sure, that the content of this localization file is up to date after an SDK update.

ℹ️&nbsp;&nbsp;__Note:__ If using CocoaPods, the original file is located under `/Pods/Jumio/Localizations`.

Jumio SDK products support following languages for your convenience:

_Afrikaans, Arabic, Bulgarian, Chinese(Simplified), Chinese(Traditional), Croatian, Czech, Danish, Dutch, Estonian, English, Finnish, French, German, Greek, Hindi, Hungarian, Indonesian, Italian, Japanese, Khmer, Korean, Latvian, Lithuanian, Maltese, Norwegian, Polish, Portuguese, Romanian, Russian, Slovak, Slovenian, Spanish, Swedish, Thai, Turkish, Vietnamese, Zulu_

Please check out our [sample project](sample) to see how to use the strings files in your app.

Our SDK supports accessibility features. Visually impaired users can enable __VoiceOver__ or increase __text size__ on their device. VoiceOver uses separate values in the localization file, which can be customized.

# Security
All SDK related traffic is sent over HTTPS using TLS and public key pinning, and additionally, the information itself within the transmission is also encrypted utilizing __Application Layer Encryption__ (ALE). ALE is Jumio custom-designed security protocol which utilizes RSA-OAEP and AES-256 to ensure that the data cannot be read or manipulated even if the traffic was captured.

# Release Notes
Please refer to our [Change Log](docs/changelog.md) for more information about our current SDK version and further details.

# Support

## Previous Version
The previous release version 3.9.4 of the Jumio Mobile SDK is supported until 2022-06-01.

In case the support period is expired, no bug fixes and technical support are provided anymore. Current bugs are typically fixed in the upcoming versions.
Older SDK versions will keep functioning with our server until further notice, but we highly recommend to always update to the latest version to benefit from SDK improvements and bug fixes.

## Two-factor Authentication
If you want to enable two-factor authentication for your Jumio Customer Portal [please contact us.](https://support.jumio.com) Once enabled, users will be guided through the setup upon their first login to obtain a security code using the "Google Authenticator" app.

## Licenses
The software contains third-party open source software. For more information, please see [licenses](licenses).

This software is based in part on the work of the Independent JPEG Group.

## Contact
If you have any questions regarding our implementation guide please contact Jumio Customer Service at support@jumio.com. The Jumio online helpdesk contains a wealth of information regarding our service including demo videos, product descriptions, FAQs and other things that may help to get you started with Jumio. [Check it out at here](https://support.jumio.com).

## Copyright
&copy; Jumio Corporation, 395 Page Mill Road, Suite 150, Palo Alto, CA 94306

The source code and software available on this website (“Software”) is provided by Jumio Corp. or its affiliated group companies (“Jumio”) "as is” and any express or implied warranties, including, but not limited to, the implied warranties of merchantability and fitness for a particular purpose are disclaimed. In no event shall Jumio be liable for any direct, indirect, incidental, special, exemplary, or consequential damages (including but not limited to procurement of substitute goods or services, loss of use, data, profits, or business interruption) however caused and on any theory of liability, whether in contract, strict liability, or tort (including negligence or otherwise) arising in any way out of the use of this Software, even if advised of the possibility of such damage.
In any case, your use of this Software is subject to the terms and conditions that apply to your contractual relationship with Jumio. As regards Jumio’s privacy practices, please see our privacy notice available here: [Privacy Policy](https://www.jumio.com/legal-information/privacy-policy/).
