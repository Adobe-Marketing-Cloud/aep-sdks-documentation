# Adobe Mobile Services

[Adobe Mobile Services](https://marketing.adobe.com/resources/help/en_US/mobile/home.html) brings together mobile marketing capabilities for mobile applications from across the Adobe Experience Cloud, which allows you to understand and improve user engagement with your mobile applications.

## **Configure Adobe Mobile Services Extension in Launch**

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Mobile Services** extension and click **Install**.
3. Provide extension settings \(see [Configure Mobile Services Extension](./#configure-mobile-servicces-extension)\)
4. Click **Save**.
5. Follow the publishing process, to update SDK configuration.

#### **Acquisition Timeout**

Time in seconds to wait for acquisition information before sending the First Launch hit. The default is 5 seconds.

For more detail, see [Timeout Reference](https://marketing.adobe.com/resources/help/en_US/mobile/t_config_acquisition.html)

#### **Acquisition App Id**

It uniquely identifies the app on the acquisition server. It is the “appid” value from the “acquisition” section in your ADBMobileConfig.json file. 

For more detail, refer [ADBMobileConfig](https://marketing.adobe.com/resources/help/en_US/mobile/android/json_config.html)

```text
"acquisition": {
  "server": "c00.adobe.com",
  "appid": "2f9f3fdae7fa090182acac1d8da79c418762e378d3c5762521afa1470f81625a"
}
```

#### **Messages Url**

URL to the set of messages. It is the “messages” value from the “remotes” section in your ADBMobileConfige.json file.

For more detail, refer [ADBMobileConfig](https://marketing.adobe.com/resources/help/en_US/mobile/android/json_config.html)

```text
"remotes": {
  "analytics.poi": "https://assets.adobedtm.com/b213090c5204bf94318f4ef0539a38b487d10368/scripts/satellite-5b3fd2fe64746d6b3d000ea7.json",
  "messages": "https://assets.adobedtm.com/b213090c5204bf94318f4ef0539a38b487d10368/scripts/satellite-5b3fd2fe64746d3f750041d2.json"
}
```
