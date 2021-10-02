# Adobe Journey Optimizer - Decisioning Extension

The Adobe Journey Optimizer - Decisioning extension powers real-time personalization workflows using Adobe Journey Optimizer - Offer Decisions or Adobe Target in mobile apps via the Edge Network. It helps deliver personalized decisions to your app and enables tracking user interactions with the proposed decisions.

## Prerequisites

Before starting, make sure the following steps are completed.

* Your IMS organization is provisioned for Edge decisioning. 
* If using Adobe Target, Target activities are set up in your desired workspace in your organization on Target UI. For more details, see [Target activities guide](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=en).
* If using Journey Optimizer - Offer Decisions, decisions are set up in your desired sandbox in your organization on Experience Platform UI. For more details, see the [create decisions guide](https://experienceleague.adobe.com/docs/offer-decisioning/using/create-manage-activities/create-offer-activities.html?lang=en).

## Adobe Experience Platform Data Collection setup

### Configure the Datastream for Adobe Target and/ or Journey Optimizer - Offer Decisions

On [Experience Platform Data Collection](https://launch.adobe.com/), navigate to **Data Collection** > **Datatreams** using the left navigation panel. Select an existing datastream or create a new datastream. For more details, see the [configure datastreams guide](https://aep-sdks.gitbook.io/docs/getting-started/configure-datastreams).

1. In the datastream, click on the desired environment from the list. Make sure **Adobe Experience Platform** section is enabled and configured with the required information like **Sandbox** and **Event Dataset**.
2. For Journey Optimizer - Offer Decisions, navigate to **Adobe Experience Platform** section and enable **Offer Decisioning** checkbox.
3. For Adobe Target, navigate to **Adobe Target** section and enable it. Specify the configuration. Make sure to configure the required information like Client Code.
4. Click **Save**.

![Datastream configuration](../../.gitbook/assets/ajo-decisioning-datastream-configuration.png)

### Configure Adobe Journey Optimizer - Decisioning extension in Tag property for Mobile

On [Experience Platform Data Collection](https://launch.adobe.com/), navigate to **Data Collection** > **Tags** using the left navigation panel. Select an existing mobile Tag property or create a new property.

1. In your mobile property, navigate to **Extensions** in the left navigation panel and click on the **Catalog** tab.
2. In the extensions Catalog, search or locate the **Adobe Journey Optimizer - Decisioning** extension, and click **Install**.
3. Since an extension configuration is not necessary, click **Save**.
4. Follow the publishing process to update SDK configuration. For more details, see the [publish the configuration guide](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property#publish-the-configuration).

![Adobe Journey Optimizer - Decisioning extension configuration](../../.gitbook/assets/ajo-decisioning-extension-configuration.png)

## Integrate Experience Platform Optimize SDK in your mobile application

{% hint style="warning" %}
For AEPOptimize APIs to work properly, it is required that you integrate Mobile Core and Edge extensions as well in your mobile app. For more details see, documentation on [Mobile Core](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core) and [Adobe Experience Platform Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/experience-platform-extension).
{% endhint %}

### Install the Experience Platform Mobile SDK

{% tabs %}
{% tab title="Android" %}
Add the Mobile Core, Edge, Identity for Edge Network and Optimize dependencies in your app's gradle file.

```java
implementation 'com.adobe.marketing.mobile:core:1.+'
implementation 'com.adobe.marketing.mobile:edge:1.+'
implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
implementation 'com.adobe.marketing.mobile:optimize:1.+'
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
Configure your app target to fetch Mobile Core, Edge, Identity for Edge Network and Optimize from Cocoapods by specifying the following pod dependencies in your `Podfile`.

```swift
platform :ios, '10.0'

use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore'
    pod 'AEPEdge'
    pod 'AEPEdgeIdentity'
    pod 'AEPOptimize'
end
```
{% endtab %}
{% endtabs %}

### Register the extensions with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

```java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;

public class MobileApp extends Application {

  @Override
  public void onCreate() {
    super.onCreate();
    MobileCore.setApplication(this);
    MobileCore.configureWithAppID(<YOUR_ENVIRONMENT_FILE_ID>); // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.

    Edge.registerExtension();
    Identity.registerExtension();
    Optimize.registerExtension();
    MobileCore.start(new AdobeCallback() {
      @Override
      public void call(final Object o) {
        // processing after start
      }});
  }
}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
// AppDelegate.swift

import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize

@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?

  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {

      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }

      return true
  }
}
```

#### Objective-C

```objc
// AppDelegate.m

@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPOptimize;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    // register the extensions
    [AEPMobileCore registerExtensions:@[AEPMobileEdge.class, AEPMobileEdgeIdentity.class, , AEPMobileOptimize.class] completion:^{
      [AEPMobileCore configureWithAppId: <YOUR_ENVIRONMENT_FILE_ID>]; // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
  }];
  ...
}
```
{% endtab %}
{% endtabs %}

## Adobe Journey Optimizer - Offer Decisions

{% hint style="warning" %}
Some offer constraints, such as Capping, are currently unsupported with the mobile Experience Edge workflows. The Capping field value specifies the number of times an offer can be presented across all users. For more details, see the [offer eligibility rules and constraints guide](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
{% endhint %}

### DecisionScope

The `DecisionScope` public class provides a constructor to create a scope object using the activityId, placementId, and optional itemCount. The decision scope activity and placement information can be obtained from the decision on the Experience Platform UI. 

{% tabs %}
{% tab title="Android" %}
```java
final DecisionScope decisionScope = DecisionScope("xcore:offer-activity:1111111111111111", "xcore:offer-placement:1111111111111111", 3);
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
let decisionScope = DecisionScope(activityId: "xcore:offer-activity:1111111111111111", 
                                  placementId: "xcore:offer-placement:1111111111111111",
                                  itemCount: 3)
```

#### Objective-C

```objc
AEPDecisionScope* decisionScope = [[AEPDecisionScope alloc] initWithActivityId:@"xcore:offer-activity:1111111111111111"         
                                                                   placementId:@"xcore:offer-placement:1111111111111111" 
                                                                     itemCount:3];
```
{% endtab %}
{% endtabs %}

Alternately, another of the class's constructor can be used to create a scope object using the encoded decision scope. The encoded scope can also be read directly from the decision on Experience Platform UI.

{% tabs %}
{% tab title="Android" %}
#### Java

```java
final DecisionScope decisionScope = DecisionScope("eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjEyYmEyZjM4MWJjYTY3NWUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJiOWEwMDA1NTUwNzM1NyIsICJ4ZG06aXRlbUNvdW50IjozfQ==");
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
let decisionScope = DecisionScope(name: "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjEyYmEyZjM4MWJjYTY3NWUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJiOWEwMDA1NTUwNzM1NyIsICJ4ZG06aXRlbUNvdW50IjozfQ==")
```

#### Objective-C

```objc
AEPDecisionScope* decisionScope = [[AEPDecisionScope alloc] initWithName:@"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjEyYmEyZjM4MWJjYTY3NWUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJiOWEwMDA1NTUwNzM1NyIsICJ4ZG06aXRlbUNvdW50IjozfQ=="];
```
{% endtab %}
{% endtabs %}

## Adobe Target

### Target location

The `DecisionScope` public class provides a designated initializer which can be used to create a Target location (or mbox).

{% tabs %}
{% tab title="Android" %}
#### Java

```java
final DecisionScope decisionScope = DecisionScope("myTargetLocation");
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
let decisionScope = DecisionScope(name: "myTargetLocation")
```

#### Objective-C

```objc
AEPDecisionScope* decisionScope = [[AEPDecisionScope alloc] initWithName:@"myTargetLocation"];
```
{% endtab %}
{% endtabs %}

### Target Parameters

Target Parameters can be sent in a personalization query request to the Experience Edge network by adding them in `data` dictionary when calling the `updatePropositions` API.

{% tabs %}
{% tab title="Android" %}
#### Java

```java
final Map<String, Object> data = new HashMap<>();
final Map<String, String> targetParameters = new HashMap<>();

// Add mbox parameters
targetParameters.put("someKey", "someValue");

// Add profile parameters - prefix with profile.
targetParameters.put("profile.membershipLevel", "platinum");

// Add product parameters
targetParameters.put("productId", "111");
targetParameters.put("categoryId", "Books");

// Add order parameters
targetParameters.put("orderId", "10");
targetParameters.put("orderTotal", "110.56");
targetParameters.put("purchasedProductIds", "111");

data.put("__adobe", new HashMap<String, Object>() {
  {
    put("target", targetParameters);
  }
});


final DecisionScope decisionScope = DecisionScope("myTargetLocation") // Target location (or mbox)
Optimize.updatePropositions(decisionScope, null, data);
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
var data: [String: Any] = [:]
var targetParameters: [String: String] = [:]

// Add mbox parameters
targetParameters["someKey"] = "someValue"

// Add profile parameters - prefix with profile.
targetParameters["profile.membershipLevel"] = "platinum"

// Add product parameters
targetParameters["productId"] = "111"
targetParameters["categoryId"] = "Books"

// Add order parameters
targetParameters["orderId"] = "10"
targetParameters["orderTotal"] = "110.56"
targetParameters["purchasedProductIds"] = "111"

data["__adobe"] = [
  "target": targetParameters
]

let decisionScope = DecisionScope(name: "myTargetLocation") // Target location (or mbox)
Optimize.updatePropositions(for: decisionScope withXdm: nil andData: data)
```

#### Objective-C

```objc
NSMutableDictionary* data = [NSMutableDictionary dictionary];
NSMutableDictionary* targetParameters = [NSMutableDictionary dictionary];

// Add mbox parameters
targetParameters[@"someKey"] = @"someValue";

// Add profile parameters - prefix with profile.
targetParameters[@"profile.membershipLevel"] = @"platinum";

// Add product parameters
targetParameters[@"productId"] = @"111";
targetParameters[@"categoryId"] = @"Books";

// Add order parameters
targetParameters[@"orderId"] = @"10";
targetParameters[@"orderTotal"] = @"110.56";
targetParameters[@"purchasedProductIds"] = @"111";

[data setObject:[NSDictionary dictionaryWithObject:targetParameters forKey:@"target"] forKey:@"__adobe"];

AEPDecisionScope* decisionScope = [[AEPDecisionScope alloc] initWithName:@"myTargetLocation"]; // Target location (or mbox)
[AEPMobileOptimize updatePropositions:@[decisionScope] withXdm:nil andData:data];
```
{% endtab %}
{% endtabs %}

### Target Third Party ID

To use Target Third Party ID in the Experience Edge mobile workflows, the corresponding namespace needs to be configured in Experience Platform Data Collection.

1. On [Experience Platform Data Collection](https://launch.adobe.com/), navigate to **Data Collection** > **Datatreams** using the left navigation panel.
2. Select your configured datastream and click on the desired environment from the list.
3. Navigate to **Adobe Target** section, specify the **Target Third Party ID Namespace**.
4. Click **Save**.

![Target Third Party ID configuration](../../.gitbook/assets/ajo-decisioning-target-tpid.png)

In your mobile application, integrate the Identity for Edge Network extension to add the Target Third Party ID in the Identity Map in the personalization query request to the Edge network when calling the `updatePropositions` API. For more details, see the [Identity for Edge Network - updateIdentities API](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#updateidentities).
 
{% tabs %}
{% tab title="Android" %}
#### Java

```java
final IdentityItem item = new IdentityItem("1111", AuthenticatedState.AUTHENTICATED, true);
final IdentityMap identityMap = new IdentityMap();
identityMap.addItem(item, "userCRMID") // userCRMID being used as Third Party ID
Identity.updateIdentities(identityMap);
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
let identityMap = IdentityMap()
identityMap.add(item: IdentityItem(id: "1111", authenticatedState: AuthenticatedState.authenticated, primary: true),
                withNamespace: "userCRMID") // userCRMID being used as Third Party ID
Identity.updateIdentities(with: identityMap)
```

#### Objective-C

```objc
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"1111" authenticatedState:AEPAuthenticatedStateAuthenticated primary:true];

