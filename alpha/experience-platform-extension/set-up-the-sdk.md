# Set up the SDK

## Configure the Experience Platform extension

### Set up the required configuration

Configure a bundle configuration called `ADBMobileConfig.json` in your application's assets folder, with the following content: 

```
{
  "global.privacy": "optedin",
  "experienceCloud.org": "COMPANY_ORG_ID@AdobeOrg",
  "experiencePlatform.configId": "CONFIG_ID"
}
```

{% hint style="warning" %}
Replace COMPANY_ORG_ID with your company's Adobe organization ID and CONFIG_ID with the Data Platform configuration identifier for your Schema and Dataset.
{% endhint %}

### Register the extension

The `registerExtension()` API registers the Identity extension with the MobileCore extension. This API allows the extension to send and receive events to and from the Experience Platform Mobile SDK.

In the Application file _onCreate()_ method, register the Mobile Core and the Experience Platform extensions.

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

Once an [Experience Platform Event](./experience-platform-events.md) is created, it can be sent to the Adobe Solutions you are provisioned with and the Adobe Data Platform using the `sendEvent` API of the Experience Platform extension.

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

As described in the [Sending events](#sending-events) section, the _responseCallback_ is an optional parameter. However, if you would like to get notified when a response is returned from the Adobe solutions, you can register a _responseCallback_ that will be invoked whenever new data is available from the server. This callback is called for each event handle returned by the server, which in Android is represented by a Map<String, Object>.

Based of the nature of the event and the various Adobe solutions you have enabled for your organization, for each Experience Platform event you can receive one, multiple or no event handles.

For optimized performance, the server side event handle comes in a chunks, so you should expect that the responseCallback is called multiple times.

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