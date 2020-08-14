# Migrating from V4 Analytics to the AEP Analytics Extension

## Configuration

The AEP Analytics extension uses [Launch](https://launch.adobe.com/) to configure the AEP SDK's. This replaces the ADBMobileConfig.json which the V4 SDK used for configuration. To get started with the AEP SDK's:

1. Create a mobile property on Launch. See [Set up a mobile property](../../getting-started/create-a-mobile-property) for more information.
2. Configure your mobile app with the create mobile property. The AEP Mobile Core extension provides general functionality required by all the Adobe AEP extensions. The Configuration extension is buult into the Mobile Core and contains the `configureWithAppId` API. This API is used to link the Launch mobile property with your mobile app. The documentation for this API can be seen at the [Configuration API Reference](../../using-mobile-extensions/mobile-core/configuration/configuration-api-reference#configurewithappid) page. A code sample showing the usage of this API is provided below.

## API changes

For an overview of the API mapping between the V4 and AEP SDK's, see the [API Change Log](../../resources/upgrading-to-aep/api-change-log). This section will go over the Analytics specific changes made with the AEP Analytics extension.

#### Deprecated API

| API                                                          | Notes                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| trackActionFromBackground ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html)) | Deprecated                                                   |
| trackLocation:data: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/geo_poi.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/geo_poi.html)) | This functionality is available in the [Places extension](../../using-mobile-extensions/adobe-places). |
| trackBeacon:Data: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)) | Support modified, [see guide](https://aep-sdks.gitbook.io/docs/resources/user-guides/track-beacon) |
| trackingClearCurrentBeacon ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)) | Support modified, [see guide](https://aep-sdks.gitbook.io/docs/resources/user-guides/track-beacon) |
| trackLifetimeValueIncrease:data: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/lifetime_value.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/lifetime_value.html)) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics) and [User Profile](../../using-mobile-extensions/profile) extensions. |
| trackTimedActionStart: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics) and [User Profile](../../using-mobile-extensions/profile) extensions. |
| trackTimedActionUpdate: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics) and [User Profile](../../using-mobile-extensions/profile) extensions. |
| trackTimedActionEnd: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics) and [User Profile](../../using-mobile-extensions/profile) extensions. |
| trackTimedActionExists: ([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics) and [User Profile](../../using-mobile-extensions/profile) extensions. |

#### Android

##### Register the AEP Extensions and link the app to the configuration created on Launch

In your App's Application class add the extension registration code:

```java
@Override
public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.main);

  MobileCore.setApplication(getApplication());
  MobileCore.setLogLevel(LoggingMode.DEBUG);
  try {
    Analytics.registerExtension();
    Identity.registerExtension();
    MobileCore.start(new AdobeCallback() {
      @Override
      public void call(Object o) {
        // add your app id from the "Environments" tab on Launch.
        MobileCore.configureWithAppID("your-app-id");
      }
    });
  } catch (InvalidInitException e) {
    e.printStackTrace();
  }
}
```

In-depth instructions can be seen at the [Analytics Readme](../../using-mobile-extensions/adobe-analytics/readme.md#add-analytics-to-your-app).

##### Track App State and Track App Actions changes

The V4 syntax and usage examples for these API are:

```java
public static void trackState(final String state, final Map<String, Object> contextData)
Analytics.trackState("MainActivity", new HashMap<String, Object>() {{
  put("firstVisit", true);
}});
```

```java
public static void trackAction(final String action, final Map<String, Object> contextData)
Analytics.trackAction("linkClicked", new HashMap<String, Object>() {{
  put("url", "https://www.adobe.com");
}});
```

The AEP SDK's have moved the `trackAction` and `trackState` APIs to the MobileCore extension. In addition, the context data Map has been changed from `<String, Object>` to `<String, String>`: 

```java
public static void trackState(final String state, final Map<String, String> contextData)
MobileCore.trackState("MainActivity", new HashMap<String, String>() {{
  put("firstVisit", "true");
}});
```

```java
public static void trackAction(final String action, final Map<String, String> contextData)
MobileCore.trackAction("linkClicked", new HashMap<String, String>() {{
  put("url", "https://www.adobe.com");
}});
```

#### iOS

# TODO