AEPIdentityMap *identityMap = [[AEPIdentityMap alloc] init];
[identityMap addItem:item withNamespace:@"userCRMID"]; // userCRMID being used as Third Party ID

[AEPMobileEdgeIdentity updateIdentities:identityMap];
```
{% endtab %}
{% endtabs %}

### Analytics for Target (A4T)

Set up the Analytics for Target (A4T) cross-solution integration by enabling the A4T campaigns to use Analytics as the reporting source for an activity. Subsequently, all reporting and segmentation for that activity is based on Analytics data collection. For more information, see [Adobe Analytics for Adobe Target (A4T)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

Once Analytics is listed as the reporting source for an activity on Target UI, A4T works out of the box in the Optimize SDK. The Experience Edge handles forwarding any Target A4T payloads to Adobe Analytics and no additional action is required on the client-side.

{% hint style="warning" %}
For this integration to work, make sure Analytics is enabled in your datastream configuration for the desired environment and Report Suite information is provided. 
{% endhint %}

## Tracking

### Proposition tracking using direct Offer class methods

User interactions with the decision propositions can be tracked using the following public methods in the `Offer` class. 

{% tabs %}
{% tab title="Android" %}
#### Java

```java
public class Offer {
  ...
  /**
    * Dispatches an event for the Edge network extension to send an Experience Event to the Edge network with the display interaction data for the
    * given {@code Proposition} offer.
    */
  public void displayed() {...}

