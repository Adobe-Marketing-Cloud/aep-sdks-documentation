# Platform Services

Currently, the AEP SDK only provides the capability for overriding the Adobe-provided network stack \(for all Adobe extensions\).

## Override network stack

This section walks through the steps necessary to create a custom network override, and register it with the SDK.

{% hint style="info" %}
This feature is only available in Android Core version 2.5.0 or later and iOS Core version 3.0.0 or later.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### 1. Create custom HTTPConnectionPerformer implementation

The `HTTPConnectionPerformer` class is an abstract base class that must be subclassed. This class contains one required method, `connect`, which must be overridden. Optionally, it's possible to override the `shouldOverride` method if you want to conditionally override network requests \(if you do not override this method, all requests will be overridden by default\).

#### Example

{% hint style="warning" %}
This is just an implementation example. For more information about handling network requests correctly in your mobile application, see [HttpURLConnection](https://developer.android.com/reference/java/net/HttpURLConnection).
{% endhint %}

```java
package com.adobe.example;

import java.io.BufferedOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Map;
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider.HTTPConnectionPerformer;
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider.Connection;

// Sample implementation of HTTPConnectionPerformer for AEP SDK Network Override.
class SampleHTTPConnectionPerformer extends HTTPConnectionPerformer {        
  // Modifications here would allow for conditional overriding based on the url/method.
  // Overriding this method is optional, by default it will always return true (meaning
  // all network requests should be overridden).
  @Override
  public boolean shouldOverride(String url, String method) {
    return true;
  }

  // Overriding the connect method is required.  This method must perform a synchronous
  // (blocking) network request and return an object conforming to the
  // Connection interface.
  @Override
  public Connection connect(String url, String method, byte[] payload, Map<String, String> headers, int connectionTimeoutSeconds, int readTimeoutSeconds) {
    try {
      final URL dest = new URL(url);
      final HttpURLConnection con = (HttpURLConnection) dest.openConnection();
      con.setReadTimeout(readTimeoutSeconds * 1000);
      con.setConnectTimeout(connectionTimeoutSeconds * 1000);

      con.setRequestMethod(method);

      for (final Map.Entry<String, String> entry : headers.entrySet()) {
        con.setRequestProperty(entry.getKey(), entry.getValue());
      }

      if (method.equals("POST") && payload != null) {
        con.setFixedLengthStreamingMode(payload.length);
      }

      con.connect();

      if (method.equals("POST") && payload != null) {
        final OutputStream os = new BufferedOutputStream(con.getOutputStream());
        os.write(payload);
        os.flush();
        os.close();
      }

      final InputStream inputStream = con.getInputStream();
      final int responseCode = con.getResponseCode();
      final String responseMessage = con.getResponseMessage();

      return new AndroidNetworkServiceOverrider.Connection() {
        @Override
        public InputStream getInputStream() {
          return inputStream;
        }

        @Override
        public int getResponseCode() {
          return responseCode;
        }

        @Override
        public String getResponseMessage() {
          return responseMessage;
        }

        @Override
        public String getResponsePropertyValue(String responsePropertyKey) {
          final String responseHeaderValue = con.getHeaderField(responsePropertyKey);
          return responseHeaderValue;
        }

        @Override
        public void close() {
          if (inputStream != null) {
            try {
              inputStream.close();
            } catch (final Exception ex) {
            }
          }
          con.disconnect();
        }
      };


    } catch (final MalformedURLException ex) {
      return CONNECTION_ERROR_URL;

    } catch (final IOException ex) {
      return CONNECTION_ERROR_IO;
    }
  }
}
```

{% hint style="info" %}
Your implementation must return an object conforming to the `Connection` interface when the connection has succeded. If the connection does not succeed, you will need to return these constants \(depending on the scenario\):

* For all URL parsing / malformed URL issues, return `HTTPConnectionPerformer.CONNECTION_ERROR_URL`. 
* For any IOExceptions or any other errors, return `HTTPConnectionPerformer.CONNECTION_ERROR_IO`.
{% endhint %}

### 2. Register your interface with the SDK.

This step should occur prior to any other interactions with the AEP SDK. While it's possible to register the network override at any point during the application lifecycle, the override will only function for network requests performed after the registration has taken place.

```java
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider;
import com.adobe.marketing.mobile.MobileCore;

public void onCreate() {
    super.onCreate();

  // Register network override prior to making any other calls to the AEP SDK
  AndroidNetworkServiceOverrider.setHTTPConnectionPerformer(new SampleHTTPConnectionPerformer());

  // First call to AEP SDK
  MobileCore.setApplication(this);
  //... continue with initialization / registering extensions.
}
```
{% endtab %}

{% tab title="iOS" %}
TBD

{% endtab %}
{% endtabs %}

