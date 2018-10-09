# Get the SDK

The Adobe Experience Platform SDK is available via Cocoapods and Gradle. 

1. Open the **Mobile** property in Launch and go to the **Environments** tab to view instructions for adding the SDKs to an app.
2. Find the platform needed in the table and click on the box icon under the **Install** column.
3. On the **Mobile Install Instructions** pop-up, choose **Android** or **iOS**.
4. Follow the instructions for using Grade with Android or CocoaPods with iOS.

The necessary dependencies and initialization code can be copied from the pop-up to the app project.

![](https://github.com/praschetan/reactor-user-docs/raw/master/.gitbook/assets/install-instructions.png)

{% tabs %}
{% tab title="Android" %}
{% hint style="warning" %}
_Adobe Experience Platform SDK for Android supports **Android 4.0 \(API 14\) or later.**_
{% endhint %}

1. Create MainActivity.java in the app.
2. Add `MobileCore.configureWithAppID("PASTE_APP_ID_HERE");`
{% endtab %}

{% tab title="Objective C" %}
_**Important:** Adobe Experience Platform SDKs for iOS supports **iOS 10 or later.**_

1. In Xcode, open AppDelegate.swift \(Swift\) or AppDelegate.m \(Objective-C\)
2. Under `didFinishLaunchingWithOptions`, add:`[ACPCore configureWithAppId:@"PASTE_APP_ID_HERE"];`
{% endtab %}

{% tab title="Swift" %}
_**Important:** Adobe Experience Platform SDKs for iOS supports **iOS 10 or later.**_

1. In Xcode, open AppDelegate.swift \(Swift\) or AppDelegate.m \(Objective-C\)
2. Under `didFinishLaunchingWithOptions`, add:`ADBMobileMarketing.configure(withAppId: "YOUR_APP_ID")`
{% endtab %}
{% endtabs %}

### Further Reading

* [How to use Gradle for Android](https://docs.gradle.org/current/userguide/userguide.html)
* [How to use CocoaPods for iOS ](https://guides.cocoapods.org/using/using-cocoapods)

