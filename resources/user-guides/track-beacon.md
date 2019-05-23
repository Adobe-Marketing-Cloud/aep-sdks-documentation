# Tracking Beacons

## Emulating the trackBeacon call from v4 SDKs

The `trackBeacon` call is no longer available in the AEP SDKs. If you would like to send beacon tracking data to your Analytics server and be able to create rules based off of a user's proximity to your beacons, you can do so manually. Note that this solution relies on the [Profile extension](../../using-mobile-extensions/profile/) for the purposes of generating beacon-related rules.

This page contains sample code to help you implement your own `trackBeacon` calls.

### Tracking a beacon

When your user comes within range of a beacon, call this method to send beacon data to [Analytics](../../using-mobile-extensions/adobe-analytics/). This code also saves all beacon-related data in the client-side Profile for use with the Rules Engine.

{% tabs %}
{% tab title="Android" %}
In this method, the `proximity` parameter is an `int` representing various distances:

* 0 - Unknown
* 1 - Immediate
* 2 - Near
* 3 - Far

```java
static final String ACP_BEACON_MAJOR = "a.beacon.major";
static final String ACP_BEACON_MINOR = "a.beacon.minor";
static final String ACP_BEACON_UUID = "a.beacon.uuid";
static final String ACP_BEACON_PROXIMITY = "a.beacon.prox";

void trackBeacon(final String beaconUUID, final String major, final String minor, final int proximity, final Map<String, String> cdata) {
    final HashMap<String, String> contextData = cdata == null ? new HashMap<String, String>() : new HashMap<String, String>(cdata);

    if (major != null && !major.isEmpty()) {
        contextData.put(ACP_BEACON_MAJOR, major);
        UserProfile.updateUserAttribute(ACP_BEACON_MAJOR, major);
    } else {
        UserProfile.removeUserAttribute(ACP_BEACON_MAJOR);
    }

    if (minor != null && !minor.isEmpty()) {
        contextData.put(ACP_BEACON_MINOR, minor);
        UserProfile.updateUserAttribute(ACP_BEACON_MINOR, minor);
    } else {
        UserProfile.removeUserAttribute(ACP_BEACON_MINOR);
    }

    if (beaconUUID != null && !beaconUUID.isEmpty()) {
        contextData.put(ACP_BEACON_UUID, beaconUUID);
        UserProfile.updateUserAttribute(ACP_BEACON_UUID, beaconUUID);
    } else {
        UserProfile.removeUserAttribute(ACP_BEACON_UUID);
    }

    contextData.put(ACP_BEACON_PROXIMITY, String.valueOf(proximity));
    UserProfile.updateUserAttribute(ACP_BEACON_PROXIMITY, String.valueOf(proximity));

    final HashMap<String, Object> eventData = new HashMap<>();
    eventData.put("trackinternal", true);
    eventData.put("action", "Beacon");
    eventData.put("contextdata", contextData);

    final Event event = new Event.Builder("TrackBeacon", "com.adobe.eventType.generic.track", "com.adobe.eventSource.requestContent")
            .setEventData(eventData)
            .build();

    MobileCore.dispatchEvent(event, null);
}
```
{% endtab %}

{% tab title="iOS" %}
`CLBeacon` is only currently available in iOS. The sample code contains the necessary checks to ensure OS compatibility.

#### Objective-C

```objectivec
#if TARGET_OS_IOS
static NSString* const ACP_BEACON_MAJOR = @"a.beacon.major";
static NSString* const ACP_BEACON_MINOR = @"a.beacon.minor";
static NSString* const ACP_BEACON_UUID = @"a.beacon.uuid";
static NSString* const ACP_BEACON_PROXIMITY = @"a.beacon.prox";

+ (void) trackBeacon:(CLBeacon *)beacon data:(NSDictionary*)data {
    NSMutableDictionary *contextData = data ? [data mutableCopy] : [@{} mutableCopy];

    if (beacon.major) {
        contextData[ACP_BEACON_MAJOR] = [beacon.major stringValue];
        [ACPUserProfile updateUserAttribute:ACP_BEACON_MAJOR withValue:[beacon.major stringValue]];
    } else {
        [ACPUserProfile removeUserAttribute:ACP_BEACON_MAJOR];
    }

    if (beacon.minor) {
        contextData[ACP_BEACON_MINOR] = [beacon.minor stringValue];
        [ACPUserProfile updateUserAttribute:ACP_BEACON_MINOR withValue:[beacon.minor stringValue]];
    } else {
        [ACPUserProfile removeUserAttribute:ACP_BEACON_MINOR];
    }

    if (beacon.proximityUUID.UUIDString) {
        contextData[ACP_BEACON_UUID] = beacon.proximityUUID.UUIDString;
        [ACPUserProfile updateUserAttribute:ACP_BEACON_UUID withValue:beacon.proximityUUID.UUIDString];
    } else {
        [ACPUserProfile removeUserAttribute:ACP_BEACON_UUID];
    }

    switch (beacon.proximity) {
        case CLProximityImmediate:
            contextData[ACP_BEACON_PROXIMITY] = @"1";
            break;
        case CLProximityNear:
            contextData[ACP_BEACON_PROXIMITY] = @"2";
            break;
        case CLProximityFar:
            contextData[ACP_BEACON_PROXIMITY] = @"3";
            break;
        case CLProximityUnknown:
        default:
            contextData[ACP_BEACON_PROXIMITY] = @"0";
    }
    [ACPUserProfile updateUserAttribute:ACP_BEACON_PROXIMITY withValue:contextData[ACP_BEACON_PROXIMITY]];

    NSDictionary *eventData = @{
                                @"trackinternal":@(YES),
                                @"action":@"Beacon",
                                @"contextdata":contextData
                                };

    ACPExtensionEvent *event = [ACPExtensionEvent extensionEventWithName:@"TrackBeacon"
                                                                    type:@"com.adobe.eventType.generic.track"
                                                                  source:@"com.adobe.eventSource.requestContent"
                                                                    data:eventData
                                                                   error:nil];
    [ACPCore dispatchEvent:event error:nil];
}
#endif
```