  /**
    * Dispatches an event for the Edge network extension to send an Experience Event to the Edge network with the tap interaction data for the
    * given {@code Proposition} offer.
    */
  public void tapped() {...}
}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
public extension Offer {
    /// Dispatches an event for the Edge extension to send an Experience Event to the Edge network with the display interaction data for the given proposition item.
    func displayed() {...}

    /// Dispatches an event for the Edge extension to send an Experience Event to the Edge network with the tap interaction data for the given proposition item.
    func tapped() {...}
}
```
{% endtab %}
{% endtabs %}

Upon calling these `Offer` methods, an Experience Event is sent to the Edge network with the proposition interaction data for the given offer.

{% tabs %}
{% tab title="Android" %}
#### Java

```java
offer.displayed(); // Sends an Offer display notification to Edge network
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
offer.displayed() // Sends an Offer display notification to Edge network
```

#### Objective-C

```objc
[offer displayed]; // Sends an Offer display notification to Edge network
```
{% endtab %}
{% endtabs %}

### Proposition tracking using Edge extension API

For more advanced tracking use cases, additional public methods are available in the `Offer` and `Proposition` classes. These methods can be used to generate XDM formatted data for `Experience Event - Proposition Interactions` and `Experience Event - Proposition Reference` field groups. 

{% tabs %}
{% tab title="Android" %}
#### Java

```java
public class Offer {
  ...
  /**
    * Generates a map containing XDM formatted data for {@code Experience Event - Proposition Interactions} field group from this {@code Proposition} item.
    * <p>
    * The returned XDM data does contain the {@code eventType} for the Experience Event with value {@code decisioning.propositionDisplay}.
    * <p>
    * Note: The Edge sendEvent API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, and override
    * dataset identifier.
    *
    * @return {@code Map<String, Object>} containing the XDM data for the proposition interaction.
    */
  public Map<String, Object> generateDisplayInteractionXdm() {...}

