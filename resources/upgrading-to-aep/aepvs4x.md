# Adobe Experience Platform SDKs vs. 4x SDK

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
| Lifecycle metrics | Yes | Yes |
| Experience Cloud ID service | Yes | Yes |
| Privacy and GDPR framework | Yes | Yes |

### Adobe Analytics

| Functionality | Version 4 SDKs | Experience Platform SDKs |
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
| Geo location and beacon tracking | Yes | Support coming |
| Geo points-of-interest management | Yes | Support coming |

### Adobe Audience Manager

| Functionality | 4x SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| Send signals to Audience Manager | Yes | Yes |
| Reset identifiers and profiles | Yes | Yes |
| Return visitor profiles | Yes | Yes |
| DPID/DPUUID synching | Yes | No |

{% hint style="warning" %}
Although synching with integration codes is fully supported, the Experience Cloud SDKs do not offer synch support with integration codes. The use of DPID/DPUUID are not supported.
{% endhint %}

### Adobe Target

| Functionality | 4x SDKs | Experience Platform SDKs |
| :--- | :--- | :--- |
| A/B, Multivariate Testing, Offers | Yes | Yes |
| Offer pre-fetch | Yes | Yes |
| Offer preview | Yes | _Support coming_ |
| Visual editor | No | _Support coming_ |

## OS/platform support

| Platform | 4x SDKs | Experience Platform SDKs |
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

