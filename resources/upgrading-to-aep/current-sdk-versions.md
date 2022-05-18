# Current SDK Versions

{% hint style="info" %}
## Swift SDKs are here!

We've released Swift versions of our iOS SDKs for Core and select extensions - please [scroll down](current-sdk-versions.md#ios-swift) for available Swift extensions and reference documentation for more information.
{% endhint %}

{% hint style="warning" %}
## Migrate to Swift

If you are currently using our Objective-C \(ACP-prefix libraries\), please see the [Migrating to Swift](../migrate-to-swift.md) guide for next steps.
{% endhint %}

## Android

{% hint style="warning" %}
Adobe Experience Platform Mobile SDK for Android supports Google Android API 14 \(Ice Cream Sandwich\) or later. The Adobe Experience Platform Edge Network extension and other **for Edge Network** extensions require Android versions 4.4 or later \(API levels 19 or later\).
{% endhint %}

{% hint style="info" %}
Due to sunset of [JCenter by JFrog](https://jfrog.com/blog/into-the-sunset-bintray-jcenter-gocenter-and-chartcenter/), our SDKs are no longer being uploaded to JCenter. Android libraries are now available on [MavenCentral](https://search.maven.org/search?q=g:com.adobe.marketing.mobile). For more information, see links below or find [our libraries on MavenCentral](https://search.maven.org/search?q=g:com.adobe.marketing.mobile). For more information on how to declare dependencies from Maven, please see [Declaring repositories](https://docs.gradle.org/current/userguide/declaring_repositories.html#sec:declaring_multiple_repositories) on Gradle.
{% endhint %}

| Extension | Maven | Github |
| :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/core.svg?logo=android&logoColor=white&label=core&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/core) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Profile](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/userprofile.svg?logo=android&logoColor=white&label=userprofile&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/userprofile) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Identity](../../foundation-extensions/mobile-core/identity/) | Bundled in Mobile Core | — |
| [Signal](../../foundation-extensions/mobile-core/signals/) | Bundled in Mobile Core | — |
| [Lifecycle](../../foundation-extensions/mobile-core/lifecycle/) | Bundled in Mobile Core | — |
| [Rules Engine](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/rules-engine) | Bundled in Mobile Core | — |
| [Adobe Experience Platform Edge Network](../../foundation-extensions/experience-platform-extension/) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/edge.svg?logo=android&logoColor=white&label=edge&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/edge) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Identity for Edge Network](../../foundation-extensions/identity-for-edge-network/) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/edgeidentity.svg?logo=android&logoColor=white&label=edgeidentity&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/edgeidentity) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Consent for Edge Network](../../foundation-extensions/consent-for-edge-network/) | [​![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/edgeconsent.svg?logo=android&logoColor=white&label=edgeconsent&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/edgeconsent) | [Link](https://github.com/adobe/aepsdk-edgeidentity-android) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/assurance.svg?logo=android&logoColor=white)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/assurance) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/places.svg?logo=android&logoColor=white&label=places&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/places) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Places Monitor](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.html?lang=en) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/places-monitor.svg?logo=android&logoColor=white&label=placesmonitor&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/places-monitor) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/analytics.svg?logo=android&logoColor=white&label=analytics&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/analytics) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Analytics - Media Analytics for Audio & Video](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/media.svg?logo=android&logoColor=white&label=media&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/media) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-audience-manager) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/audience.svg?logo=android&logoColor=white&label=audience&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/audience) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/mobileservices.svg?logo=android&logoColor=white&label=mobileservices&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/mobileservices) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Journey Optimizer](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/messaging.svg?logo=android&logoColor=white&label=messaging&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/messaging) | [Link](https://github.com/adobe/aepsdk-messaging-android) |
| [Adobe Target](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/target.svg?logo=android&logoColor=white&label=target&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/target) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Campaign Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/campaign.svg?logo=android&logoColor=white&label=campaign&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/campaign) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |
| [Adobe Campaign Classic](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaignclassic) | [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/campaignclassic.svg?logo=android&logoColor=white&label=campaignclassic&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/campaignclassic) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) |

## iOS — Swift

