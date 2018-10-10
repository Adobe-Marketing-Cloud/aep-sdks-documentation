# AEP vs. 4x SDK

Comparison tables of the differences between the new Adobe Experience Platform and 4x SDK are provided for your convenience.

## Functionality support

### Core functionality

| Functionality | Version 4 SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| Modular SDK, Adobe & 3rd-party extensions | No | Yes |
| Server-side configuration | No | Yes |
| Programmatic configuration | No | Yes |
| Bundled configuration | Yes | Yes |
| Configuration management in Launch | No | Yes |
| Lifecycle metrics | Yes | Yes |
| Experience Cloud ID service | Yes | Yes |
| Privacy & GDPR framework | Yes | Yes |

### Adobe Analytics

| Functionality | Version 4 SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| App screens & user actions tracking | Yes | Yes |
| Offline tracking | Yes | Yes |
| Hit batching | Yes | Yes |
| Milestone media tracking | Yes | No |
| Timed action tracking | Yes | No |
| Video heartbeats | Yes | _Support coming_ |
| Lifetime value | Yes | Yes, use Profile extension |
| Server-side forwarding - Audience Manager | Yes | Yes |
| Set/get custom visitor ID \(vid or s.vid\) | Yes | No |

### Adobe Analytics - Mobile Services / Mobile Add-on

| Functionality | 4x SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| Postbacks - Get/POST URL requests | Yes | Yes, use Signals extension |
| Postbacks - PII Get/POST URL requests | Yes | Yes, use Signals extension |
| Postbacks - Open app deeplink | Yes | Yes, use Signals extension |
| Push Messaging | Yes | Support coming |
| In-app Messaging | Yes | Support coming |
| Marketing/Acquisition Links | Yes | Support coming |
| Geo location & beacon tracking | Yes | Support coming |
| Geo points-of-interest management | Yes | Support coming |

### Adobe Audience Manager

| Functionality | 4x SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| Send signals to Audience Manager | Yes | Yes |
| Reset identifiers & profiles | Yes | Yes |
| Return visitor profiles | Yes | Yes |
| DPID/DPUUID synching | Yes | No |

{% hint style="warning" %}
While synching with integration codes are fully supported, Experience Cloud SDK does not offer synch support with integration codes. The use of DPID/DPUUID are not supported.
{% endhint %}

### Adobe Target

| Functionality | 4x SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| A/B, Multivariate Testing, Offers | Yes | Yes |
| Offer pre-fetch | Yes | Yes |
| Offer preview | Yes | _Support coming_ |
| Visual editor | No | _Support coming_ |

## OS/platform support

| Platform | 4x SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| Android | Supported | Supported |
| Android Wear​ | Supported | _Support coming_ |
| Apple iOS​ | Supported | Supported |
| Apple WatchOS​ | Supported | Supported |
| Apple tvOS​ | Supported | Supported |
| React Native \(iOS & Android\) | Unsupported | Supported |
| Unity \(iOS & Android\)​ | Supported | _Support coming_ |
| Xamarin \(iOS & Android\)​ | Supported | _Support coming_ |
| PhoneGap \(iOS & Android\)​ | Supported | _Support coming_ |
| Universal Windows Platform \(UWP\) / Win 10 | Unsupported | _Support coming_ |
| Windows 8​ | Supported | Unsupported |
| Blackberry​ | Supported | Unsupported |

