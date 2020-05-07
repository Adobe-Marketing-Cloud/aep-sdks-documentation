# Platform Services

Currently, the AEP SDK only provides the capability for overriding the Adobe-provided network stack \(for all Adobe extensions\).

## Override network stack

This section walks through the steps necessary to create a custom network override, and register it with the SDK.

{% hint style="info" %}
This feature is only available in Android Core version 2.5.0 or later and iOS Core version 2.6.0 or later.
{% endhint %}



{% tabs %}
{% tab title="Android" %}

### 1. Create custom HTTPConnectionPerformer implementation

The `HTTPConnectionPerformer` class is an abstract base class that must be subclassed. This class contains one required method, `connect`, which must be overridden. Optionally, it's possible to override the `shouldOverride` method if you want to conditionally override network requests \(if you do not override this method, all requests will be overridden by default\).

#### Example

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
  // (blocking) network request.  Upon success, return an object conforming to the
  // Connection interface.  Upon error, return one of these values:
  //  - URL Parsing / Malformed issues - CONNECTION_ERROR_URL
  //  - IO / Other errors - CONNECTION_ERROR_IO
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

### 1. Conform to the ACPHttpConnectionPerformer protocol

The `ACPHttpConnectionPerformer` is a protocol which must be conformed to in order to override the network stack. It provides two methods which must be implemented:

1. `shouldOverride`, which takes a URL and an HTTP method. Return true if you want the network stack to be overridden by the performer, or false if not. 
2. `requestUrl`, which is the URL request override with a completion block.

### 2. Create an ACPHttpConnection and pass relevant data from your NSURLSessionDataTask completion block

The completion block for the `requestUrl` method takes an `ACPHttpConnection` as its parameter. The `ACPHttpConnection` is used when overriding the network stack in place of the internal network connection implementation and represents the response to an HTTP request. It is to be created using the NSURLResponse and NSData from your url request response. In the case of a Network Error, or timeout, the `ACPHttpConnection*` is expected to be nil.

#### Example

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
class SamplePerformerOverrider: ACPHttpConnectionPerformer {
    func shouldOverride(_ url: URL, method: String) -> Bool {
        return true
    }

    func request(_ url: URL, httpCommand command: String, connectPayload payload: String, requestPropertyDict requestProperty: [String : String], connectTimeout: TimeInterval, readTimeout: TimeInterval, completion: @escaping (ACPHttpConnection?) -> Void) {
        //...
        let session = URLSession()
        _ = session.dataTask(with: url) { (data, response, error) in
            let httpResponse = response as! HTTPURLResponse
            let connectionOverride = ACPHttpConnection(response: httpResponse, data: data)
            if let error = error {
                // Handle error
                completion(nil)
            } else {
                completion(connectionOverride)
            }
        }
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