{% hint style="warning" %}

## Migrate to Swift

If you are currently using our Objective-C (ACP-prefix) libraries, please see the [Migrating to Swift](../migrate-to-swift.md) guide for next steps.

Adobe Experience Platform Mobile SDK for iOS supports iOS 10 or later; requires Swift 5.1 or newer and Xcode 11.0 or newer. In addition to **CocoaPods**, **Swift Package Manager (SPM)** installation option is supported with the latest iOS Swift SDKs! Find more details at the GitHub links below.

{% endhint %}

{% hint style="info" %}

## Swift = Open Source

The Swift iOS SDKs are open source - read more about [our move to Swift and open source](https://medium.com/adobetech/adobe-experience-platform-mobile-sdks-move-to-swift-for-ios-6aa67b67b4d4).

{% endhint %}

| Extension | App Extension | CocoaPods | GitHub |
| :--- | :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | ✔️ | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPCore.svg?color=orange&label=AEPCore&logo=apple&logoColor=white&style=flat-square)​](https://cocoapods.org/pods/AEPCore) | [Link](https://github.com/adobe/aepsdk-core-ios) |
| [Profile](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPUserProfile.svg?color=orange&label=AEPUserProfile&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPUserProfile) | [Link](https://github.com/adobe/aepsdk-userprofile-ios) |
| [Identity](../../foundation-extensions/mobile-core/identity/) | ✔️ | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPIdentity.svg?color=orange&label=AEPIdentity&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPIdentity) | [Link](https://github.com/adobe/aepsdk-core-ios) |
| [Signal](../../foundation-extensions/mobile-core/signals/) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPSignal.svg?color=orange&label=AEPSignal&logo=apple&logoColor=white&style=flat-square)​](https://cocoapods.org/pods/AEPSignal) | [Link](https://github.com/adobe/aepsdk-core-ios) |
| [Lifecycle](../../foundation-extensions/mobile-core/lifecycle/) | ✔️ | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPLifecycle.svg?color=orange&label=AEPLifecycle&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPLifecycle) | [Link](https://github.com/adobe/aepsdk-core-ios) |
| [Rules Engine](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/rules-engine) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPRulesEngine.svg?color=orange&label=AEPRulesEngine&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPRulesEngine) | [Link](https://github.com/adobe/aepsdk-rulesengine-ios) |
| [Adobe Experience Platform Edge Network](../../foundation-extensions/experience-platform-extension/) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPEdge.svg?color=orange&label=AEPEdge&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPEdge) | [Link](https://github.com/adobe/aepsdk-edge-ios) |
| [Identity for Edge Network](../../foundation-extensions/identity-for-edge-network/) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPEdgeIdentity.svg?color=orange&label=AEPEdgeIdentity&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPEdgeIdentity) | [Link](https://github.com/adobe/aepsdk-edgeidentity-ios) |
| [Consent for Edge Network](../../foundation-extensions/consent-for-edge-network/) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPEdgeConsent.svg?color=orange&label=AEPEdgeConsent&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPEdgeConsent) | [Link](https://github.com/adobe/aepsdk-edgeconsent-ios) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPAssurance.svg?color=orange&label=AEPAssurance&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPAssurance) | [Link](https://github.com/adobe/aepsdk-assurance-ios) |
| [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPPlaces.svg?color=orange&label=AEPPlaces&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPPlaces) | [Link](https://github.com/adobe/aepsdk-places-ios) |
| [Places Monitor](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.html?lang=en) |  | Releasing Soon |  |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | ✔️ | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPAnalytics.svg?color=orange&label=AEPAnalytics&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPAnalytics) | [Link](https://github.com/adobe/aepsdk-analytics-ios) |
| [Adobe Analytics - Media Analytics for Audio & Video](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPMedia.svg?color=orange&label=AEPMedia&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPMedia) | [Link](https://github.com/adobe/aepsdk-media-ios) |
| [Adobe Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-audience-manager) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPAudience.svg?color=orange&label=AEPAudience&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPAudience) | [Link](https://github.com/adobe/aepsdk-audience-ios) |
| [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPMobileServices.svg?color=orange&label=AEPMobileServices&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPMobileServices) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/AEPMobileServices) |
| [Adobe Journey Optimizer](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPMessaging.svg?color=orange&label=AEPMessaging&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPMessaging) | [Link](https://github.com/adobe/aepsdk-messaging-ios) |
| [Adobe Target](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPTarget.svg?color=orange&label=AEPTarget&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPTarget) | [Link](https://github.com/adobe/aepsdk-target-ios) |
| [Adobe Campaign Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) |  | [![Cocoapods](https://img.shields.io/cocoapods/v/AEPCampaign.svg?color=orange&label=AEPCampaign&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/AEPMCampaign) | [Link](https://github.com/adobe/aepsdk-campaign-ios) |
| [Adobe Campaign Classic](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaignclassic) |  | To Be Determined |  |

## iOS — Objective-C

{% hint style="warning" %}
Adobe Experience Platform Mobile SDK for iOS supports iOS 10 or later (includes support for iOS, iPadOS, and tvOS).
{% endhint %}

| Extension | CocoaPods | GitHub |
| :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) \(supports tvOS\) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPCore.svg?color=orange&label=ACPCore&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPCore) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPCore) |
| [Profile](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPUserProfile.svg?color=orange&label=ACPUserProfile&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPUserProfile) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPUserProfile) |
| [Identity](../../foundation-extensions/mobile-core/identity/) | Bundled in Mobile Core | — |
| [Signal](../../foundation-extensions/mobile-core/signals/) | Bundled in Mobile Core | — |
| [Lifecycle](../../foundation-extensions/mobile-core/lifecycle/) | Bundled in Mobile Core | — |
| [Rules Engine](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/rules-engine) | Bundled in Mobile Core | — |
| [Adobe Experience Platform Edge Network](../../foundation-extensions/experience-platform-extension/) | Not Available | — |
| [Identity for Edge Network](../../foundation-extensions/identity-for-edge-network/) | Not Available | — |
| [Consent for Edge Network](../../foundation-extensions/consent-for-edge-network/) | Not Available | — |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [![Cocoapods](https://img.shields.io/badge/AEPAssurance-v1.1.3-orange?logo=apple&style=flat-square)](https://cocoapods.org/pods/AEPAssurance) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/AEPAssurance) |
| [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPPlaces.svg?color=orange&label=ACPPlaces&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPPlaces) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPPlaces) |
| [Places Monitor](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.html?lang=en) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPPlacesMonitor.svg?color=orange&label=ACPPlacesMonitor&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPPlacesMonitor) | [Link](https://github.com/adobe/places-monitor-ios) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) \(supports tvOS\) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPAnalytics.svg?color=orange&label=ACPAnalytics&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPAnalytics) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPAnalytics) |
| [Adobe Analytics - Media Analytics for Audio & Video](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) \(supports tvOS\) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPMedia.svg?color=orange&label=ACPMedia&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPMedia) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPMedia) |
| [Adobe Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-audience-manager) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPAudience.svg?color=orange&label=ACPAudience&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPAudience) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPAudience) |
| [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPMobileServices.svg?color=orange&label=ACPMobileServices&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPMobileServices) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.0-ACPMobileServices) |
| [Adobe Target](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPTarget.svg?color=orange&label=ACPTarget&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPTarget) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPTarget) |
| [Adobe Campaign Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPCampaign.svg?color=orange&label=ACPCampaign&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPCampaign) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPCampaign) |
| [Adobe Campaign Classic](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaignclassic) | [![Cocoapods](https://img.shields.io/cocoapods/v/ACPCampaignClassic.svg?color=orange&label=ACPCampaignClassic&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPCampaignClassic) | [Link](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS/ACPCampaignClassic) |

## React Native (AEP 1.x) <a id="react-native-aep"></a>

Adobe Experience Platform Mobile SDK plugin for React Native supports React Native **version 0.60.0 or later**. For the latest installation instructions, see the `README` file in the [`aepsdk-react-native`](https://github.com/adobe/aepsdk-react-native#installation) repository.

{% hint style="danger" %}
Adobe Experience Platform Mobile SDK plugins (AEP 1.x) for React Native are compatible only with [Android](current-sdk-versions.md#android) and [iOS — Swift](current-sdk-versions#ios-swift) libraries.
{% endhint %}

{% hint style="info" %}
If you are currently using our ACP-prefix React Native libraries, please see [the guide to migrate to the Experience Platform SDK libraries (AEP 1.x)](https://github.com/adobe/aepsdk-react-native/blob/main/docs/migration.md) for React Native.
{% endhint %}

| Extension | npmjs |
| ---- | ---- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) |[![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepcore.svg?color=green&label=%40adobe%2Freact-native-aepcore&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepcore)   |
|  [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile)   |   [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepuserprofile.svg?color=green&label=%40adobe%2Freact-native-aepuserprofile&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepuserprofile) |
|  [Edge](https://aep-sdks.gitbook.io/docs/foundation-extensions/experience-platform-extension)    |   [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepedge.svg?color=green&label=%40adobe%2Freact-native-aepedge&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepedge)   |
|  [EdgeIdentity](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network)    |     [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepedgeidentity.svg?color=green&label=%40adobe%2Freact-native-aepedgeidentity&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepedgeidentity)  |
|  [EdgeConsent](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network)    |   [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepedgeconsent.svg?color=green&label=%40adobe%2Freact-native-aepedgeconsent&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepedgeconsent)  |
|  [Messaging](https://aep-sdks.gitbook.io/docs/beta/iam)  |   [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepmessaging.svg?color=green&label=%40adobe%2Freact-native-aepmessaging&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepmessaging)   |
|  [assurance](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance)    |  [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepassurance.svg?color=green&label=%40adobe%2Freact-native-aepassurance&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepassurance)  |



## React Native (ACP 2.x) <a id="react-native-acp"></a>

Adobe Experience Platform Mobile SDK plugin for React Native supports React Native **version 0.60.0 or later**. For the latest installation instructions, see the `README` file in the [`react-native-acpcore`](https://github.com/adobe/react-native-acpcore) repository.

{% hint style="danger" %}
Adobe Experience Platform Mobile SDK plugins (ACP 2.x) for React Native are compatible only with [Android](current-sdk-versions.md#android) and [iOS — Objective-C](current-sdk-versions#ios-objective-c) libraries.
{% endhint %}

{% hint style="info" %}
For React Native, we recommend that you first install [Node.js](https://nodejs.org/en/) to download packages from [npm](https://npm.io/). For additional instructions on getting started with React Native applications, see this [tutorial](https://reactnative.dev/docs/getting-started).
{% endhint %}

| Extension | npmjs | Github | Sample |
| :--- | :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpcore.svg?color=green&label=%40adobe%2Freact-native-acpcore&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpcore) | [Link](https://github.com/adobe/react-native-acpcore) | [Sample](https://github.com/adobe/react-native-acpcore/tree/main/sample/ACPCoreSampleApp) |
| [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpuserprofile.svg?color=green&label=%40adobe%2Freact-native-acpuserprofile&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpuserprofile) | [Link](https://github.com/adobe/react-native-acpuserprofile) | [Sample](https://github.com/adobe/react-native-acpuserprofile/tree/main/sample/ACPUserProfileSampleApp) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-aepassurance.svg?color=green&label=%40adobe%2Freact-native-aepassurance&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-aepassurance) | [Link](https://github.com/adobe/react-native-aepassurance) | [Sample](https://github.com/adobe/react-native-aepassurance/tree/main/SampleApp) |
| [Places Service](https://docs.adobe.com/content/help/en/places/using/home.html) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpplaces.svg?color=green&label=%40adobe%2Freact-native-acpplaces&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpplaces) | [Link](https://github.com/adobe/react-native-acpplaces) | [Sample](https://github.com/adobe/react-native-acpplaces/tree/main/sample/ACPPlacesSampleApp) |
| [Places Monitor](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.html) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpplaces-monitor.svg?color=green&label=%40adobe%2Freact-native-acpplaces-monitor&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpplaces-monitor) | [Link](https://github.com/adobe/react-native-acpplaces-monitor) | [Sample](https://github.com/adobe/react-native-acpplaces-monitor/tree/main/sample/ACPPlacesMonitorSample) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpanalytics.svg?color=green&label=%40adobe%2Freact-native-acpanalytics&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpanalytics) | [Link](https://github.com/adobe/react-native-acpanalytics) | [Sample](https://github.com/adobe/react-native-acpanalytics/tree/main/sample/ACPAnalyticsSampleApp) |
| [Adobe Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpmedia.svg?color=green&label=%40adobe%2Freact-native-acpmedia&logo=npm&style=flat-square)](https://www.npmjs.com/package/@adobe/react-native-acpmedia) | [Link](https://github.com/adobe/react-native-acpmedia) | [Sample](https://github.com/adobe/react-native-acpmedia/tree/main/sample/ACPMediaSampleApp) |
| [Adobe Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-audience-manager) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpaudience.svg?color=green&label=%40adobe%2Freact-native-acpaudience&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpaudience) | [Link](https://github.com/adobe/react-native-acpaudience) | [Sample](https://github.com/adobe/react-native-acpaudience/tree/main/sample/ACPAudienceSampleApp) |
| [Adobe Target](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acptarget.svg?color=green&label=%40adobe%2Freact-native-acptarget&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acptarget) | [Link](https://github.com/adobe/react-native-acptarget) | [Sample](https://github.com/adobe/react-native-acptarget/tree/main/sample/ACPTargetSampleApp) |
| [Adobe Campaign Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) | [![npm version](https://img.shields.io/npm/v/@adobe/react-native-acpcampaign.svg?color=green&label=%40adobe%2Freact-native-acpcampaign&logo=npm&style=flat-square)](https://badge.fury.io/js/%40adobe%2Freact-native-acpcampaign) | [Link](https://github.com/adobe/react-native-acpcampaign) | [Sample](https://github.com/adobe/react-native-acpcampaign/tree/main/sample/ACPCampaignSampleApp) |

{% hint style="info" %}
Beta versions of React Native Experience Platform Edge Network, Edge Identity, Edge Consent, Messaging and Assurance can be found in the repository link [here](https://github.com/adobe/aepsdk-react-native). These new beta extensions require the latest AEP Core to opperate. See [`README`](https://github.com/adobe/aepsdk-react-native/blob/main/README.md) for further information on installation and configuration.
{% endhint %}

## Cordova

Adobe Experience Platform Mobile SDK plugins for Cordova supports Cordova **versions 9.0.0 or later**. For the latest Cordova installation instructions, see the `README` file in the [`cordova-acpcore`](https://github.com/adobe/cordova-acpcore) repository.

{% hint style="danger" %}
Adobe Experience Platform Mobile SDK plugins for Cordova are compatible only with [Android](current-sdk-versions.md#android) and [iOS — Objective-C](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#ios-objective-c) libraries, at this time.
{% endhint %}

A sample Cordova application that uses the Adobe Experience Platform Mobile SDK can be found [here](https://github.com/adobe/cordova-acpsample).

{% hint style="info" %}
For Cordova, we recommend that you first install [Node.js](https://nodejs.org/en/) to download packages from npm. For additional instructions on getting started with Cordova applications, see this [guide](https://netbeans.apache.org/kb/docs/webclient/cordova-gettingstarted.html).
{% endhint %}

With Node.js installed, you may install the Cordova framework from terminal using the following statement:

```text
sudo npm install -g cordova
```

To start using the Adobe Experience Platform Mobile SDK plugin for Cordova, navigate to the directory of your Cordova app and install the plugin\(s\) using the following statement:

```text
cordova plugin add https://github.com/adobe/cordova-acpcore.git
```

| Extension | npmjs | Github |
| :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | [![npm](https://img.shields.io/npm/v/@adobe/cordova-acpcore?label=cordova-acpcore&logo=npm)](https://www.npmjs.com/package/@adobe/cordova-acpcore) | [Link](https://github.com/adobe/cordova-acpcore) |
| [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile#cordova) | [![npm](https://img.shields.io/npm/v/@adobe/cordova-acpuserprofile?label=cordova-acpuserprofile&logo=npm)](https://www.npmjs.com/package/@adobe/cordova-acpuserprofile) | [Link](https://github.com/adobe/cordova-acpuserprofile) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [![npm](https://img.shields.io/npm/v/@adobe/cordova-aepassurance?label=cordova-aepassurance&logo=npm)](https://www.npmjs.com/package/@adobe/cordova-aepassurance) | [Link](https://github.com/adobe/cordova-aepassurance) |
| [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en) | [![npm](https://img.shields.io/npm/v/@adobe/cordova-acpplaces?label=cordova-acpplaces&logo=npm)](https://www.npmjs.com/package/@adobe/cordova-acpplaces) | [Link](https://github.com/adobe/cordova-acpplaces) |
| [Places Monitor](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.html?lang=en) | [![npm](https://img.shields.io/npm/v/@adobe/cordova-acpplacesmonitor?label=cordova-acpplacesmonitor&logo=npm)](https://www.npmjs.com/package/@adobe/cordova-acpplacesmonitor) | [Link](https://github.com/adobe/cordova-acpplaces-monitor) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | [![npm](https://img.shields.io/npm/v/@adobe/cordova-acpanalytics?label=cordova-acpanalytics&logo=npm)](https://www.npmjs.com/package/@adobe/cordova-acpanalytics) | [Link](https://github.com/adobe/cordova-acpanalytics) |

## Flutter

Adobe Experience Platform Mobile SDK plugin for Flutter supports Flutter **versions 1.10.0 or later**.

{% hint style="danger" %}
Adobe Experience Platform Mobile SDK plugins for Flutter are compatible only with [Android](current-sdk-versions.md#android) and [iOS — Objective-C](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#ios-objective-c) libraries, at this time.
{% endhint %}

| Extension | pub.dev | Github | Sample App |
| :--- | :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | [![pub package](https://img.shields.io/pub/v/flutter_acpcore.svg)](https://pub.dartlang.org/packages/flutter_acpcore) | [Link](https://github.com/adobe/flutter_acpcore) | [Sample](https://github.com/adobe/flutter_acpcore/tree/master/example) |
| [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile#flutter) | [![pub package](https://img.shields.io/pub/v/flutter_acpuserprofile.svg)](https://pub.dartlang.org/packages/flutter_acpuserprofile) | [Link](https://github.com/adobe/flutter-acpuserprofile) | [Sample](https://github.com/adobe/flutter_acpuserprofile/tree/master/example) |
| [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en) | [![pub package](https://img.shields.io/pub/v/flutter_acpplaces.svg)](https://pub.dartlang.org/packages/flutter_acpplaces) | [Link](https://github.com/adobe/flutter-acpplaces) | [Sample](https://github.com/adobe/flutter_acpplaces/tree/master/example) |
| [Places Monitor](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.html?lang=en) | [![pub package](https://img.shields.io/pub/v/flutter_acpplaces_monitor.svg)](https://pub.dartlang.org/packages/flutter_acpplaces_monitor) | [Link](https://github.com/adobe/flutter-acpplaces_monitor) | [Sample](https://github.com/adobe/flutter_acpplaces_monitor/tree/master/example) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [![pub package](https://img.shields.io/pub/v/flutter_assurance.svg)](https://pub.dartlang.org/packages/flutter_assurance) | [Link](https://github.com/adobe/flutter_assurance) | [Sample](https://github.com/adobe/flutter_assurance/tree/master/example) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | [![pub package](https://img.shields.io/pub/v/flutter_acpanalytics.svg)](https://pub.dartlang.org/packages/flutter_acpanalytics) | [Link](https://github.com/adobe/flutter_acpanalytics) | [Sample](https://github.com/adobe/flutter_acpanalytics/tree/master/example) |

## Xamarin

Adobe Experience Platform Mobile SDK plugins for Xamarin require **MonoAndroid 9.0+ and Xamarin.iOS 1.0+**. For the latest Xamarin installation instructions, see the `README` file in the [`xamarin-acpcore`](https://github.com/adobe/xamarin-acpcore) repository.

{% hint style="danger" %}
Adobe Experience Platform Mobile SDK plugins for Xamarin are compatible only with [Android](current-sdk-versions.md#android) and [iOS — Objective-C](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#ios-objective-c) libraries, at this time.
{% endhint %}

{% hint style="info" %}
The Adobe Experience Platform Mobile SDK plugins for Xamarin are packages distributed via [nuget](https://www.nuget.org/packages). NuGet packages can be added to projects within a [Visual Studio](https://visualstudio.microsoft.com/downloads/) solution. The NuGet packages can also be generated locally via the included Makefile located in each of the Xamarin repositories.
{% endhint %}

| Extension | Android | iOS | Github |
| :--- | :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPCore.Android?label=Adobe.ACPCore.Android&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPCore.Android/) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPCore.iOS?label=Adobe.ACPCore.iOS&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPCore.iOS/) | [Link](https://github.com/adobe/xamarin-acpcore) |
| [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile#xamarin) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPUserProfile.Android?label=Adobe.ACPUserProfile.Android&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPUserProfile.Android/) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPUserProfile.iOS?label=Adobe.ACPUserProfile.iOS&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPUserProfile.iOS/) | [Link](https://github.com/adobe/xamarin-acpuserprofile) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [![Nuget](https://img.shields.io/nuget/v/Adobe.AEPAssurance.Android?label=Adobe.AEPAssurance.Android&logo=xamarin)](https://www.nuget.org/packages/Adobe.AEPAssurance.Android/) | [![Nuget](https://img.shields.io/nuget/v/Adobe.AEPAssurance.iOS?label=Adobe.AEPAssurance.iOS&logo=xamarin)](https://www.nuget.org/packages/Adobe.AEPAssurance.iOS/) | [Link](https://github.com/adobe/xamarin-aepassurance) |
| [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPPlaces.Android?label=Adobe.ACPPlaces.Android&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPPlaces.Android/) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPPlaces.iOS?label=Adobe.ACPPlaces.iOS&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPPlaces.iOS/) | [Link](https://github.com/adobe/xamarin-acpcore) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPAnalytics.Android?label=Adobe.ACPAnalytics.Android&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPAnalytics.Android/) | [![Nuget](https://img.shields.io/nuget/v/Adobe.ACPAnalytics.iOS?label=Adobe.ACPAnalytics.iOS&logo=xamarin)](https://www.nuget.org/packages/Adobe.ACPAnalytics.iOS/) | [Link](https://github.com/adobe/xamarin-acpanalytics) |

## Unity

{% hint style="warning" %}
Effective March 30, 2022, support for Adobe Experience Platform Mobile SDKs on Unity is no longer active. While you may continue using our libraries, Adobe no longer plans to update, modify, or provide support for these libraries. Please contact your Adobe CSM for details.
{% endhint %}

Adobe Experience Platform Mobile SDK plugin for Unity supports Unity **version 2019.4.34f1**. For the latest Unity installation instructions, see the `README` file in the [`unity-acpcore`](https://github.com/adobe/unity-acpcore) repository.

{% hint style="danger" %}
Adobe Experience Platform Mobile SDK plugins for Unity are compatible only with [Android](current-sdk-versions.md#android) and [iOS — Objective-C](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#ios-objective-c) libraries, at this time.
{% endhint %}

To start using the Adobe Experience Platform Mobile SDK for Unity, open your application and import the following Unity package\(s\):

| Extension | Github | Sample App |
| :--- | :--- | :--- |
| [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) | [Link](https://github.com/adobe/unity-acpcore/tree/master/bin) | [Sample](https://github.com/adobe/unity-acpcore#sample-app) |
| [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) | [Link](https://github.com/adobe/unity-aepassurance/tree/master/bin) | [Sample](https://github.com/adobe/unity-aepassurance#sample-app) |
| [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) | [Link](https://github.com/adobe/unity-acpanalytics/tree/master/bin) | [Sample](https://github.com/adobe/unity-acpanalytics#sample-app) |
| [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) | [Link](https://github.com/adobe/unity_acpuserprofile/tree/master/bin) | [Sample](https://github.com/adobe/unity_acpuserprofile#sample-app) |

