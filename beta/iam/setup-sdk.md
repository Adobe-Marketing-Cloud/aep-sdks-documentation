#  Set up AEPMessaging SDK

## Beta instructions

While the in-app messaging feature is in beta, the developer will need to use the Messaging extension on the `staging` branch of this repo.

{% tabs %}
{% tab title="iOS (cocoapods)" %}

The example below shows how to point to the `staging` branch in a Cocoapods `Podfile`:

```
pod 'AEPMessaging', :git => 'https://github.com/adobe/aepsdk-messaging-ios.git', :branch => 'staging'
```

{% endtab %}

{% tab title="Android (gradle)" %}

{% endtab %}
{% endtabs %}

### Import and register the Messaging extension

Import the AEPMessaging framework and its dependencies, then register the Messaging extension and dependencies.

{% tabs %}
{% tab title="iOS" %}

In the `application(_: didFinishLaunchingWithOptions:)` method in the `AppDelegate`:

Swift

```swift
import AEPMessaging
import AEPCore
import AEPEdge
import AEPEdgeIdentity

class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions _: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // optionally enable debug logging
        MobileCore.setLogLevel(.trace)

        // create a list of extensions that will be registered
        let extensions = [
            Messaging.self,
            AEPEdgeIdentity.Identity.self,
            Edge.self,
            Optimize.self
        ]

        MobileCore.registerExtensions(extensions) {            
            // use the App ID assigned for this application from Adobe Data Collection (formerly Adobe Launch)
            MobileCore.configureWith(appId: "MY_APP_ID")
        }

        return true
    }
}
```

{% endtab %}

{% tab title="Android" %}

{% endtab %}
{% endtabs %}
