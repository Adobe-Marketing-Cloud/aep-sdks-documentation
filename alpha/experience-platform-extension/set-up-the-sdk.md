# Set up the SDK

In this section, we provide information to help you set up the SDK.

## Configure the Experience Platform extension

Before you can use the SDK, you must first set it up.

### Set up the required configuration

In your application's assets folder, configure a bundle configuration called `ADBMobileConfig.json` with the following content:

```
{
  "global.privacy": "optedin",
  "experienceCloud.org": "COMPANY_ORG_ID@AdobeOrg",
  "experiencePlatform.configId": "CONFIG_ID"
}
```

{% hint style="warning" %}
Replace the COMPANY_ORG_ID with your company's Adobe organization ID and CONFIG_ID with the Experience Platform configuration identifier for your schema and dataset.
{% endhint %}

### Register the extension

The `registerExtension()` API registers the Experience Platform extension with the Mobile Core extension. This API allows the extension to send and receive events to and from the Experience Platform Mobile SDK.

In the Application file's `onCreate()` method, register the Mobile Core and the Experience Platform extensions.

```java
public class ExperiencePlatformDemoApplication extends Application {
...
@Override
public void onCreate() {
	super.onCreate();
    MobileCore.setApplication(this);

	try {
    	// register Mobile Core extensions
        Identity.registerExtension();
        Signal.registerExtension();
        Lifecycle.registerExtension();
        
        // register the Experience Platform extension
        ExperiencePlatform.registerExtension();
   	} catch (InvalidInitException e) {
     	e.printStackTrace();
   	}

	MobileCore.start(new AdobeCallback() {
		@Override
		public void call(final Object o) {
			Log.d(LOG_TAG, "Mobile SDK was initialized.");
		}
	});
}
...
}
```



## Sending events

After you create an Experience Platform event, use `sendEvent` to send this event to the Adobe solutions for which you are provisioned and to the Experience Platform. For more information, see [Experience Platform event](./experience-platform-events.md).

**Syntax**

```java
public static void sendEvent(final ExperiencePlatformEvent experiencePlatformEvent, final ExperiencePlatformCallback responseCallback)
```

- _experiencePlatformEvent (required)_ event to be sent to Adobe Data Platform. It should not be null.
- _responseCallback (optional)_ callback to be invoked when the response handles are received from Adobe Data Platform. It can be called on a different thread and may be invoked multiple times.

**Example (commerce event)** 

```java
// create the ExperiencePlatformEvent for your use case
final String eventType = "commerce.productListAdds";
MobileSDKPlatformEventSchema xdmData = new MobileSDKPlatformEventSchema();
xdmData.setEventType(eventType);
xdmData.setCommerce(commerce);
xdmData.setProductListItems(itemsList);

ExperiencePlatformEvent event = new ExperiencePlatformEvent.Builder()
    .setXdmSchema(xdmData)
    .build();

// send the event to the Experience Platform extension
ExperiencePlatform.sendEvent(event, null);
```



## Retrieving data from Adobe solutions

As described in the [Sending events](#sending-events) section, `responseCallback` is an optional parameter. However, to be notified when a response is returned from the Adobe solutions, you can register a `responseCallback` that is invoked when new data is available from the server. This callback is called for each event handle that is returned by the server.

**Tip**: In Android, the event handle is represented by a `Map<String, Object>`.

Depending on the nature of the event, and the various Adobe solutions you enabled for your organization, you can receive one, multiple, or no event handles for each Experience Platform event.

For the best performance, the server-side event handle comes in chunks. As a result, the `responseCallback` is called multiple times.

```java
// create the ExperiencePlatformEvent for your use case
...
    
// send the event to the Experience Platform extension
ExperiencePlatform.sendEvent(event, new ExperiencePlatformCallback() {
    @Override
    public void onResponse(final Map<String, Object> data) {
        // TODO: handle the data received from the server
        Log.d(LOG_TAG, String.format("Received Data Platform response for event '%s': %s", eventType, data));
    }
});
```

For more information about about response and error response handling, see [Server response handling](./response-handling.md).