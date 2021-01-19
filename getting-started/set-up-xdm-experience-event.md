# Set up your first XDM Experience event

In the context of Adobe Experience Platform Mobile SDKs, an `Experience Event` is an object that contains data conforming to an XDM ExperienceEvent Schema definition in Adobe Experience Platform.

Use XDM Experience Events to track time-series-based user actions in your mobile application or cross channel.

This section shows how to start tracking product reviews as user actions in a mobile implementation using Adobe Experience Platform datasets and the Adobe Experience Platform Edge mobile extension.

## Before you start

In Adobe Experience Platform, create a schema by choosing the XDM ExperienceEvent option. For this example add the `Environment Details` mixin and create a custom mixin for product reviews containing the following fields: productSku, rating, ratingText, reviewerId. Then save the schema. 

Create a dataset based on this Schema, set it up in your Edge configuration in Adobe Launch UI and enable Adobe Experience Platform.

Next, create a mobile property and install the **Adobe Experience Platform Edge Network** extension and set up the Edge configuration created in the step above.

Import and register the AEP Edge extension in your client-side mobile implementation.

## Create Experience event

{% tabs %}
{% tab title="Android" %}

### Java

```java
Map<String, Object> reviewXdmData = new HashMap<>();
reviewXdmData.put("productSku", "demo123");
reviewXdmData.put("rating", 5);
reviewXdmData.put("reviewText", "I love this demo!");
reviewXdmData.put("reviewerId", "Anonymous user");

Map<String, Object> xdmData = new HashMap<>();
xdmData.put("eventType", "MyFirstXDMExperienceEvent");
xdmData.put(_yourTenantId, reviewXdmData);

ExperienceEvent experienceEvent = new ExperienceEvent.Builder()
                .setXdmSchema(xdmData)
                .build();
```

{% endtab %}

{% tab title="iOS" %}

### Swift

```swift
var xdmData : [String: Any] = [:]
xdmData["eventType"] = "MyFirstXDMExperienceEvent"
xdmData[_yourTenantId] = ["productSku": "demo123",
                          "rating": 5,
                          "reviewText": "I love this demo!",
                          "reviewerId": "Anonymous user"]
let experienceEvent = ExperienceEvent(xdm: xdmData)
```

### Objective-C

```objective-c
NSDictionary<NSString*, NSObject*>* xdmData;
[xdmData setValue:@"MyFirstXDMExperienceEvent" forKey:@"eventType"];
[xdmData setValue:@{@"productSku": @"demo123",
                    @"rating": @5,
                    @"reviewText": @"I love this demo!",
                    @"reviewerId": @"Anonymous user"}
				 	 forKey:_yourTenantId];
AEPExperienceEvent *experienceEvent = [[AEPExperienceEvent alloc] initWithXdm:xdmData data:nil datasetIdentifier:nil];
```

{% endtab %}
{% endtabs %}



## Send an Experience event to Adobe Experience Edge Network

Use the AEP Edge mobile extension to send the Experience event created in the previous step



{% tabs %}
{% tab title="Android" %}

#### Java

```java
Edge.sendEvent(experienceEvent, null);
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

```swift
Edge.sendEvent(experienceEvent: experienceEvent)
```

#### Objective-C

```objective-c
[AEPMobileEdge sendEventWithExperienceEvent:experienceEvent :nil];
```

{% endtab %}
{% endtabs %}

