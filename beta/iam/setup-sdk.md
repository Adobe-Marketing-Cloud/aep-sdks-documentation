#  Set up AEPMessaging SDK

## Beta instructions

While the in-app messaging feature is in beta, the developer will need to use the Messaging extension on the `staging` branch of this repo.

{% tabs %}
{% tab title="iOS (cocoapods)" %}

The example below shows how to point to the `staging` branch in a Cocoapods `Podfile`:

```
pod 'AEPMessaging', :git => 'https://github.com/adobe/aepsdk-messaging-ios.git', :branch => 'staging'
pod 'AEPOptimize', :git => 'https://github.com/adobe/aepsdk-optimize-ios.git', :branch => 'staging'
```

{% endtab %}

{% tab title="Android (gradle)" %}

In-app messages are enabled in Messaging SDK version `1.2.0` or newer. Libraries built from the staging branch will contain `beta` in the artifact name.

The Messaging SDK is available from the Sonatype snapshot repository while it is in beta. In your app's top level Gradle file, add a reference to the repository:

```groovy
allprojects {
  repositories {
    // other needed repositories...
    // add the sonatype snapshot repository
    maven { url "https://oss.sonatype.org/content/repositories/snapshots/" }
  }
} 
```

The Messaging extension has a dependency on the Optimize extension. The Optimize extension must be added as a dependency in the app level Gradle file.

```groovy
implementation('com.adobe.marketing.mobile:messaging:1.2.0-beta-1-SNAPSHOT')
implementation('com.adobe.marketing.mobile:optimize:1.0.0-SNAPSHOT')
```

{% endtab %}
{% endtabs %}

### Import and register the Messaging extension

Import the AEPMessaging framework and its dependencies, then register the Messaging extension and dependencies.

{% tabs %}
{% tab title="iOS" %}

In the `application(_: didFinishLaunchingWithOptions:)` method in the `AppDelegate`:

#### Swift

```swift
import AEPMessaging
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize

class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions _: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // optionally enable trace logging
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

#### Java

```java
import android.app.Application;

import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.Messaging;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;

public class MainApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.VERBOSE);

        try {
            Messaging.registerExtension();
            Optimize.registerExtension();
            Identity.registerExtension();
            Edge.registerExtension();

            MobileCore.start(new AdobeCallback() {
                @Override
                public void call(Object o) {
                    MobileCore.configureWithAppID("MY_APP_ID");
                }
            });
        } catch (Exception e) {
            //Log the exception
        }
    }
}
```

{% endtab %}
{% endtabs %}