  /**
    * Generates a map containing XDM formatted data for {@code Experience Event - Proposition Interactions} field group from this {@code Proposition} offer.
    * <p>
    * The returned XDM data contains the {@code eventType} for the Experience Event with value {@code decisioning.propositionInteract}.
    * <p>
    * Note: The Edge sendEvent API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, and override
    * dataset identifier.
    *
    * @return {@code Map<String, Object>} containing the XDM data for the proposition interaction.
    */
  public Map<String, Object> generateTapInteractionXdm() {...}
}
```
```java
public class Proposition {
  ...
  /**
    * Generates a map containing XDM formatted data for {@code Experience Event - Proposition Reference} field group from this {@code Proposition}.
    * <p>
    * The returned XDM data does not contain {@code eventType} for the Experience Event.
    *
    * @return {@code Map<String, Object>} containing the XDM data for the proposition reference.
    */
  public Map<String, Object> generateReferenceXdm() {...}
}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
public extension Offer {
  /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Interactions` field group from the given proposition option.
  ///
  /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
  ///
  /// - Note: The returned XDM data also contains the `eventType` for the Experience Event with value `decisioning.propositionDisplay`.
  /// - Returns A dictionary containing XDM data for the propositon interactions.
  func generateDisplayInteractionXdm() -> [String: Any] {...}

  /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Interactions` field group from the given proposition option.
  ///
  /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
  ///
  /// - Note: The returned XDM data also contains the `eventType` for the Experience Event with value `decisioning.propositionInteract`.
  /// - Returns A dictionary containing XDM data for the propositon interactions.
  func generateTapInteractionXdm() -> [String: Any] {...}
}
```
```swift
public extension Proposition {
  /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Reference` field group from the given proposition.
  ///
  /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
  ///
  /// - Note: The returned XDM data does not contain an `eventType` for the Experience Event.
  /// - Returns A dictionary containing XDM data for the propositon reference.
  func generateReferenceXdm() -> [String: Any] {...}
}
```
{% endtab %}
{% endtabs %}

The Edge `sendEvent` API can then be used to send this tracking XDM data along with any additional XDM and freeform data to the Experience Edge network. Additionally, an override dataset can also be specified for tracking data. For more details, see [Edge - sendEvent API](https://aep-sdks.gitbook.io/docs/foundation-extensions/experience-platform-extension/edge-network-api-reference#sendevent).

{% tabs %}
{% tab title="Android" %}
#### Java

```java
// When a proposition is retrieved using getPropositions API or onUpdatePropositions API callback 
// and the corresponding offer is displayed, invoke method on Offer object to get the XDM data.

final Map<String, Object> displayInteractionXdm = offer.generateDisplayInteractionXdm() // Offer display tracking XDM
final Map<String, Object> additionalData = new HashMap<>();
additionalData.put("someDataKey", "someDataValue");

final ExperienceEvent experienceEvent = new ExperienceEvent.Builder().setXdmSchema(displayInteractionXdm).setData(additionalData).build();
Edge.sendEvent(experienceEvent, null)
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
// When a proposition is retrieved using getPropositions API or onUpdatePropositions API callback 
// and the corresponding offer is displayed, invoke method on Offer object to get the XDM data.

let displayInteractionXdm = offer.generateDisplayInteractionXdm() // Offer display tracking XDM
let additionalData: [String: Any] = ["someDataKey": "someDataValue"]

let experienceEvent = ExperienceEvent(xdm: displayInteractionXdm, data: additionalData)
Edge.sendEvent(experienceEvent)
```

#### Objective-C

```objc
// When a proposition is retrieved using getPropositions API or onUpdatePropositions API callback 
// and the corresponding offer is displayed, invoke method on Offer object to get the XDM data.

NSDictionary* displayInteractionXdm = [offer generateDisplayInteractionXdm];
NSDictionary* additionalData = @{@"someDataKey": @"someDataValue"};

AEPExperienceEvent* experienceEvent = [[AEPExperienceEvent alloc] initWithXdm:displayInteractionXdm data:additionalData datasetIdentifier:nil];
[AEPMobileEdge sendExperienceEvent:event completion:nil];
```
{% endtab %}
{% endtabs %}

## Configuration keys

To update the SDK configuration programmatically, use the following information to change the Optimize extension configuration values. For more information, see the [programmatic updates to Configuration guide](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/configuration/configuration-api-reference#updateconfiguration).

| Key | Required | Description | Data Type |
| :--- | :--- | :--- | :--- |
| optimize.datasetId | No | Override dataset's Identifier which can be obtained from the Experience Platform UI. For more details see, [Datasets UI guide](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en) | String |

{% hint style="info" %}
If the override dataset is used for proposition tracking, make sure the corresponding schema definition contains the `Experience Event - Proposition Interaction` field group. For more information, see the [setup schemas and datasets guide](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/62a861aec745af2d8237c287656c68d8f8cdd5ed/getting-started/configure-schema-and-dataset.md).
{% endhint %}


