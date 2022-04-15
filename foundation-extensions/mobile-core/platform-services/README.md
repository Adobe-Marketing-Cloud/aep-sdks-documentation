# Platform Services

The Platform Services are provided by the Adobe Experience Platform Mobile SDKs as part of the Mobile Core extension. These services provide shared functionality throughout the SDK that can be shared by extensions. For example, services provide shared functionality for networking, data queuing, caching, and more.

{% hint style="info" %}
This feature is only available in [Android Core 1.8.0](https://aep-sdks.gitbook.io/docs/release-notes#android-core-1-8-0) or later and [iOS Core 3.0.0](https://aep-sdks.gitbook.io/docs/release-notes#adobe-experience-platform-ios-core-sdks) or later.
{% endhint %}

| Service  | Android SDK | iOS SDK |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :---------------------------------------------------------- |
| [Networking](./network-service.md) | Core 1.8.0 + | AEPCore 3.0.0 + |
| [DataQueue](./data-queue-service.md) | Core 1.8.0 + | AEPCore 3.0.0 + |
| [SystemInfoService/DeviceInforming](./system-device-info-service.md) | Core 1.8.0 + | AEPCore 3.0.0 + |

## Accessing Services

The MobileCore extension provides a shared `ServiceProvider`, responsible for accessing the current set of provided services.

The following code snippet shows how to access `Network Service`  as an example.

{% tabs %}
{% tab title="Android" %}

```java
import com.adobe.marketing.mobile.services.*;

// Get an instance of the current network service
Networking networkService = ServiceProvider.getInstance().getNetworkService();
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

```swift
import AEPServices

// Get an instance of the current network service
let networkService = ServiceProvider.shared.networkService
```

{% endtab %}
{% endtabs %}

## Override network stack

This section walks through the steps necessary to create a custom network override, and register it with the SDK.

{% hint style="info" %}
This feature is only available in Android Core version 1.8.0 or later and iOS Core version 2.6.0 or later.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

### 1. Create custom HTTPConnectionPerformer implementation

The `HTTPConnectionPerformer` class is an abstract base class that must be subclassed. This class contains one required method, `connect`, which must be overridden. Optionally, it's possible to override the `shouldOverride` method if you want to conditionally override network requests (if you do not override this method, all requests will be overridden by default).

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
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider.Connecting;

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
        con.setDoOutput(true);
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
Your implementation must return an object conforming to the `Connection` interface when the connection has succeded. If the connection does not succeed, you will need to return these constants (depending on the scenario):

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
### 1. Conform to the ACPHttpConnectionPerformer protocol

The `ACPHttpConnectionPerformer` is a protocol which must be conformed to in order to override the network stack. It provides two methods which must be implemented:

1. `shouldOverride`, which takes a URL and an HTTP method. Return true if you want the network stack to be overridden by the performer, or false if not. 
2. `requestUrl`, which is the URL request override with a completion block.

### 2. Create an ACPHttpConnection and pass relevant data from your NSURLSessionDataTask completion block

The completion block for the `requestUrl` method takes an `ACPHttpConnection` as its parameter. The `ACPHttpConnection` is used when overriding the network stack in place of the internal network connection implementation and represents the response to an HTTP request. It is to be created using the NSURLResponse and NSData from your url request response. In the case of a Network Error, or timeout, the `ACPHttpConnection*` is expected to be nil.

#### Example

{% hint style="warning" %}
This is just an implementation example. For more information about handling network requests correctly in your mobile application, see [NSURLSessionConfiguration](https://developer.apple.com/documentation/foundation/nsurlsessionconfiguration) and [NSMutableURLRequest](https://developer.apple.com/documentation/foundation/nsmutableurlrequest).
{% endhint %}

**Objective-C**

```objectivec
#import <Foundation/Foundation.h>
#import "ACPNetworkServiceOverrider.h"

@interface SamplePerformerOverrider : NSObject<ACPHttpConnectionPerformer>

@end

@implementation SamplePerformerOverrider {
    void (^requestUrlCompletion)(ACPHttpConnection*);
}

  // Modifications here would allow for conditional overriding based on the url/method.
  // In this example it always returns true to override all network requests.
- (BOOL) shouldOverride: (NSURL*) url method: (NSString*) method {
    return true;
}

    // Network request override with a completion block. The provided parameters should be configured on the network request.
- (void) requestUrl: (NSURL*) url httpCommand: (NSString*) command connectPayload: (NSString*) payload requestPropertyDict: (NSDictionary<NSString*, NSString*>*) requestProperty connectTimeout: (NSTimeInterval) connectTimeout readTimeout: (NSTimeInterval) readTimeout completion: (void (^) (ACPHttpConnection*)) completion {

    requestUrlCompletion = completion;

    // Create the NSURLSessionConfiguration with the provided timeouts
    NSURLSessionConfiguration* config = [NSURLSessionConfiguration ephemeralSessionConfiguration];
    config.URLCache = nil;
    config.timeoutIntervalForRequest = readTimeout;
    config.timeoutIntervalForResource = connectTimeout;

    NSURLSession* session = [NSURLSession sessionWithConfiguration:config];

    // Create an NSURLRequest with the provided request parameters
    NSMutableURLRequest* request = [NSMutableURLRequest new];
    [request setCachePolicy:NSURLRequestReloadIgnoringLocalCacheData];
    [request setHTTPMethod:command];
    [request setURL:url];

      if (payload.length > 0 && [@"POST" isEqualToString:[command uppercaseString]]) {
       [request setHTTPBody:[payload dataUsingEncoding:NSUTF8StringEncoding]];
    }

    for (NSString *key in requestProperty) {
        NSString* value = requestProperty[key];
        [request setValue:value forHTTPHeaderField:key];
    }

    // Start the request
    NSURLSessionDataTask* task;
    task = [session dataTaskWithRequest:request
                      completionHandler: ^ (NSData * data, NSURLResponse * response, NSError * error) {
                if(!error) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;

            // ***** NOTE the creation of the ACPHttpConnection outlined in step 2.*****
            ACPHttpConnection* connOverride = [[ACPHttpConnection alloc] initWithResponse:httpResponse data:data];
            completion(connOverride); 
        } else {
            completion(nil);
        }
    }];
    [task resume];
}

