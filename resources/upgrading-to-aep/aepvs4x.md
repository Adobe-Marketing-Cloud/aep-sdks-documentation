# Experience Platform SDKs vs. 4x SDKs

The following tables provide information about the differences between the new Experience Platform SDKs and the 4x SDKs:

## Functionality support

### Core functionality

| Functionality | Version 4 SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| Modular SDK, Adobe and third-party extensions | No | Yes |
| Server-side configuration | No | Yes |
| Programmatic configuration | No | Yes |
| Bundled configuration | Yes | Yes |
| Configuration management in Launch | No | Yes |
| Lifecycle metrics | Yes | Yes, see [Manual Lifecycle Implementation](manual-lifecycle-implementation.md) |
| Experience Cloud ID service | Yes | Yes |
| Privacy and GDPR framework | Yes | Yes |

### Adobe Analytics

| Functionality | Version 4 SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| App screens & user actions tracking | Yes | Yes |
| Offline tracking | Yes | Yes |
| Hit batching | Yes | Yes |
| Milestone media tracking | Yes | Deprecated |
| Timed action tracking | Yes | Deprecated |
| Video heartbeats | Yes | Yes |
| Lifetime value | Yes | Yes, use Profile extension |
| Server-side forwarding - Audience Manager | Yes | Yes |
| Set/get custom visitor ID \(vid or s.vid\) | Yes | Yes |

### Adobe Analytics - Mobile Services / Mobile Add-on

| Functionality | 4x SDK | Experience Platform SDK |
| :--- | :--- | :--- |
| Postbacks - Get/POST URL requests | Yes | Yes - [Signals](aepvs4x.md) extension |
| Postbacks - PII Get/POST URL requests | Yes | Yes - [Signals](aepvs4x.md) extension |
| Postbacks - Open app deeplink | Yes | Yes - [Signals](aepvs4x.md) extension |
| Push Messaging | Yes | Yes - [Mobile Services](../../using-mobile-extensions/adobe-analytics-mobile-services/) extension |
| In-app Messaging | Yes | Yes - [Mobile Services](../../using-mobile-extensions/adobe-analytics-mobile-services/) extension |
| Marketing/Acquisition Links | Yes | Yes - [Mobile Services](../../using-mobile-extensions/adobe-analytics-mobile-services/) extension |
| Geo location and beacon tracking | Yes | Yes - Use [Places](aepvs4x.md) extension |
| Geo points-of-interest management | Yes | Yes - Use [Places](aepvs4x.md) extension |

### Adobe Audience Manager

| Functionality | 4x SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| Send signals to Audience Manager | Yes | Yes |
| Reset identifiers and profiles | Yes | Yes |
| Return visitor profiles | Yes | Yes |
| DPID/DPUUID synching | Yes | Deprecated |

{% hint style="warning" %}
Although synching with integration codes is fully supported, the Experience Cloud SDKs do not offer synch support with integration codes. The use of DPID/DPUUID are not supported.
{% endhint %}

### Adobe Target

| Functionality | 4x SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| A/B, Multivariate Testing, Offers | Yes | Yes |
| Offer pre-fetch | Yes | Yes |
| Offer preview | Yes | Yes |

## OS/platform support

| Platform | 4x SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| Android | Supported | Supported |
| Android Wear​ | Supported | _Support coming_ |
| Apple iOS​ | Supported | Supported |
| Apple WatchOS​ | Supported | _Support coming_ |
| Apple tvOS​ | Supported | Supported |
| React Native \(iOS & Android\) | Supported | Supported |
| Flutter \(iOS & Android\) | Unupported | Supported |
| Unity \(iOS & Android\)​ | Supported | ~~Supported~~ Deprecated |
| Xamarin \(iOS & Android\)​ | Supported | Supported |
| Cordova \(iOS & Android\)​ | Supported | Supported |
| Universal Windows Platform \(UWP\) / Win 10 | Unsupported | _Not supported_ |
| Windows 8​ | Supported | _Not supported_ |
| Blackberry​ | Supported | _Not supported_ |