#### Swift

```swift
import ARKit

class ARKitSampleViewController: UIViewController {
    var label: UILabel?
    var planeFound = false

    func plane(from anchor: ARPlaneAnchor?) -> SCNNode? {
        let plane = SCNPlane(width: CGFloat(anchor?.extent.x ?? 0.0), height: CGFloat(anchor?.extent.z ?? 0.0))

        plane.firstMaterial?.diffuse.contents = UIColor.clear
        let planeNode = SCNNode(geometry: plane)
        planeNode.position = SCNVector3Make(anchor?.center.x ?? 0.0, 0, anchor?.center.z ?? 0.0)
        // SCNPlanes are vertically oriented in their local coordinate space.
        // Rotate it to match the horizontal orientation of the ARPlaneAnchor.
        planeNode.transform = SCNMatrix4MakeRotation(-.pi * 0.5, 1, 0, 0)

        return planeNode
    }

// MARK: - ARSCNViewDelegate
    func renderer(_ renderer: SCNSceneRenderer, didAdd node: SCNNode, for anchor: ARAnchor) {
        if planeFound == false {
            if (anchor is ARPlaneAnchor) {
                DispatchQueue.main.async(execute: {
                    self.planeFound = true
                    self.label?.text = "DANCEFLOOR FOUND. LET'S BOOGIE"

                    let overlay = UIView(frame: self.view.frame)
                    overlay.backgroundColor = UIColor.black
                    overlay.alpha = 0
                    if let label = self.label {
                        self.view.insertSubview(overlay, belowSubview: label)
                    }

                    UIView.animate(withDuration: 1.5, delay: 2, options: .curveEaseIn, animations: {
                        self.label?.alpha = 0
                        overlay.alpha = 0.5
                    }) { finished in
                        let planeAnchor = anchor as? ARPlaneAnchor
                        // Show the disco ball here
                    }
                })
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

### Clearing the current beacon

The `clearCurrentBeacon` code will remove any previously set user attributes in the Profile extension. To keep Rules working as expected, this method should be called whenever the user is no longer within range of your beacon.

{% tabs %}
{% tab title="Android" %}
This example is using `static` constant strings that were provided in the `trackBeacon` code sample above.

```java
void clearCurrentBeacon() {
    UserProfile.removeUserAttribute(ACP_BEACON_MAJOR);
    UserProfile.removeUserAttribute(ACP_BEACON_MINOR);
    UserProfile.removeUserAttribute(ACP_BEACON_UUID);
    UserProfile.removeUserAttribute(ACP_BEACON_PROXIMITY);
}
```
{% endtab %}

{% tab title="iOS" %}
`CLBeacon` is only currently available in iOS. The sample code contains the necessary checks to ensure OS compatibility.

This example is using `static` constant strings that were provided in the `trackBeacon` code sample above.

#### Objective-C

```objectivec
#if TARGET_OS_IOS
+ (void) clearCurrentBeacon {
    [ACPUserProfile removeUserAttribute:ACP_BEACON_MAJOR];
    [ACPUserProfile removeUserAttribute:ACP_BEACON_MINOR];
    [ACPUserProfile removeUserAttribute:ACP_BEACON_UUID];
    [ACPUserProfile removeUserAttribute:ACP_BEACON_PROXIMITY];
}
#endif
```

#### Swift

```swift
#if TARGET_OS_IOS
+clearCurrentBeacon
do {
    ACPUserProfile.removeUserAttribute(ACP_BEACON_MAJOR)
    ACPUserProfile.removeUserAttribute(ACP_BEACON_MINOR)
    ACPUserProfile.removeUserAttribute(ACP_BEACON_UUID)
    ACPUserProfile.removeUserAttribute(ACP_BEACON_PROXIMITY)
}
#endif
```
{% endtab %}
{% endtabs %}

## Using beacon values in Launch rules

In the above code samples, attributes are being set in the client-side user profile. We can use those attributes when creating a rule in Launch to give a custom experience or take a specific action when the user is near a beacon.

### Beacon data in rule conditions

Mix-and-match beacon data in conditions to determine the specific audience for your action. You can use the following beacon-related variables:

* UUID \(`a.beacon.uuid`\)
* Major ID \(`a.beacon.major`\)
* Minor ID \(`a.beacon.minor`\)
* User Proximity \(`a.beacon.prox`\)

Configure your condition by selecting the `Profile` extension, choosing `Profile Value` as a condition type, and entering in the desired variable. The following image shows an example of a condition which will pass when the Major ID \(`a.beacon.major`\) of the beacon is equal to `12`:

![](../../.gitbook/assets/beacon-condition.png)

![](../../.gitbook/assets/beacon-rule.png)

### Beacon data in rule actions

Before using beacon data in your actions, creating a data element is recommended. You will need to create a data element for each variable you want to use in your actions. The image below is an example of creating a data element named `beacon.major` for the `a.beacon.major` key in our profile:

![](../../.gitbook/assets/beacon-data-element.png)

After creating a data element, we can use it as token replacement in our actions. The screenshot below shows an action sending data to Analytics, and attaching the `beacon.major` data element as additional context data:

![](../../.gitbook/assets/beacon-token-replacement.png)