@end
```

**Swift**

```swift
import Foundation
import ACPCore

class SamplePerformerOverrider: NSObject, ACPHttpConnectionPerformer {

    // Modifications here would allow for conditional overriding based on the url/method.
    // In this example it always returns true to override all network requests.
    func shouldOverride(_ url: URL, method: String) -> Bool {
      return true
    }

    // Network request override with a completion block. The provided parameters should be configured on the network request.
    func request(_ url: URL, httpCommand command: String, connectPayload payload: String, requestPropertyDict requestProperty: [String : String], connectTimeout: TimeInterval, readTimeout: TimeInterval, completion: @escaping (ACPHttpConnection?) -> Void) {

      // Create the URLSessionConfiguration with the provided timeouts
      let config = URLSessionConfiguration.ephemeral
      config.urlCache = nil
      config.timeoutIntervalForRequest = readTimeout
      config.timeoutIntervalForResource = connectTimeout

      let session = URLSession(configuration: config)

      // Create an NSURLRequest with the provided request parameters
      let request = NSMutableURLRequest.init(url: url)
      request.cachePolicy = NSURLRequest.CachePolicy.reloadIgnoringLocalCacheData
      request.httpMethod = command

      if !payload.isEmpty && "POST" == command.uppercased() {
        request.httpBody = payload.data(using: .utf8)
      }

      for property in requestProperty {
        request.setValue(property.value, forHTTPHeaderField: property.key)
      }

      // Start the request
      let task = session.dataTask(with: url, completionHandler: { (data, response, error) in
        if error == nil {
          let httpResponse = response as? HTTPURLResponse
          // create ACPHttpConnection object with the data received and call the completion handler
          let connectionOverride = ACPHttpConnection(response: httpResponse, data: data)
          completion(connectionOverride)
        } else {
          completion(nil)
        }
      })
      task.resume()
    }
}
```

### 3: Register your ACPHttpConnectionPerformer with the SDK

This step should occur prior to any other interactions with the AEP SDK. While it's possible to register the network override at any point during the application lifecycle, the override will only function for network requests performed after the registration has taken place.

#### Example

**Objective-C**

```objectivec
#import "SamplePerformerOverrider.h"
#import "ACPCore.h"

@implementation AppDelegate

-(BOOL)application:(UIApplication *)application 
didFinishLaunchingWithOptions:(NSDictionary<UIApplicationLaunchOptionsKey, id> *)launchOptions {
        ...
        [ACPNetworkServiceOverrider setHttpConnectionPerformer:[[SamplePerformerOverrider alloc] init]];
        ...
        [ACPCore start:^{
        ...
        }];
```

**Swift**

```swift
import ACPCore

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?
    func applicationDidFinishLaunching(_ application: UIApplication) {
        ...
        ACPNetworkServiceOverrider.setHttpConnectionPerformer(SamplePerformerOverrider())
        ACPCore.start {
        ...
        }
```
{% endtab %}
{% endtabs %}