## API footprint
| 4x SDK | Experience Platform SDK | Extension/Framework | Notes |
| :--- | :--- | :--- | :--- |
| version | extensionVersion | All | each extension has and returns its own version |
| privacyStatus | getPrivacyStatus: | ACPCore |  |
| setPrivacyStatus: | setPrivacyStatus: | ACPCore |  |
| lifetimeValue | - | na | Should be kept in UserProfile, need an API to retrieve UserProfile values |
| userIdentifier | getUserIdentifier: | na | VID |
| setUserIdentifier: | setUserIdentifier: | na | VID |
| setPushIdentifier: | setPushIdentifier: | ACPCore |  |
| setAdvertisingIdentifier: | setAdvertisingIdentifier: | ACPCore |  |
| debugLogging | ? | ACPCore | Do we need a getter? |
| setDebugLogging: | setLogLevel: | ACPCore |  |
| collectLifecycleData | lifecycleStart: | ACPCore |  |
| collectLifecycleDataWithAdditionalData: | lifecycleStart: | ACPCore |  |
|  | lifecycleStop: | ACPCore |  |
| keepLifecycleSessionAlive | n/a | na |  |
| overrideConfigPath: | configureWithFileInPath: | ACPCore |  |
|  | configureWithAppId: | ACPCore |  |
|  | updateConfiguration: | ACPCore |  |
| setAppGroup: | setAppGroup: | ACPCore | extension support, needed for iOS and extension binary |
| setAppExtensionType: | + | na | extension support, needed for iOS and extension binary |
| syncSettings: | + | na | watch support, needed for iOS and watchOS |
| installWatch | n/a | na | watch support, watch only |
| installTVMLHooks: | n/a | na | tv support only, tv only |
| registerAdobeDataCallback: | n/a | na |  |
| trackState:data: | trackState:data: | ACPCore |  |
| trackAction:data: | trackAction:data: | ACPCore |  |
| trackActionFromBackground: | n/a | na |  |
| trackLocation:data: | ? | na | Are we supporting "TrackLocation", or waiting for Places? |
| trackBeacon:data: | ? | na | iOS only - same question as for "TrackLocation" |
| trackingClearCurrentBeacon | ? | na | iOS only |
| trackPushMessageClickThrough: | trackNotificationResponse: | ACPAcquisition |  |
| trackLocalNotificationClickThrough: | trackNotificationResponse: | ACPAcquisition |  |
"| trackAdobeDeepLink: | trackAdobeDeeplink: or 
collectLaunchInfo: | ??? |  |"
| trackLifetimeValueIncrease:data: | + | na |  |
| trackCoordinateSpace:data: | n/a | na |  |
| trackTimedActionStart:data: | n/a | na |  |
| trackTimedActionUpdate:data: | n/a | na |  |
| trackTimedActionEnd:logic: | n/a | na |  |
| trackingTimedActionExists: | n/a | na |  |
| trackingIdentifier | getTrackingIdentifier: | ACPAnalytics | AID |
| trackingSendQueuedHits | sendQueuedHits | ACPAnalytics |  |
| trackingClearQueue | clearQueue | ACPAnalytics |  |
| trackingGetQueueSize | getQueueSize: | ACPAnalytics |  |
| acquisitionCampaignStartForApp:data: | acquisitionCampaignStart:withData: | na |  |
|  | getDeferredDeeplinkUrl: | na | need this because we don't have adobeDataCallback any longer |
| targetPrefetchObjectWithName:mboxParameters: | prefetchObjectWithName:mboxParameters: | ACPTarget |  |
| targetRequestObjectWithName:defaultContent:mboxParameters:callback: | requestObjectWithName:defaultContent:mboxParameters:callback: | ACPTarget |  |
| targetPrefetchContent:withProfileParameters:callback: | prefetchContent:withProfileParameters:callback: | ACPTarget |  |
| targetLoadRequests:withProfileParameters: | loadRequests:withProfileParameters: | ACPTarget |  |
| targetPrefetchClearCache | prefetchClearCache | ACPTarget |  |
| targetLoadRequest:callback: | n/a | na |  |
| targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:callback: | n/a | na |  |
| targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:requestLocationParameters:callback: | n/a | na |  |
| targetCreateRequestWithName:defaultContent:parameters: | n/a | na |  |
| targetCreateOrderConfirmRequestWithName:orderId:orderTotal:productPurchasedId:parameters: | n/a | na |  |
| targetThirdPartyID | getThirdPartyId: | ACPTarget |  |
| targetSetThirdPartyID: | setThirdPartyId: | ACPTarget |  |
| targetPcID | n/a | na |  |
| targetSessionID | n/a | na |  |
|  | getTntId: | ACPTarget | this method is a replacement/combination of pcid and sessionid |
| targetClearCookies | resetExperience | ACPTarget |  |
"| targetEnterPreviewModeWithDeepLink: | trackAdobeDeeplink: or 
collectLaunchInfo: | ACPTarget | iOS only |"
| targetPreviewRestartDeeplink: | setPreviewRestartDeeplink: | ACPTarget | iOS only |
| audienceVisitorProfile | getVisitorProfile: | ACPAudience |  |
| audienceSetDpid:dpuuid: | audienceSetDpid:Dpuuid: | na |  |
| audienceDpid | audienceGetDpid: | na |  |
| audienceDpuuid | audienceGetDpuuid: | na |  |
| audienceSignalWithData:callback: | signalWithData:callback: | ACPAudience |  |
| audienceReset | reset | ACPAudience |  |
| visitorMarketingCloudID | getMarketingCloudId: | ACPIdentity | MID/ECID |
| visitorSyncIdentifiers: | syncIdentifiers: | ACPIdentity |  |
| visitorSyncIdentifiers:authenticationState: | syncIdentifiers:authentication: | ACPIdentity |  |
| visitorSyncIdentifiersWithType:identifier:authenticationState: | syncIdentifier:identifier:authentication: | ACPIdentity |  |
| visitorGetIDs | getIdentifiers: | ACPIdentity |  |
| visitorAppendToURL: | appendToUrl:withCallback: | ACPIdentity |  |
| visitorGetUrlVariablesAsync: | + | na | Added in 4.16.0 |
| collectPII: | collectPii: | ACPCore |  |
| getAllIdentifiersAsync: | + | ACPCore | Added for GDPR (4.15.0) |
| registerURLSessionConfigurationCallback: | + | na | To be released in 4.17.0 |
|  | downloadRules |  |  |
|  | registerExtension:withName:withVersion:error: |  |  |
|  | updateUserAttributes: |  |  |
|  | updateUserAttribute:withValue: |  |  |
|  | removeUserAttribute: |  |  |
|  |  |  |  |
| media* | n/a |  | media methods not supported in v5 |



