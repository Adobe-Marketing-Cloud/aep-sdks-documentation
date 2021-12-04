# Media Analytics API reference

## extensionVersion

The `extensionVersion()` API returns the version of the Media extension that is registered with the Mobile Core extension.

{% tabs %}
{% tab title="Android" %}
### Java

```java
String mediaExtensionVersion = Media.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

```swift
let mediaExtensionVersion  = Media.extensionVersion()
```

### Objective-C

```objc
NSString *mediaExtensionVersion = [AEPMobileMedia extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### Swift

```swift
let mediaExtensionVersion  = ACPMedia.extensionVersion()
```

### Objective-C

```objc
NSString *mediaExtensionVersion = [ACPMedia extensionVersion];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPMedia.extensionVersion().then(mediaExtensionVersion => console.log("AdobeExperienceSDK: ACPMedia version: " + mediaExtensionVersion));
```
{% endtab %}
{% endtabs %}

### createTracker

{% hint style="warning" %}
The API createTracker with callback has been deprecated.
{% endhint %}

This API creates a media tracker instance that tracks the playback session. The tracker created should be used to track the streaming content and it sends periodic pings to the media analytics backend.

{% tabs %}
{% tab title="Android" %}
#### Java

The createTracker function returns the instance of `MediaTracker` for tracking a media session.

{% hint style="warning" %}
If MobileCore.resetIdentities() is called in the implementation, the existing tracker will stop sending pings. You will need to create a new tracker to generate a new media session.

Please note that the createTracker function with a callback has been **deprecated**.
{% endhint %}

**Syntax**

```java
public static MediaTracker createTracker()

// Deprecated
public static void createTracker(AdobeCallback<MediaTracker> callback)
```

**Example**

```java
MediaTracker mediaTracker = Media.createTracker();  // Use the instance for tracking media.

// Deprecated
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker mediaTracker) {
        // Use the instance for tracking media.
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Creates a media tracker instance that tracks the playback session. The tracker created should be used to track the streaming content and it sends periodic pings to the media analytics backend.

{% hint style="warning" %}
If MobileCore.resetIdentities() is called in the implementation, the existing tracker will stop sending pings. You will need to create a new tracker to generate a new media session.
{% endhint %}

#### Swift

**Syntax**

```swift
static func createTracker()
```

**Example**

```swift
let tracker = Media.createTracker()  // Use the instance for tracking media.
```

#### Objective-C

**Example**

```objc
id<AEPMediaTracker> tracker; 
_tracker = [AEPMobileMedia createTracker];  // Use the instance for tracking media.
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
The createTracker function returns an instance of ACPMediaTracker for tracking a media session. 

{% hint style="warning" %}
The createTracker function with callback as a parameter has been deprecated.
{% endhint %}

#### Objective-C

**Syntax**

```objc
+(ACPMediaTracker* _Nullable) createTracker;

// Deprecated
+(void) createTracker: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;
```

**Example**

```objc
ACPMediaTracker *mediaTracker = [ACPMedia createTracker];  // Use the instance for tracking media.


// Deprecated
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

#### Swift

```swift
let mediaTracker = ACPMedia.createTracker()  // Use the instance for tracking media.

// Deprecated
ACPMedia.createTracker({mediaTracker in
    // Use the instance for tracking media.
})
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
createTracker();
```

**Example**

```jsx
ACPMedia.createTracker().then(tracker =>
  this.setState({currentTracker: tracker})
);
```
{% endtab %}
{% endtabs %}

### createTrackerWithConfig

Creates a media tracker instance based on the configuration to track the playback session.

| **Key** | **Required** | **Type** | **Description** |
| :--- | :--- | :--- | :---: |
| `config.channel` | No | String | Channel name for media. Set this to overwrite the channel name configured from launch for media tracked with this tracker instance. |
| `config.downloadedcontent` | No | Boolean | Creates a tracker instance to track downloaded media. Instead of sending periodic pings, the tracker only sends one ping for the entire content. |

{% tabs %}
{% tab title="Android" %}
This function creates a configured media tracker to track a media session.

{% hint style="warning" %}
The `createTracker` function with a callback as a parameter has been **deprecated**.
{% endhint %}

#### Java

**Syntax**

```java
public class MediaConstants {

    public static final class Config {
        public static final String CHANNEL = "config.channel";
        public static final String DOWNLOADED_CONTENT = "config.downloadedcontent";
    }

}

public static MediaTracker createTracker(Map<String, Object> config)

// Deprecated
public static void createTracker(Map<String, Object> config, final AdobeCallback<MediaTracker> callback)
```

| **Variable** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `config` | Map<String, Object> | A configuration object. Contains information about the channel and the downloaded content. |

**Example**

```java
HashMap<String, Object> config = new HashMap<String, Object>();
config.put(MediaConstants.Config.CHANNEL, "custom-channel");  // Override channel configured from launch
config.put(MediaConstants.Config.DOWNLOADED_CONTENT, true);   // Creates downloaded content tracker


MediaTracker mediaTracker = Media.createTracker(config);  // Use the instance for tracking media.

// Deprecated
Media.createTracker(config, new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker mediaTracker) {
        // Use the instance for tracking media.
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
This function creates a media tracker instance, based on the configuration, to track the playback session.

#### Swift

**Syntax**

```swift
static func createTrackerWith(config: [String: Any]?)
```

**Example**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.CHANNEL] = "custom-channel" // Overrides channel configured from launch
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true    // Creates downloaded content tracker

let tracker = Media.createTrackerWith(config: config)
```

#### Objective-C

**Example**

```objc
id<AEPMediaTracker> _tracker; 
NSMutableDictionary* config = [NSMutableDictionary dictionary];

config[AEPMediaTrackerConfig.CHANNEL] = @"custom-channel"; // Overrides channel configured from launch
config[AEPMediaTrackerConfig.DOWNLOADED_CONTENT] = [NSNumber numberWithBool:true]; // Creates downloaded content tracker

_tracker = [AEPMobileMedia createTrackerWithConfig:config];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
This function creates a configured media tracker to track a media session.

{% hint style="warning" %}
The `createTracker` function with a callback as a parameter has been **deprecated**.
{% endhint %}

#### Objective-C

**Syntax**

```objc
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyConfigChannel;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyConfigDownloadedContent;

+ (ACPMediaTracker* _Nullable) createTrackerWithConfig: (NSDictionary* _Nullable) config;

// Deprecated
+ (void) createTrackerWithConfig: (NSDictionary* _Nullable) config
                        callback: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;
```

**Example**

```objc
NSMutableDictionary* config = [NSMutableDictionary dictionary];
config[ACPMediaKeyConfigChannel] = @"custom-channel"; // Override channel configured from launch
config[ACPMediaKeyConfigDownloadedContent] = @YES;    // Creates downloaded content tracker

ACPMediaTracker *mediaTracker = [ACPMedia createTrackerWithConfig:config]; // Use the instance for tracking media.

// Deprecated
[ACPMedia createTrackerWithConfig: config
                         callback:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

#### Swift

**Example**

```swift
var config: [String: Any] = [:]
config[ACPMediaKeyConfigChannel] = "custom-channel"  // Override channel configured from launch
config[ACPMediaKeyConfigDownloadedContent] = true    // Creates downloaded content tracker

let mediaTracker = ACPMedia.createTrackerWithConfig(config); // Use the instance for tracking media.

// Deprecated
ACPMedia.createTrackerWithConfig(config, {mediaTracker in
    // Use the instance for tracking media.
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Example**

```jsx
var config = new Object();
config[ACPMediaConstants.ACPMediaKeyConfigChannel] = "customer-channel";  // Override channel configured from launch
config[ACPMediaConstants.ACPMediaKeyConfigDownloadedContent] = true;  // Creates downloaded content tracker
ACPMedia.createTrackerWithConfig(config).then(tracker =>
  this.setState({currentTracker: tracker})
);
```
{% endtab %}
{% endtabs %}

### createMediaObject

Creates an instance of the Media object.

{% tabs %}
{% tab title="Android" %}
Returns a HashMap instance that contains information about the media.

#### Java

**Syntax**

```java
public static HashMap<String, Object> createMediaObject(
    String name, String mediaId, Double length, String streamType, MediaType mediaType
);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | The media's name |
| `mediaId` | Yes | String | The media's unique identifier |
| `length` | Yes | Double | The media's length |
| `streamType` | Yes | String | An enum that represents the media's stream type. More information, including possible values, can be found in the [stream type section](#stream-type). |
| `mediaType` | Yes | MediaType | An enum that represents the media's type. More information, including possible values, can be found in the [media type section](#media-type). |

**Example**

```java
HashMap<String, Object> mediaInfo = Media.createMediaObject("video-name",
                                                            "video-id",
                                                            60D,
                                                            MediaConstants.StreamType.VOD,
                                                            Media.MediaType.Video);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Returns a map that contains information about the media.

#### Swift

**Syntax**

```swift
static func createMediaObjectWith(name: String, 
                                    id: String, 
                                length: Double, 
                            streamType: String,
                             mediaType: MediaType) -> [String: Any]?
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | The media's name |
| `id` | Yes | String | The media's unique identifier |
| `length` | Yes | Double | The media's length |
| `streamType` | Yes | String | An enum that represents the media's stream type. More information, including possible values, can be found in the [stream type section](#stream-type). |
| `mediaType` | Yes | MediaType | An enum that represents the media's type. More information, including possible values, can be found in the [media type section](#media-type). |

**Example**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-name",
                                                id: "videoId", 
                                            length: 60,
                                        streamType: MediaConstants.StreamType.VOD, 
                                         mediaType: MediaType.Video)
```

#### Objective-C

**Example**

```objc
NSDictionary *mediaObject = [AEPMobileMedia createMediaObjectWith:@"video-name"
                                                                id:@"video-id" 
                                                            length:60 
                                                        streamType:AEPMediaStreamType.VOD
                                                         mediaType:AEPMediaTypeVideo];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
Returns an NSDictionary instance that contains information about the media.

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createMediaObjectWithName: (NSString* _Nonnull) name
                                             mediaId: (NSString* _Nonnull) mediaId
                                              length: (double) length
                                          streamType: (NSString* _Nonnull) streamType
                                           mediaType: (ACPMediaType) mediaType;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | The media's name |
| `mediaId` | Yes | String | The media's unique identifier |
| `length` | Yes | Double | The media's length |
| `streamType` | Yes | String | An enum that represents the media's stream type. More information, including possible values, can be found in the [stream type section](#stream-type). |
| `mediaType` | Yes | MediaType | An enum that represents the media's type. More information, including possible values, can be found in the [media type section](#media-type). |

**Example**

```objc
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName: @"video-name"
                                                        mediaId: @"video-id"
                                                         length: 60
                                                     streamType: ACPMediaStreamTypeVod
                                                      mediaType: ACPMediaTypeVideo];
```

**Swift**

```swift
let mediaObject = ACPMedia.createMediaObject(withName: "video-name", mediaId: "video-id",
                                               length: Double(60),
                                           streamType: ACPMediaStreamTypeVod,
                                            mediaType:ACPMediaType.video)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
createMediaObject(String mediaName, String mediaId, int length, String streamType, String mediaType);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | The media's name |
| `id` | Yes | String | The media's unique identifier |
| `length` | Yes | Double | The media's length |
| `streamType` | Yes | String | An enum that represents the media's stream type. More information, including possible values, can be found in the [stream type section](#stream-type). |
| `mediaType` | Yes | MediaType | An enum that represents the media's type. More information, including possible values, can be found in the [media type section](#media-type). |

**Example**

```jsx
let mediaObject = ACPMedia.createMediaObject("video-name", "video-id", 60, ACPMediaConstants.ACPMediaStreamTypeVod, ACPMediaType.Video);
```
{% endtab %}
{% endtabs %}

### createAdBreakObject

Creates an instance of the AdBreak object.

{% tabs %}
{% tab title="Android" %}
Returns a HashMap instance that contains information about the ad break.

#### Java

**Syntax**

```java
public static HashMap<String, Object> createAdBreakObject(String name, Long position, Double startTime);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Ad break name such as pre-roll, mid-roll, and post-roll. |
| `position` | Yes | Long |The number position of the ad break within the content, starting with 1. |
| `startTime` | Yes | Double | Playhead value at the start of the ad break. |


**Example**

```java
HashMap<String, Object> adBreakObject = Media.createAdBreakObject("adbreak-name", 1L, 0D);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Returns a map that contains information about the ad break.

#### Swift

**Syntax**

```swift
static func createAdBreakObjectWith(name: String,
                                position: Int, 
                                startTime: Double) -> [String: Any]?
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Ad break name such as pre-roll, mid-roll, and post-roll. |
| `position` | Yes | Int |The number position of the ad break within the content, starting with 1. |
| `startTime` | Yes | Double | Playhead value at the start of the ad break. |

**Example**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "adbreak-name", 
                                              position: 1, 
                                             startTime: 0)
```

#### Objective-C

**Example**

```objc
NSDictionary *adBreakObject = [AEPMobileMedia createAdBreakObjectWith:@"adbreak-name" 
                                                             position:1 
                                                            startTime:0];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
Returns an NSDictionary instance that contains information about the ad break.

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createAdBreakObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                             startTime: (double) startTime;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Ad break name such as pre-roll, mid-roll, and post-roll. |
| `position` | Yes | Double |The number position of the ad break within the content, starting with 1. |
| `startTime` | Yes | Double | Playhead value at the start of the ad break. |

**Example**

```objc
NSDictionary *adBreakObject = [ACPMedia createAdBreakObjectWithName: @"adbreak-name"
                                                           position: 1
                                                          startTime: 0];
```

#### Swift

**Example**

```swift
let adBreakObject = ACPMedia.createAdBreakObject(withName: "adbreak-name", position: 1, startTime: 0)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Example**

```jsx
let adBreakObject = ACPMedia.createAdBreakObject("adbreak-name", 1, 0);
```
{% endtab %}
{% endtabs %}

### createAdObject

Creates an instance of the Ad object.

{% tabs %}
{% tab title="Android" %}
Returns a HashMap instance that contains information about the ad.

#### Java

**Syntax**

```java
public static HashMap<String, Object> createAdObject(String name, String adId, Long position, Double length);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Friendly name of the ad. |
| `adId` | Yes | String | Unique identifier for the ad. |
| `position` | Yes | Long | The number position of the ad within the ad break, starting with 1. |
| `length` | Yes | Double | Ad length |

**Example**

```java
HashMap<String, Object> adInfo = Media.createAdObject("ad-name", "ad-id", 1L, 15D);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Returns a map that contains information about the ad.

#### Swift

**Syntax**

```swift
static func createAdObjectWith(name: String, 
                                 id: String, 
                           position: Int, 
                             length: Double) -> [String: Any]?
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Friendly name of the ad. |
| `adId` | Yes | String | Unique identifier for the ad. |
| `position` | Yes | Int | The number position of the ad within the ad break, starting with 1. |
| `length` | Yes | Double | Ad length |


**Example**

```swift
let adObject = Media.createObjectWith(name: "ad-name", 
                                        id: "ad-id", 
                                  position: 0, 
                                    length: 30)
```

#### Objective-C

**Example**

```objc
NSDictionary *adObject = [AEPMobileMedia createAdObjectWith:@"ad-name" 
                                                         id:@"ad-id" 
                                                   position:0 
                                                     length:30];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
Returns an NSDictionary instance that contains information about the ad.

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createAdObjectWithName: (NSString* _Nonnull) name
                                             adId: (NSString* _Nonnull) adId
                                         position: (double) position
                                           length: (double) length;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Friendly name of the ad. |
| `adId` | Yes | String | Unique identifier for the ad. |
| `position` | Yes | Double | The number position of the ad within the ad break, starting with 1. |
| `length` | Yes | Double | Ad length |

**Example**

```objc
NSDictionary *adObject = [ACPMedia createAdObjectWithName: @"ad-name"
                                                     adId: @"ad-id"
                                                 position: 1
                                                   length: 15];
```

#### Swift

**Example**

```swift
let adObject = ACPMedia.createAdObject(withName: "ad-name", adId: "ad-id", position: 1, length: 15)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
createAdObject(String name, String adId, Number position, Number length);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Friendly name of the ad. |
| `adId` | Yes | String | Unique identifier for the ad. |
| `position` | Yes | Number | The number position of the ad within the ad break, starting with 1. |
| `length` | Yes | Number | Ad length |

**Example**

```jsx
let adObject = ACPMedia.createAdObject("ad-name", "ad-id", 1, 15);
```
{% endtab %}
{% endtabs %}

### createChapterObject

Creates an instance of the Chapter object.

{% tabs %}
{% tab title="Android" %}
Returns a HashMap instance that contains information about the chapter.

#### Java

**Syntax**

```java
public static HashMap<String, Object> createChapterObject(String name,
                                                          Long position,
                                                          Double length,
                                                          Double startTime);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Chapter name |
| `position` | Yes | Long | The number position of the chapter within the content, starting with 1. |
| `length` | Yes | Double | Chapter length |
| `startTime` | Yes | Double | Playhead value at the start of the chapter |

**Example**

```java
HashMap<String, Object> chapterInfo = Media.createChapterObject("chapter-name", 1L, 60D, 0D);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Returns a map that contains information about the chapter.

#### Swift

**Syntax**

```swift
static func createChapterObjectWith(name: String, 
                                position: Int, 
                                  length: Double, 
                               startTime: Double) -> [String: Any]?
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Chapter name |
| `position` | Yes | Int | The number position of the chapter within the content, starting with 1. |
| `length` | Yes | Double | Chapter length |
| `startTime` | Yes | Double | Playhead value at the start of the chapter |

**Example**

```swift
let chapterObject = Media.createChapterObjectWith(name: "chapter_name", 
                                              position: 1, 
                                                length: 60, 
                                             startTime: 0)
```

#### Objective-C

**Example**

```objc
NSDictionary *chapterObject = [AEPMobileMedia createChapterObjectWith:@"chapter_name" 
                                                             position:1 
                                                               length:60 
                                                            startTime:0];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
Returns an NSDictionary instance that contains information about the chapter.

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createChapterObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                                length: (double) length
                                             startTime: (double) startTime;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Chapter name |
| `position` | Yes | Double | The number position of the chapter within the content, starting with 1. |
| `length` | Yes | Double | Chapter length |
| `startTime` | Yes | Double | Playhead value at the start of the chapter |

**Example**

```objc
NSDictionary *chapterObject = [ACPMedia createChapterObjectWithName: @"chapter-name"
                                                           position: 1
                                                             length: 60
                                                          startTime: 0];
```

#### Swift

**Example**

```swift
let chapterObject = ACPMedia.createChapterObject(withName: "chapter-name", position: 1, length: 60, startTime: 0)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
createChapterObject(String name, Number position, Number length, Number startTime);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `name` | Yes | String | Chapter name |
| `position` | Yes | Number | The number position of the chapter within the content, starting with 1. |
| `length` | Yes | Number | Chapter length |
| `startTime` | Yes | Number | Playhead value at the start of the chapter |

**Example**

```jsx
let chapterObject = ACPMedia.createChapterObject('chapter-name', 1, 60, 0);
```
{% endtab %}
{% endtabs %}

### createQoEObject

Creates an instance of the quality of experience (QoE) object.


{% hint style="info" %}
All the QoE values `bitrate`, `startupTime`, `fps`, `droppedFrames` would be converted to `long` for reporting purposes.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Returns a HashMap instance that contains information about the quality of experience.

#### Java

**Syntax**

```java
public static HashMap<String, Object> createQoEObject(Long bitrate,
                                                      Double startupTime,
                                                      Double fps,
                                                      Long droppedFrames);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `bitrate` | Yes | Long | Current bitrate |
| `startupTime` | Yes | Double | Startup time |
| `fps` | Yes | Double | FPS value |
| `droppedFrames` | Yes | Long | Number of dropped frames |

**Example**

```java
HashMap<String, Object> qoeInfo = Media.createQoEObject(10000000L, 2D, 23D, 10D);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Returns a map that contains information about the quality of experience.

#### Swift

**Syntax**

```swift
static func createQoEObjectWith(bitrate: Double, 
                            startupTime: Double, 
                                    fps: Double, 
                          droppedFrames: Double) -> [String: Any]?
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `bitrate` | Yes | Double | Current bitrate |
| `startupTime` | Yes | Double | Startup time |
| `fps` | Yes | Double | FPS value |
| `droppedFrames` | Yes | Double | Number of dropped frames |

**Example**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 500000, 
                                      startupTime: 2, 
                                              fps: 24, 
                                    droppedFrames: 10)
```

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createQoEObjectWith: (double) bitrate
                                          startupTime: (double) startupTime
                                                  fps: (double) fps
                                        droppedFrames: (double) droppedFrames;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `bitrate` | Yes | Double | Current bitrate |
| `startupTime` | Yes | Double | Startup time |
| `fps` | Yes | Double | FPS value |
| `droppedFrames` | Yes | Double | Number of dropped frames |

**Example**

```objc
NSDictionary *qoeObject = [AEPMobileMedia createQoEObjectWith:50000 
                                                    startTime:2 
                                                          fps:24 
                                                droppedFrames:10];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
Returns an NSDictionary instance that contains information about the quality of experience.

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createQoEObjectWithBitrate: (double) bitrate
                                          startupTime: (double) startupTime
                                                  fps: (double) fps
                                        droppedFrames: (double) droppedFrames;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `bitrate` | Yes | Double | Current bitrate |
| `startupTime` | Yes | Double | Startup time |
| `fps` | Yes | Double | FPS value |
| `droppedFrames` | Yes | Double | Number of dropped frames |

**Example**

```objc
NSDictionary *qoeObject = [ACPMedia createQoEObjectWithBitrate: 10000000
                                                   startupTime: 2
                                                           fps: 23
                                                 droppedFrames: 10];
```

#### Swift

**Syntax**

```swift
static func createQoEObjectWithBitrate(bitrate: Double, 
                            startupTime: Double, 
                                    fps: Double, 
                          droppedFrames: Double) -> [String: Any]?
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `bitrate` | Yes | Double | Current bitrate |
| `startupTime` | Yes | Double | Startup time |
| `fps` | Yes | Double | FPS value |
| `droppedFrames` | Yes | Double | Number of dropped frames |

**Example**

```swift
let qoeObject = ACPMedia.createQoEObject(withBitrate: 10000000, startupTime: 2, fps: 23, droppedFrames: 10)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
createQoEObject(Number bitrate, Number startupTime, Number fps, Number droppedFrames);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `bitrate` | Yes | Number | Current bitrate |
| `startupTime` | Yes | Number | Startup time |
| `fps` | Yes | Number | FPS value |
| `droppedFrames` | Yes | Number | Number of dropped frames |

**Example**

```jsx
let qoeObject = ACPMedia.createQoEObject(1000000, 2, 23, 10);
```
{% endtab %}
{% endtabs %}

### createStateObject

Creates an instance of the player state object.

{% tabs %}
{% tab title="Android" %}
Returns a HashMap instance that contains information about the State.

#### Java

**Syntax**

```java
public static HashMap<String, Object> createStateObject(String stateName);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `stateName` | Yes | String | The name of the state. More information, including the supported values, can be found in the [player state constants section](#player-state-constants). | Yes |

**Example**

```java
HashMap<String, Object> playerStateInfo = Media.createStateObject("fullscreen");
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
Returns a map that contains information about the player state.

#### Swift

**Syntax**

```swift
static func createStateObjectWith(stateName: String) -> [String: Any]
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `stateName` | Yes | String | The name of the state. More information, including the supported values, can be found in the [player state constants section](#player-state-constants). | Yes |


**Example**

```swift
let fullScreenState = Media.createStateObjectWith(stateName: "fullscreen")
```

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createStateObjectWithName: (NSString* _Nonnull) stateName;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `stateName` | Yes | String | The name of the state. More information, including the supported values, can be found in the [player state constants section](#player-state-constants). | Yes |

**Example**

```objc
NSDictionary* fullScreenState = [AEPMobileMedia createStateObjectWith:AEPMediaPlayerState.FULLSCREEN]
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
Returns an NSDictionary instance that contains information about the player state.

#### Objective-C

**Syntax**

```objc
+ (NSDictionary* _Nonnull) createStateObjectWithName: (NSString* _Nonnull) stateName;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `stateName` | Yes | String | The name of the state. More information, including the supported values, can be found in the [player state constants section](#player-state-constants). | Yes |

**Example**

```objc
NSDictionary *playerStateObject = [ACPMedia createStateObjectWithName: @"fullscreen"];
```

#### Swift

**Syntax**

```swift
static func createStateObjectWith(stateName: String) -> [String: Any]
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `stateName` | Yes | String | The name of the state. More information, including the supported values, can be found in the [player state constants section](#player-state-constants). | Yes |

**Example**

```swift
let playerStateObject = ACPMedia.createStateObject(withName: "fullscreen")
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### createStateObject

```jsx
let playerStateObject = ACPMedia.createStateObject("fullscreen");
```
{% endtab %}
{% endtabs %}

## Media tracker API reference

### trackSessionStart

Tracks the intention to start playback. This starts a tracking session on the media tracker instance. To learn how to resume a previously closed session, please read the [media resume guide](media-api-reference.md#media-resume)

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void trackSessionStart(Map<String, Object> mediaInfo, Map<String, String> contextData);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `mediaInfo` | Yes | Map<String, Object> | Media information created using the [createMediaObject](#createmediaobject) method. |
| `contextData` | No | Map<String, String> | Optional media context data. For standard metadata keys, use [standard video constants](#standard-video-constants) or [standard audio constants](#standard-audio-constants). |

**Example**

```java
HashMap<String, Object> mediaObject = Media.createMediaObject("media-name", "media-id", 60D, MediaConstants.StreamType.VOD, Media.MediaType.Video);

HashMap<String, String> mediaMetadata = new HashMap<String, String>();
// Standard metadata keys provided by Adobe.
mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, "Sample Episode");
mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, "Sample Show");

// Custom metadata keys
mediaMetadata.put("isUserLoggedIn", "false");
mediaMetadata.put("tvStation", "Sample TV Station");

_tracker.trackSessionStart(mediaInfo, mediaMetadata);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
public func trackSessionStart(info: [String: Any], metadata: [String: String]? = nil)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `info` | Yes | Dictionary<String, Object> | Media information created using the [createMediaObject](#createmediaobject) method. |
| `contextData` | No | Dictionary<String, String> | Optional media context data. For standard metadata keys, use [standard video constants](#standard-video-constants) or [standard audio constants](#standard-audio-constants). |

**Example**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-name", id: "videoId", length: 60, streamType: MediaConstants.StreamType.VOD, mediaType: MediaType.Video)

var videoMetadata: [String: String] = [:]
// Sample implementation for using video standard metadata keys
videoMetadata[MediaConstants.VideoMetadataKeys.SHOW] = "Sample show"
videoMetadata[MediaConstants.VideoMetadataKeys.SEASON] = "Sample season"

// Sample implementation for using custom metadata keys
videoMetadata["isUserLoggedIn"] = "false"
videoMetadata["tvStation"] = "Sample TV station"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

#### Objective-C

**Syntax**

```objc
- (void) trackSessionStart: (NSDictionary* _Nonnull) mediaInfo data: (NSDictionary* _Nullable) contextData;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `info` | Yes | Dictionary<String, Object> | Media information created using the [createMediaObject](#createmediaobject) method. |
| `contextData` | No | Dictionary<String, String> | Optional media context data. For standard metadata keys, use [standard video constants](#standard-video-constants) or [standard audio constants](#standard-audio-constants). |

**Example**

```objc
NSDictionary *mediaObject = [AEPMobileMedia createMediaObjectWith:@"video-name" id:@"video-id" length:60 streamType:AEPMediaStreamType.VOD mediaType:AEPMediaTypeVideo];

NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
// Sample implementation for using standard video metadata keys
[videoMetadata setObject:@"Sample show" forKey:AEPVideoMetadataKeys.SHOW];
[videoMetadata setObject:@"Sample Season" forKey:AEPVideoMetadataKeys.SEASON];

// Sample implementation for using custom metadata keys
[videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
[videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];

[_tracker trackSessionStart:mediaObject metadata:videoMetadata];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### trackSessionStart

**Syntax**

```objc
- (void) trackSessionStart: (NSDictionary* _Nonnull) mediaInfo data: (NSDictionary* _Nullable) contextData;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `info` | Yes | Dictionary<String, Object> | Media information created using the [createMediaObject](#createmediaobject) method. |
| `contextData` | No | Dictionary<String, String> | Optional media context data. For standard metadata keys, use [standard video constants](#standard-video-constants) or [standard audio constants](#standard-audio-constants). |

**Example**

```objc
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName:@"media-name" mediaId:@"media-id" length:60 streamType:ACPMediaStreamTypeVod mediaType:ACPMediaTypeVideo];

NSMutableDictionary *mediaMetadata = [[NSMutableDictionary alloc] init];
// Standard metadata keys provided by adobe.
[mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
[mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];

// Custom metadata keys
[mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
[mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];

[_tracker trackSessionStart:mediaObject data:mediaMetadata];
```

#### Swift

**Syntax**

```swift
public func trackSessionStart(info: [String: Any], metadata: [String: String]? = nil)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `info` | Yes | Dictionary<String, Object> | Media information created using the [createMediaObject](#createmediaobject) method. |
| `contextData` | No | Dictionary<String, String> | Optional media context data. For standard metadata keys, use [standard video constants](#standard-video-constants) or [standard audio constants](#standard-audio-constants). |

**Example**

```swift
let mediaObject = ACPMedia.createMediaObject(withName: "media-name", mediaId: "media-id", length: 60, streamType: ACPMediaStreamTypeVod, mediaType:ACPMediaType.video)

// Standard metadata keys provided by adobe.      
var mediaMetadata = [ACPVideoMetadataKeyShow: "Sample show", ACPVideoMetadataKeySeason: "Sample season"]

// Custom metadata keys      
mediaMetadata["isUserLoggedIn"] = "false"
mediaMetadata["tvStation"] = "Sample TV station"

_tracker.trackSessionStart(mediaObject, data: mediaMetadata)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackSessionStart(Object mediaObject, Object mediaMetadata)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `info` | Yes | Object | Media information created using the [createMediaObject](#createmediaobject) method. |
| `contextData` | No | Object | Optional media context data. For standard metadata keys, use [standard video constants](#standard-video-constants) or [standard audio constants](#standard-audio-constants). |

**Example**

```jsx
let mediaObject = ACPMedia.createMediaObject("media-name", "media-id", 60, ACPMediaConstants.ACPMediaStreamTypeVod, ACPMediaType.Video);
var mediaMetadata = new Object();
mediaMetadata[ACPMediaConstants.ACPVideoMetadataKeyShow] = "Sample Show";
mediaMetadata[ACPMediaConstants.ACPVideoMetadataKeySeason] = "Sample Season";

// Custom metadata keys
mediaMetadata["isUserLoggedIn"] = "false";
mediaMetadata["tvStation"] = "Sample TV station";

tracker.trackSessionStart(mediaObject, mediaMetadata);
```
{% endtab %}
{% endtabs %}

### trackPlay

Tracks the media play, or resume, after a previous pause.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void trackPlay();
```

**Example**

```java
_tracker.trackPlay();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func trackPlay()
```

**Example**

```swift
tracker.trackPlay()
```

#### Objective-C

**Syntax**

```objc
- (void) trackPlay;
```

**Example**

```objc
[_tracker trackPlay];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
- (void) trackPlay;
```

**Example**

```objc
[_tracker trackPlay];
```

#### Swift

**Syntax**

```swift
func trackPlay()
```

**Example**

```swift
_tracker.trackPlay()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackPlay()
```

**Example**

```jsx
tracker.trackPlay();
```
{% endtab %}
{% endtabs %}

### trackPause

Tracks the media pause.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void trackPause();
```

**Example**

```java
_tracker.trackPause();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func trackPause()
```

**Example**

```swift
tracker.trackPause()
```

#### Objective-C

**Syntax**

```objc
- (void) trackPause;
```

**Example**

```objc
[_tracker trackPause];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
- (void) trackPause;
```

**Example**

```objc
[_tracker trackPause];
```

#### Swift

**Syntax**

```swift
func trackPause()
```

**Example**

```swift
_tracker.trackPause()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackPause()
```

**Example**

```jsx
tracker.trackPause();
```
{% endtab %}
{% endtabs %}

### trackComplete

Tracks media complete. Call this method only when the media has been completely viewed.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void trackComplete();
```

**Example**

```java
_tracker.trackComplete();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func trackComplete()
```

**Example**

```swift
tracker.trackComplete()
```

#### Objective-C

**Syntax**

```objc
- (void) trackComplete;
```

**Example**

```objc
[_tracker trackComplete];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
- (void) trackComplete;
```

**Example**

```objc
[_tracker trackComplete];
```

#### Swift

**Swift**

```swift
func trackComplete()
```

**Example**

```swift
_tracker.trackComplete()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackComplete()
```

**Example**

```jsx
tracker.trackComplete();
```
{% endtab %}
{% endtabs %}

### trackSessionEnd

Tracks the end of a viewing session. This method should be called even if the user does not view the media to completion.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void trackSessionEnd();
```

**Example**

```java
_tracker.trackSessionEnd();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func trackSessionEnd()
```

**Example**

```swift
tracker.trackSessionEnd()
```

#### Objective-C

**Syntax**

```objc
- (void) trackSessionEnd;
```

**Example**

```objc
[_tracker trackSessionEnd];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective C

**Syntax**

```objc
- (void) trackSessionEnd;
```

**Example**

```objc
[_tracker trackSessionEnd];
```

#### Swift

**Syntax**

```swift
func trackSessionEnd()
```

**Example**

```swift
_tracker.trackSessionEnd()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackSessionEnd()
```

**Example**

```jsx
tracker.trackSessionEnd();
```
{% endtab %}
{% endtabs %}

### trackError

Tracks an error in media playback.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void trackError(String errorId);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `errorId` | Yes | String | The ID of the error you want to track. |

**Example**

```java
_tracker.trackError("errorId");
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func trackError(errorId: String)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `errorId` | Yes | String | The ID of the error you want to track. |

**Example**

```swift
tracker.trackError(errorId: "errorId")
```

#### Objective-C

**Syntax**

```objc
[_tracker trackError:@"errorId"];
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `errorId` | Yes | String | The ID of the error you want to track. |

**Example**

```objc
[_tracker trackError:@"errorId"];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
- (void) trackError: (NSString* _Nonnull) errorId;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `errorId` | Yes | String | The ID of the error you want to track. |

**Example**

```objc
[_tracker trackError:@"errorId"];
```

#### Swift

**Syntax**

```swift
func trackError(errorId: String)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `errorId` | Yes | String | The ID of the error you want to track. |

**Example**

```swift
_tracker.trackError("errorId")
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackError(String errorId)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `errorId` | Yes | String | The ID of the error you want to track. |

**Example**

```jsx
tracker.trackError("errorId");
```
{% endtab %}
{% endtabs %}

### trackEvent

Tracks a media event.

{% tabs %}
{% tab title="Android" %}
#### trackEvent

**Syntax**

```java
  public void trackEvent(Media.Event event,
                         Map<String, Object> info,
                         Map<String, String> data);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `event` | Yes | [Media event object](#media-events) | The type of the tracking event. |
| `info` | Yes* | Map<String, Object> | You need to include this additional information for the following event types: <ul><li>`AdBreakStart` - For an `AdBreakStart` event, the ad break information is created by using the [createAdBreakObject](#createadbreakobject) method.</li><li>`AdStart` -  For an `AdStart` event, the ad information is created by using the [createAdObject](#createadobject) method.</li><li>`ChapterStart` - For a `ChapterStart` event, the chapter information is created by using the [createChapterObject](#createchapterobject) method.</li><li>`StateStart` and `StateEnd` -  For a `StateStart` or a `StateEnd` event, the state information is created by using the [createStateObject](#createstateobject) method.</li></ul> For all other types of events, this value **must** be `nil`. |
| `data` | Yes* | Map<String, String> | You need to include this information for the following event types: <ul><li>`AdStart`</li><li>`ChapterStart`</li></ul> For all other types of events, this value **must** be `nil`. |

**Examples**

**Tracking player states**

```java
// StateStart
  HashMap<String, Object> stateObject = Media.createStateObject("fullscreen");
  _tracker.trackEvent(Media.Event.StateStart, stateObject, null);

// StateEnd
  HashMap<String, Object> stateObject = Media.createStateObject("fullscreen");
  _tracker.trackEvent(Media.Event.StateEnd, stateObject, null);
```

**Tracking ad breaks**

```java
// AdBreakStart
  HashMap<String, Object> adBreakObject = Media.createAdBreakObject("adbreak-name", 1L, 0D);
  _tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null);

// AdBreakComplete
  _tracker.trackEvent(Media.Event.AdBreakComplete, null, null);
```

**Tracking ads**

```java
// AdStart
  HashMap<String, Object> adObject = Media.createAdObject("ad-name", "ad-id", 1L, 15D);

  HashMap<String, String> adMetadata = new HashMap<String, String>();
  // Standard metadata keys provided by adobe.
  adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, "Sample Advertiser");
  adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign");
  // Custom metadata keys
  adMetadata.put("affiliate", "Sample affiliate");

  _tracker.trackEvent(Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  _tracker.trackEvent(Media.Event.AdComplete, null, null);

// AdSkip
  _tracker.trackEvent(Media.Event.AdSkip, null, null);
```

**Tracking chapters**

```java
// ChapterStart
  HashMap<String, Object> chapterObject = Media.createChapterObject("chapter-name", 1L, 60D, 0D);

  HashMap<String, String> chapterMetadata = new HashMap<String, String>();
  chapterMetadata.put("segmentType", "Sample segment type");

  _tracker.trackEvent(Media.Event.ChapterStart, chapterDataInfo, chapterMetadata);

// ChapterComplete
  _tracker.trackEvent(Media.Event.ChapterComplete, null, null);

// ChapterSkip
  _tracker.trackEvent(Media.Event.ChapterSkip, null, null);
```

**Tracking playback events**

```java
// BufferStart
  _tracker.trackEvent(Media.Event.BufferStart, null, null);

// BufferComplete
  _tracker.trackEvent(Media.Event.BufferComplete, null, null);

// SeekStart
  _tracker.trackEvent(Media.Event.SeekStart, null, null);

// SeekComplete
  _tracker.trackEvent(Media.Event.SeekComplete, null, null);
```

**Tracking bitrate changes**

```java
// If the new bitrate value is available provide it to the tracker.
  HashMap<String, Object> qoeObject = Media.createQoEObject(2000000L, 2D, 25D, 10D);
  _tracker.updateQoEObject(qoeObject);

// Bitrate change
  _tracker.trackEvent(Media.Event.BitrateChange, null, null);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func trackEvent(event: MediaEvent, info: [String: Any]?, metadata: [String: String]?)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `event` | Yes | [Media event object](#media-events) | The type of the tracking event. |
| `info` | Yes, pending event type | [String: Any]? | You need to include this additional information for the following event types: <ul><li>`AdBreakStart` - For an `AdBreakStart` event, the `adBreak` information is created by using the [createAdBreakObject](#createadbreakobject) method.</li><li>`AdStart` -  For an `AdStart` event, the ad information is created by using the [createAdObject](#createadobject) method.</li><li>`ChapterStart` - For a `ChapterStart` event, the chapter information is created by using the [createChapterObject](#createchapterobject) method.</li><li>`StateStart` and `StateEnd` -  For a `StateStart` or a `StateEnd` event, the state information is created by using the [createStateObject](#createstateobject) method.</li></ul> For all other types of events, this value **must** be `nil`. |
| `data` | Yes, pending event type | [String: String]? | You need to include this information for the following event types: <ul><li>`AdStart`</li><li>`ChapterStart`</li></ul> For all other types of events, this value **must** be `nil`. |

**Examples**

**Tracking player states**

```swift
// StateStart
  let fullScreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
  tracker.trackEvent(event: MediaEvent.StateStart, info: fullScreenState, metadata: nil)

// StateEnd
  let fullScreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
  tracker.trackEvent(event: MediaEvent.StateEnd, info: fullScreenState, metadata: nil)
```

**Tracking ad breaks**

```swift
// AdBreakStart
  let adBreakObject = Media.createAdBreakObjectWith(name: "adbreak-name", position: 1, startTime: 0)
  tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)

// AdBreakComplete
  tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Tracking ads**

```swift
// AdStart
  let adObject = Media.createObjectWith(name: "adbreak-name", id: "ad-id", position: 0, length: 30)

// Standard metadata keys provided by adobe.
  var adMetadata: [String: String] = [:]
  adMetadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Sample Advertiser"
  adMetadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign"

// Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate"

  tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: adMetadata)

// AdComplete
  tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)

// AdSkip
   tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Tracking chapters**

```swift
// ChapterStart
  let chapterObject = Media.createChapterObjectWith(name: "chapter_name", position: 1, length: 60, startTime: 0)
  let chapterDictionary = ["segmentType": "Sample segment type"]

  tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: chapterDictionary)

// ChapterComplete
  tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)

// ChapterSkip
  tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Tracking playback events**

```swift
// BufferStart
   tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// BufferComplete
   tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)

// SeekStart
   tracker.trackEvent(event: MediaEvent.SeekStart, info: nil, metadata: nil)

// SeekComplete
   tracker.trackEvent(event: MediaEvent.SeekComplete, info: nil, metadata: nil)
```

**Tracking bitrate change**

```swift
// If the new bitrate value is available provide it to the tracker.
  let qoeObject = Media.createQoEObjectWith(bitrate: 500000, startupTime: 2, fps: 24, droppedFrames: 10)
  tracker.updateQoEObject(qoeObject)

// Bitrate change
  tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

#### Objective-C

**Syntax**

```objc
  - (void) trackEvent: (ACPMediaEvent) event
                 info: (NSDictionary* _Nullable) info
                 data: (NSDictionary* _Nullable) data;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `event` | Yes | [Media event object](#media-events) | The type of the tracking event. |
| `info` | Yes, pending event type | NSDictionary* _Nullable | You need to include this additional information for the following event types: <ul><li>`AdBreakStart` - For an `AdBreakStart` event, the `adBreak` information is created by using the [createAdBreakObject](#createadbreakobject) method.</li><li>`AdStart` -  For an `AdStart` event, the ad information is created by using the [createAdObject](#createadobject) method.</li><li>`ChapterStart` - For a `ChapterStart` event, the chapter information is created by using the [createChapterObject](#createchapterobject) method.</li><li>`StateStart` and `StateEnd` -  For a `StateStart` or a `StateEnd` event, the state information is created by using the [createStateObject](#createstateobject) method.</li></ul> For all other types of events, this value **must** be `nil`. |
| `data` | Yes, pending event type | NSDictionary* _Nullable  | You need to include this information for the following event types: <ul><li>`AdStart`</li><li>`ChapterStart`</li></ul> For all other types of events, this value **must** be `nil`. |

**Examples**

**Tracking player states**

```objc
// StateStart
  NSDictionary* fullScreenState = [AEPMobileMedia createStateObjectWith:AEPMediaPlayerState.FULLSCREEN];
  [_tracker trackEvent:AEPMediaEventStateStart info:fullScreenState metadata:nil];

// StateEnd
  NSDictionary* fullScreenState = [AEPMobileMedia createStateObjectWith:AEPMediaPlayerState.FULLSCREEN];
  [_tracker trackEvent:AEPMediaEventStateEnd info:fullScreenState metadata:nil];
```

**Tracking ad breaks**

```objc
// AdBreakStart
  NSDictionary *adBreakObject = [AEPMobileMedia createAdBreakObjectWith:@"adbreak-name" position:1 startTime:0];
  [_tracker trackEvent:AEPMediaEventAdBreakStart info:adBreakObject metadata:nil];

// AdBreakComplete
  [_tracker trackEvent:AEPMediaEventAdBreakComplete info:nil metadata:nil];
```

**Tracking ads**

```objc
// AdStart
  NSDictionary *adObject = [AEPMobileMedia createAdObjectWith:@"ad-name" id:@"ad-id" position:0 length:30];
  NSMutableDictionary* adMetadata = [[NSMutableDictionary alloc] init];

// Standard metadata keys provided by adobe.
  [adMetadata setObject:@"Sample Advertiser" forKey:AEPAdMetadataKeys.ADVERTISER];
  [adMetadata setObject:@"Sample Campaign" forKey:AEPAdMetadataKeys.CAMPAIGN_ID];

// Custom metadata keys
  [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];

  [_tracker trackEvent:AEPMediaEventAdStart info:adObject metadata:adMetadata];

// AdComplete
  [_tracker trackEvent:AEPMediaEventAdComplete info:nil metadata:nil];

// AdSkip
  [_tracker trackEvent:AEPMediaEventAdSkip info:nil metadata:nil];
```

**Tracking chapters**

```objc
// ChapterStart
  NSDictionary *chapterObject = [AEPMobileMedia createChapterObjectWith:@"chapter_name" position:1 length:60 startTime:0];

  NSMutableDictionary *chapterMetadata = [[NSMutableDictionary alloc] init];
  [chapterMetadata setObject:@"Sample segment type" forKey:@"segmentType"];

  [_tracker trackEvent:AEPMediaEventChapterStart info:chapterObject metadata:chapterMetadata];

// ChapterComplete
  [_tracker trackEvent:AEPMediaEventChapterComplete info:nil metadata:nil];

// ChapterSkip
  [_tracker trackEvent:AEPMediaEventChapterSkip info:nil metadata:nil];
```

**Tracking playback events**

```objc
// BufferStart
  [_tracker trackEvent:AEPMediaEventBufferStart info:nil metadata:nil];

// BufferComplete
  [_tracker trackEvent:AEPMediaEventBufferComplete info:nil metadata:nil];

// SeekStart
  [_tracker trackEvent:AEPMediaEventSeekStart info:nil metadata:nil];

// SeekComplete
  [_tracker trackEvent:AEPMediaEventSeekComplete info:nil metadata:nil];
```

**Tracking bitrate change**

```objc
// If the new bitrate value is available provide it to the tracker.
  NSDictionary *qoeObject = [AEPMobileMedia createQoEObjectWith:50000 startTime:2 fps:24 droppedFrames:10];

// Bitrate change
  [_tracker trackEvent:AEPMediaEventBitrateChange info:nil metadata:nil];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
  - (void) trackEvent: (ACPMediaEvent) event
                 info: (NSDictionary* _Nullable) info
                 data: (NSDictionary* _Nullable) data;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `event` | Yes | [Media event object](#media-events) | The type of the tracking event. |
| `info` | Yes, pending event type | NSDictionary* _Nullable | You need to include this additional information for the following event types: <ul><li>`AdBreakStart` - For an `AdBreakStart` event, the `adBreak` information is created by using the [createAdBreakObject](#createadbreakobject) method.</li><li>`AdStart` -  For an `AdStart` event, the ad information is created by using the [createAdObject](#createadobject) method.</li><li>`ChapterStart` - For a `ChapterStart` event, the chapter information is created by using the [createChapterObject](#createchapterobject) method.</li><li>`StateStart` and `StateEnd` -  For a `StateStart` or a `StateEnd` event, the state information is created by using the [createStateObject](#createstateobject) method.</li></ul> For all other types of events, this value **must** be `nil`. |
| `data` | Yes, pending event type | NSDictionary* _Nullable  | You need to include this information for the following event types: <ul><li>`AdStart`</li><li>`ChapterStart`</li></ul> For all other types of events, this value **must** be `nil`. |

**Examples**

**Tracking player states**

```objc
// StateStart
  NSDictionary* stateObject = [ACPMedia createStateObjectWithName:@"fullscreen"];
  [_tracker trackEvent:ACPMediaEventStateStart mediaObject:stateObject data:nil];

// StateEnd
  NSDictionary* stateObject = [ACPMedia createStateObjectWithName:@"fullscreen"];
  [_tracker trackEvent:ACPMediaEventStateEnd mediaObject:stateObject data:nil];
```

**Tracking ad breaks**

```objc
// AdBreakStart
  NSDictionary* adBreakObject = [ACPMedia createAdBreakObjectWithName:@"adbreak-name" position:1 startTime:0];
  [_tracker trackEvent:ACPMediaEventAdBreakStart mediaObject:adBreakObject data:nil];

// AdBreakComplete
  [_tracker trackEvent:ACPMediaEventAdBreakComplete mediaObject:nil data:nil];
```

**Tracking ads**

```objc
// AdStart
  NSDictionary* adObject = [ACPMedia createAdObjectWithName:@"ad-name" adId:@"ad-id" position:1 length:15];
  NSMutableDictionary* adMetadata = [[NSMutableDictionary alloc] init];

  // Standard metadata keys provided by adobe.
  [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
  [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
  // Custom metadata keys
  [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];

  [_tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];

// AdComplete
  [_tracker trackEvent:ACPMediaEventAdComplete mediaObject:nil data:nil];

// AdSkip
  [_tracker trackEvent:ACPMediaEventAdSkip mediaObject:nil data:nil];
```

**Tracking chapters**

```objc
// ChapterStart
  NSDictionary* chapterObject = [ACPMedia createChapterObjectWithName:@"chapter-name" position:1 length:30 startTime:0];

  NSMutableDictionary *chapterMetadata = [[NSMutableDictionary alloc] init];
  [chapterMetadata setObject:@"Sample segment type" forKey:@"segmentType"];

  [_tracker trackEvent:ACPMediaEventChapterStart mediaObject:chapterObject data:chapterMetadata];

// ChapterComplete
  [_tracker trackEvent:ACPMediaEventChapterComplete mediaObject:nil    data:nil];

// ChapterSkip
  [_tracker trackEvent:ACPMediaEventChapterSkip mediaObject:nil    data:nil];
```

**Tracking playback events**

```objc
// BufferStart
  [_tracker trackEvent:ACPMediaEventBufferStart info:nil data:nil];

// BufferComplete
  [_tracker trackEvent:ACPMediaEventBufferComplete info:nil data:nil];

// SeekStart
  [_tracker trackEvent:ACPMediaEventSeekStart info:nil data:nil];

// SeekComplete
  [_tracker trackEvent:ACPMediaEventSeekComplete info:nil data:nil];
```

**Tracking bitrate change**

```objc
// If the new bitrate value is available provide it to the tracker.
  NSDictionary* qoeObject = [ACPMedia createQoEObjectWithBitrate:2000000 startupTime:2 fps:25 droppedFrames:10];
  [_tracker updateQoEObject:qoeObject];

// Bitrate change
  [_tracker trackEvent:ACPMediaEventBitrateChange info:nil data:nil];
```

#### Swift

**Syntax**

```swift
func trackEvent(event: MediaEvent, info: [String: Any]?, metadata: [String: String]?)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `event` | Yes | [Media event object](#media-events) | The type of the tracking event. |
| `info` | Yes, pending event type | [String: Any]? | You need to include this additional information for the following event types: <ul><li>`AdBreakStart` - For an `AdBreakStart` event, the `adBreak` information is created by using the [createAdBreakObject](#createadbreakobject) method.</li><li>`AdStart` -  For an `AdStart` event, the ad information is created by using the [createAdObject](#createadobject) method.</li><li>`ChapterStart` - For a `ChapterStart` event, the chapter information is created by using the [createChapterObject](#createchapterobject) method.</li><li>`StateStart` and `StateEnd` -  For a `StateStart` or a `StateEnd` event, the state information is created by using the [createStateObject](#createstateobject) method.</li></ul> For all other types of events, this value **must** be `nil`. |
| `metadata` | Yes, pending event type | [String: String]? | You need to include this information for the following event types: <ul><li>`AdStart`</li><li>`ChapterStart`</li></ul> For all other types of events, this value **must** be `nil`. |

**Examples**

**Tracking player states**

```swift
// StateStart
  let stateObject = ACPMedia.createStateObject(withName: "fullscreen")
  _tracker.trackEvent(ACPMediaEvent.stateStart, mediaObject: stateObject, data: nil)

// StateEnd
  let stateObject = ACPMedia.createStateObject(withName: "fullscreen")
  _tracker.trackEvent(ACPMediaEvent.stateEnd, mediaObject: stateObject, data: nil)
```

**Tracking ad breaks**

```swift
// AdBreakStart
  let adBreakObject = ACPMedia.createAdBreakObject(withName: "adbreak-name", position: 1, startTime: 0)
  _tracker.trackEvent(ACPMediaEvent.adBreakStart, mediaObject: adBreakObject, data: nil)

// AdBreakComplete
  _tracker.trackEvent(ACPMediaEvent.adBreakComplete, mediaObject: nil, data: nil)
```

**Tracking ads**

```swift
// AdStart
  let adObject = ACPMedia.createAdObject(withName: "ad-name", adId: "ad-id", position: 1, length: 15)

  // Standard metadata keys provided by adobe.
  var adMetadata = [ACPAdMetadataKeyAdvertiser: "Sample Advertiser", ACPAdMetadataKeyCampaignId: "Sample Campaign"]
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate"

  _tracker.trackEvent(ACPMediaEvent.adStart, mediaObject: adObject, data: adMetadata)

// AdComplete
  _tracker.trackEvent(ACPMediaEvent.adComplete, mediaObject: nil, data: nil)

// AdSkip
  _tracker.trackEvent(ACPMediaEvent.adSkip, mediaObject: nil, data: nil)
```

**Tracking chapters**

```swift
// ChapterStart
  let chapterObject = ACPMedia.createChapterObject(withName: "chapter-name", position: 1, length: 60, startTime: 0)
  let chapterMetadata = ["Sample segment type": "segmentType"];

  _tracker.trackEvent(ACPMediaEvent.chapterStart, mediaObject: chapterObject, data: chapterMetadata)

// ChapterComplete
  _tracker.trackEvent(ACPMediaEvent.chapterComplete, mediaObject: nil, data: nil)

// ChapterSkip
  _tracker.trackEvent(ACPMediaEvent.chapterSkip, mediaObject: nil, data: nil)
```

**Tracking playback events**

```swift
// BufferStart
  _tracker.trackEvent(ACPMediaEvent.bufferStart, mediaObject: nil, data: nil)

// BufferComplete
  _tracker.trackEvent(ACPMediaEvent.bufferComplete, mediaObject: nil, data: nil)

// SeekStart
  _tracker.trackEvent(ACPMediaEvent.seekStart, mediaObject: nil, data: nil)

// SeekComplete
  _tracker.trackEvent(ACPMediaEvent.seekComplete, mediaObject: nil, data: nil)
```

**Tracking bitrate change**

```swift
// If the new bitrate value is available provide it to the tracker.
  let qoeObject = ACPMedia.createQoEObject(withBitrate: 2000000, startupTime: 2, fps: 25, droppedFrames: 10)
  _tracker.updateQoEObject(qoeObject)

// Bitrate change
  _tracker.trackEvent(ACPMediaEvent.bitrateChange, mediaObject: nil, data: nil)
```

{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function trackEvent(String event, Object info, Object data)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `event` | Yes | [Media event object](#media-events) | The type of the tracking event. |
| `info` | Yes, pending event type | Object | You need to include this additional information for the following event types: <ul><li>`AdBreakStart` - For an `AdBreakStart` event, the `adBreak` information is created by using the [createAdBreakObject](#createadbreakobject) method.</li><li>`AdStart` -  For an `AdStart` event, the ad information is created by using the [createAdObject](#createadobject) method.</li><li>`ChapterStart` - For a `ChapterStart` event, the chapter information is created by using the [createChapterObject](#createchapterobject) method.</li><li>`StateStart` and `StateEnd` -  For a `StateStart` or a `StateEnd` event, the state information is created by using the [createStateObject](#createstateobject) method.</li></ul> For all other types of events, this value **must** be `nil`. |
| `data` | Yes, pending event type | Object | You need to include this information for the following event types: <ul><li>`AdStart`</li><li>`ChapterStart` - For a `ChapterStart` event, the </li></ul> all other types of events, this value **must** be `nil`. |

**Examples**

**Tracking player states**

```jsx
// StateStart
  let stateObject = ACPMedia.createStateObject("fullscreen");
  tracker.trackEvent(ACPMediaEvent.EventStateStart, stateObject, null);

// StateEnd
  let stateObject = ACPMedia.createStateObject("fullscreen");
  tracker.trackEvent(ACPMediaEvent.EventStateEnd, stateObject, null);
```

**Tracking ad breaks**

```jsx
// AdBreakStart
  let adBreakObject = ACPMedia.createAdBreakObject("adbreak-name", 1, 0);
  tracker.trackEvent(ACPMediaEvent.EventAdBreakStart, adBreakObject, null);

// AdBreakComplete
  tracker.trackEvent(ACPMediaEvent.EventAdBreakComplete, null, null);
```

**Tracking ads**

```jsx
// AdStart
  let adObject = ACPMedia.createAdObject("ad-name", "ad-id", 1, 15);
  var adMetadata = new Object();
  adMetadata[ACPMediaConstants.ACPAdMetadataKeyAdvertiser] = "Sample Advertiser";
  adMetadata[ACPMediaConstants.ACPAdMetadataKeyCampaignId] = "Sample Campaign";

  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ACPMediaEvent.EventAdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ACPMediaEvent.EventAdComplete, null, null);

// AdSkip
  tracker.trackEvent(ACPMediaEvent.EventAdSkip, null, null);
```

**Tracking chapters**

```jsx
// ChapterStart
  let chapterObject = ACPMedia.createChapterObject("chapter-name", 1, 60, 0);
  var chapterMetadata = new Object();
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ACPMediaEvent.EventChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ACPMediaEvent.EventChapterComplete, null, null);

// ChapterSkip
  tracker.trackEvent(ACPMediaEvent.EventChapterSkip, null, null);
```

**Tracking playback events**

```jsx
// BufferStart
  tracker.trackEvent(ACPMediaEvent.EventBufferStart, null, null);

// BufferComplete
  tracker.trackEvent(ACPMediaEvent.EventBufferComplete, null, null);

// SeekStart
  tracker.trackEvent(ACPMediaEvent.EventSeekStart, null, null);

// SeekComplete
  tracker.trackEvent(ACPMediaEvent.EventSeekComplete, null, null);
```

**Tracking bitrate changes**

```jsx
// If the new bitrate value is available provide it to the tracker.
  let qoeObject = ACPMedia.createQoEObject(2000000, 2, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ACPMediaEvent.EventBitrateChange, null, null);
```
{% endtab %}
{% endtabs %}

### updateCurrentPlayhead

Provides a media tracker with the current media playhead. For accurate tracking, call this method multiple times when the playhead changes.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void updateCurrentPlayhead(double time);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `time` | Yes | Double | Current playhead in seconds. For video-on-demand (VOD), the value is specified in seconds from the beginning of the media item. For live streaming, the value is specified as the number of seconds since midnight UTC on that day. |

**Examples**

**Video-on-demand**

```java
_tracker.updateCurrentPlayhead(1);
```

**Live streaming**

```java
double timeFromMidnightInSecond = (System.currentTimeMillis()/1000) % 86400;

_tracker.updateCurrentPlayhead(timeFromMidnightInSecond);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func updateCurrentPlayhead(time: Double)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `time` | Yes | Double | Current playhead in seconds. For video-on-demand (VOD), the value is specified in seconds from the beginning of the media item. For live streaming, the value is specified as the number of seconds since midnight UTC on that day. |

**Examples**

**Video-on-demand**

```swift
tracker.updateCurrentPlayhead(1);
```

**Live streaming**

```swift
let secondsSince1970: TimeInterval = (Date().timeIntervalSince1970)
let timeFromMidnightInSecond = secondsSince1970.truncatingRemainder(dividingBy: 86400)

tracker.updateCurrentPlayhead(time: timeFromMidnightInSecond)
```

#### Objective-C

**Syntax**

```objc
- (void) updateCurrentPlayhead: (double) time;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `time` | Yes | Double | Current playhead in seconds. For video-on-demand (VOD), the value is specified in seconds from the beginning of the media item. For live streaming, the value is specified as the number of seconds since midnight UTC on that day. |

**Examples**

**Video-on-demand**

```objc
[_tracker updateCurrentPlayhead:1];
```

**Live streaming**

```objc
double secondsSince1970 = [[NSDate date] timeIntervalSince1970];
double timeFromMidnightInSecond = fmod(secondsSince1970 , 86400);

[_tracker updateCurrentPlayhead: timeFromMidnightInSecond];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
- (void) updateCurrentPlayhead: (double) time;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `time` | Yes | Double | Current playhead in seconds. For video-on-demand (VOD), the value is specified in seconds from the beginning of the media item. For live streaming, the value is specified as the number of seconds since midnight UTC on that day. |

**Examples**

**Video-on-demand**

```objc
[_tracker updateCurrentPlayhead:1];
```

**Live streaming**

```objc
double secondsSince1970 = [[NSDate date] timeIntervalSince1970];
double timeFromMidnightInSecond = fmod(secondsSince1970 , 86400);

[_tracker updateCurrentPlayhead: timeFromMidnightInSecond];
```

#### Swift

**Syntax**

```swift
func updateCurrentPlayhead(time: Double)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `time` | Yes | Double | Current playhead in seconds. For video-on-demand (VOD), the value is specified in seconds from the beginning of the media item. For live streaming, the value is specified as the number of seconds since midnight UTC on that day. |

**Examples**

**Video-on-demand**

```swift
_tracker.updateCurrentPlayhead(1)
```

**Live streaming**

```swift
let secondsSince1970: TimeInterval = (Date().timeIntervalSince1970)
let timeFromMidnightInSecond = secondsSince1970.truncatingRemainder(dividingBy: 86400)

tracker.updateCurrentPlayhead(time: timeFromMidnightInSecond)
```

{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function updateCurrentPlayhead(Number time)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `time` | Yes | Number | Current playhead in seconds. For video-on-demand (VOD), the value is specified in seconds from the beginning of the media item. For live streaming, the value is specified as the number of seconds since midnight UTC on that day. |

**Examples**

**Video-on-demand**

```jsx
tracker.updateCurrentPlayhead(1);
```

**Live streaming**

```js
let timeFromMidnightInSeconds = (Date.now() / 1000) % 86400;
tracker.updateCurrentPlayhead(timeFromMidnightInSeconds);
```
{% endtab %}
{% endtabs %}

### updateQoEObject

Provides the media tracker with the current quality of experience (QoE) information. For accurate tracking, call this method multiple times when the media player provides the updated QoE information.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public void updateQoEObject(Map<String, Object> qoeObject);
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `qoeObject` | Yes | Map<String, Object> | Current QoE information that was created by using the [createQoEObject](#createqoeobject) method. |

**Example**

```java
HashMap<String, Object> qoeObject = Media.createQoEObject(1000000L, 2D, 25D, 10D);
_tracker.updateQoEObject(qoeObject);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
func updateQoEObject(qoe: [String: Any])
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `qoeObject` | Yes | [String: Any] | Current QoE information that was created by using the [createQoEObject](#createqoeobject) method. |

**Example**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 500000, startupTime: 2, fps: 24, droppedFrames: 10)
tracker.updateQoEObject(qoe: qoeObject)
```

#### Objective-C

**Syntax**

```objc
- (void) updateQoEObject: (NSDictionary* _Nonnull) qoeObject;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `qoeObject` | Yes | NSDictionary* _Nonnull | Current QoE information that was created by using the [createQoEObject](#createqoeobject) method. |

**Example**

```objc
NSDictionary *qoeObject = [AEPMobileMedia createQoEObjectWith:50000 startTime:2 fps:24 droppedFrames:10]
[_tracker updateQoEObject:qoeObject];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

**Syntax**

```objc
- (void) updateQoEObject: (NSDictionary* _Nonnull) qoeObject;
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `qoeObject` | Yes | NSDictionary* _Nonnull | Current QoE information that was created by using the [createQoEObject](#createqoeobject) method. |

**Example**

```objc
NSDictionary* qoeObject = [ACPMedia createQoEObjectWithBitrate:1000000 startupTime:2 fps:25 droppedFrames:10];
[_tracker updateQoEObject:qoeObject];
```

#### Swift

**Syntax**

```swift
func updateQoEObject(qoe: [String: Any])
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `qoeObject` | Yes | [String: Any] | Current QoE information that was created by using the [createQoEObject](#createqoeobject) method. |

**Example**

```swift
let qoeObject = ACPMedia.createQoEObject(withBitrate: 1000000, startupTime: 2, fps: 25, droppedFrames: 10)
_tracker.updateQoEObject(qoeObject)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```js
function updateQoEObject(Object qoeObject)
```

| **Variable** | **Required** | **Type** | **Description** |
| :----------- | :----------- | :------- | :-------------- |
| `qoeObject` | Yes | Object | Current QoE information that was created by using the [createQoEObject](#createqoeobject) method. |

**Example**

```jsx
let qoeObject = ACPMedia.createQoEObject(1000000, 2, 25, 10);
tracker.updateQoEObject(qoeObject);
```
{% endtab %}
{% endtabs %}

## Media constants

### Media type

Defines the type of a media that is currently tracked.

{% tabs %}
{% tab title="Android" %}
```java
public class Media {

  public enum MediaType {
      /**
      * Constant defining media type for Video streams
      */
      Video,

      /**
      * Constant defining media type for Audio streams
      */
      Audio
  }

}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
```swift
@objc(AEPMediaType)
public enum MediaType: Int, RawRepresentable {
 //Constant defining media type for Video streams
 case Audio
 //Constant defining media type for Audio streams
 case Video
}
```

**Example**

**Swift**

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-name", id: "videoId", length: "60", streamType: MediaConstants.StreamType.VOD, mediaType: MediaType.Video)
```

**Objective-C**

```objc
NSDictionary *mediaObject = [AEPMobileMedia createMediaObjectWith:@"video-name" id:@"video-id" length:60 streamType:AEPMediaStreamType.VOD mediaType:AEPMediaTypeVideo];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
typedef NS_ENUM(NSInteger, ACPMediaType) {
    /**
    * Constant defining media type for Video streams
    */
    ACPMediaTypeVideo,

    /**
    * Constant defining media type for Audio streams
    */
    ACPMediaTypeAudio
};
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaType} from '@adobe/react-native-acpmedia';

ACPMediaType.Video
ACPMediaType.Audio
```
{% endtab %}
{% endtabs %}

### Stream type

Defines the stream type of the content that is currently tracked.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class StreamType {
      /**
      * Constant defining stream type for VOD streams
      */
      public static final String VOD = "vod";

      /**
      * Constant defining stream type for Live streams
      */
      public static final String LIVE = "live";

      /**
      * Constant defining stream type for Linear streams
      */
      public static final String LINEAR = "linear";

      /**
      * Constant defining stream type for Podcast streams
      */
      public static final String PODCAST = "podcast";

      /**
      * Constant defining stream type for Audiobook streams
      */
      public static final String AUDIOBOOK = "audiobook";

      /**
      * Constant defining stream type for AOD streams
      */
      public static final String AOD = "aod";
  }

}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
```swift
public class MediaConstants: NSObject {
  @objc(AEPMediaStreamType)
  public class StreamType: NSObject {
     // Constant defining stream type for VOD streams.
        public static let VOD = "vod"
     // Constant defining stream type for Live streams.
        public static let LIVE = "live"
     // Constant defining stream type for Linear streams.
        public static let LINEAR = "linear"
     // Constant defining stream type for Podcast streams.
        public static let PODCAST = "podcast"
     // Constant defining stream type for Audiobook streams.
        public static let AUDIOBOOK = "audiobook"
     // Constant defining stream type for AOD streams.
        public static let AOD = "aod"
    }
}
```

**Example**

**Swift**

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-name", id: "videoId", length: "60", streamType: MediaConstants.StreamType.VOD, mediaType: MediaType.Video)
```

**Objective-C**

```objc
NSDictionary *mediaObject = [AEPMobileMedia createMediaObjectWith:@"video-name" id:@"video-id" length:60 streamType:AEPMediaStreamType.VOD mediaType:AEPMediaTypeVideo];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
/**
 * Constant defining stream type for VOD streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeVod;

/**
 * Constant defining stream type for Live streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeLive;

/**
 * Constant defining stream type for Linear streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeLinear;

/**
 * Constant defining stream type for Podcast streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypePodcast;

/**
 * Constant defining stream type for Audiobook streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeAudiobook;

/**
 * Constant defining stream type for AOD streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeAod;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPMediaStreamTypeVod
ACPMediaConstants.ACPMediaStreamTypeLive
ACPMediaConstants.ACPMediaConstantsACPMediaStreamTypeLinear
ACPMediaConstants.ACPMediaStreamTypePodcast
ACPMediaConstants.ACPMediaStreamTypeAudiobook
ACPMediaConstants.ACPMediaStreamTypeAod
```
{% endtab %}
{% endtabs %}

### Standard video constants

Defines the standard metadata keys for video streams.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class VideoMetadataKeys {
      public static final String SHOW = "a.media.show";
      public static final String SEASON = "a.media.season";
      public static final String EPISODE = "a.media.episode";
      public static final String ASSET_ID = "a.media.asset";
      public static final String GENRE = "a.media.genre";
      public static final String FIRST_AIR_DATE = "a.media.airDate";
      public static final String FIRST_DIGITAL_DATE = "a.media.digitalDate";
      public static final String RATING = "a.media.rating";
      public static final String ORIGINATOR = "a.media.originator";
      public static final String NETWORK = "a.media.network";
      public static final String SHOW_TYPE = "a.media.type";
      public static final String AD_LOAD = "a.media.adLoad";
      public static final String MVPD = "a.media.pass.mvpd";
      public static final String AUTHORIZED = "a.media.pass.auth";
      public static final String DAY_PART = "a.media.dayPart";
      public static final String FEED = "a.media.feed";
      public static final String STREAM_FORMAT = "a.media.format";
  }

}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
```swift
public class MediaConstants: NSObject {
  @objc(AEPVideoMetadataKeys)
  public class VideoMetadataKeys: NSObject {
        public static let SHOW = "a.media.show"
        public static let SEASON = "a.media.season"
        public static let EPISODE = "a.media.episode"
        public static let ASSET_ID = "a.media.asset"
        public static let GENRE = "a.media.genre"
        public static let FIRST_AIR_DATE = "a.media.airDate"
        public static let FIRST_DIGITAL_DATE = "a.media.digitalDate"
        public static let RATING = "a.media.rating"
        public static let ORIGINATOR = "a.media.originator"
        public static let NETWORK = "a.media.network"
        public static let SHOW_TYPE = "a.media.type"
        public static let AD_LOAD = "a.media.adLoad"
        public static let MVPD = "a.media.pass.mvpd"
        public static let AUTHORIZED = "a.media.pass.auth"
        public static let DAY_PART = "a.media.dayPart"
        public static let FEED = "a.media.feed"
        public static let STREAM_FORMAT = "a.media.format"
    }
}
```

**Example**

**Swift**

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-name", id: "videoId", length: "60", streamType: MediaConstants.StreamType.VOD, mediaType: MediaType.Video)

var videoMetadata: [String: String] = [:]
// Standard Video Metadata
videoMetadata[MediaConstants.VideoMetadataKeys.SHOW] = "Sample show"
videoMetadata[MediaConstants.VideoMetadataKeys.SEASON] = "Sample season"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

**Objective-C**

```objc
NSDictionary *mediaObject = [AEPMobileMedia createMediaObjectWith:@"video-name" id:@"video-id" length:60 streamType:AEPMediaStreamType.VOD mediaType:AEPMediaTypeVideo];

NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
// Standard Video Metadata
[videoMetadata setObject:@"Sample show" forKey:AEPVideoMetadataKeys.SHOW];
[videoMetadata setObject:@"Sample Season" forKey:AEPVideoMetadataKeys.SEASON];

[_tracker trackSessionStart:mediaObject metadata:videoMetadata];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyShow;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeySeason;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyEpisode;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyAssetId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyGenre;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyFirstAirDate;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyFirstDigitalDate;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyRating;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyOriginator;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyNetwork;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyShowType;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyAdLoad;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyMvpd;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyAuthorized;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyDayPart;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyFeed;
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyStreamFormat;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPVideoMetadataKeyShow
ACPMediaConstants.ACPVideoMetadataKeySeason
ACPMediaConstants.ACPVideoMetadataKeyEpisode
ACPMediaConstants.ACPVideoMetadataKeyAssetId
ACPMediaConstants.ACPVideoMetadataKeyGenre
ACPMediaConstants.ACPVideoMetadataKeyFirstAirDate
ACPMediaConstants.ACPVideoMetadataKeyFirstDigitalDate
ACPMediaConstants.ACPVideoMetadataKeyRating
ACPMediaConstants.ACPVideoMetadataKeyOriginator
ACPMediaConstants.ACPVideoMetadataKeyNetwork
ACPMediaConstants.ACPVideoMetadataKeyShowType
ACPMediaConstants.ACPVideoMetadataKeyAdLoad
ACPMediaConstants.ACPVideoMetadataKeyMvpd
ACPMediaConstants.ACPVideoMetadataKeyAuthorized
ACPMediaConstants.ACPVideoMetadataKeyDayPart
ACPMediaConstants.ACPVideoMetadataKeyFeed
ACPMediaConstants.ACPVideoMetadataKeyStreamFormat
```
{% endtab %}
{% endtabs %}

### Standard audio constants

Defines the standard metadata keys for audio streams.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class AudioMetadataKeys {
    public static final String ARTIST = "a.media.artist";
    public static final String ALBUM = "a.media.album";
    public static final String LABEL = "a.media.label";
    public static final String AUTHOR = "a.media.author";
    public static final String STATION = "a.media.station";
    public static final String PUBLISHER = "a.media.publisher";
  }

}
```
{% endtab %}

{% tab title="iOS —  Swift" %}
```objc
public class MediaConstants: NSObject {
  @objc(AEPAudioMetadataKeys)
  public class AudioMetadataKeys: NSObject {
        public static let ARTIST = "a.media.artist"
        public static let ALBUM = "a.media.album"
        public static let LABEL = "a.media.label"
        public static let AUTHOR = "a.media.author"
        public static let STATION = "a.media.station"
        public static let PUBLISHER = "a.media.publisher"
    }
}
```

**Example**

**Swift**

```swift
var audioObject = Media.createMediaObjectWith(name: "audio-name", id: "audioId", length: 30, streamType: MediaConstants.StreamType.AOD, mediaType: MediaType.AUDIO)

var audioMetadata: [String: String] = [:]
// Standard Audio Metadata
audioMetadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Sample artist"
audioMetadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Sample album"

tracker.trackSessionStart(info: audioObject, metadata: audioMetadata)
```

**Objective-C**

```objc
NSDictionary *audioObject = [AEPMobileMedia createMediaObjectWith:@"audio-name" id:@"audioid" length:30 streamType:AEPMediaStreamType.AOD mediaType:AEPMediaTypeAudio];

NSMutableDictionary *audioMetadata = [[NSMutableDictionary alloc] init];
// Standard Audio Metadata
[audioMetadata setObject:@"Sample artist" forKey:AEPAudioMetadataKeys.ARTIST];
[audioMetadata setObject:@"Sample album" forKey:AEPAudioMetadataKeys.ALBUM];

[_tracker trackSessionStart:audioObject metadata:audioMetadata];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyArtist;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAlbum;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyLabel;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAuthor;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyStation;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyPublisher;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPAudioMetadataKeyArtist
ACPMediaConstants.ACPAudioMetadataKeyAlbum
ACPMediaConstants.ACPAudioMetadataKeyLabel
ACPMediaConstants.ACPAudioMetadataKeyAuthor
ACPMediaConstants.ACPAudioMetadataKeyStation
ACPMediaConstants.ACPAudioMetadataKeyPublisher
```
{% endtab %}
{% endtabs %}

### Standard ad constants

Defines the standard metadata keys for ads.

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class AdMetadataKeys {
    public static final String ADVERTISER = "a.media.ad.advertiser";
    public static final String CAMPAIGN_ID = "a.media.ad.campaign";
    public static final String CREATIVE_ID = "a.media.ad.creative";
    public static final String PLACEMENT_ID = "a.media.ad.placement";
    public static final String SITE_ID = "a.media.ad.site";
    public static final String CREATIVE_URL = "a.media.ad.creativeURL";
  }

}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
```objc
public class MediaConstants: NSObject {
  @objc(AEPAdMetadataKeys)
  public class AdMetadataKeys: NSObject {
        public static let ADVERTISER = "a.media.ad.advertiser"
        public static let CAMPAIGN_ID = "a.media.ad.campaign"
        public static let CREATIVE_ID = "a.media.ad.creative"
        public static let PLACEMENT_ID = "a.media.ad.placement"
        public static let SITE_ID = "a.media.ad.site"
        public static let CREATIVE_URL = "a.media.ad.creativeURL"
    }
}
```

**Example**

**Swift**

```swift
let adObject = Media.createObjectWith(name: "adbreak-name", id: "ad-id", position: 0, length: 30)
var adMetadata: [String: String] = [:]
// Standard Ad Metadata
adMetadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Sample Advertiser"
adMetadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: adMetadata)
```

**Objective-C**

```objc
NSDictionary *adObject = [AEPMobileMedia createAdObjectWith:@"ad-name" id:@"ad-id" position:0 length:30];

NSMutableDictionary *adMetadata = [[NSMutableDictionary alloc] init];
// Standard Ad Metadata
[adMetadata setObject:@"Sample Advertiser" forKey:AEPAdMetadataKeys.ADVERTISER];
[adMetadata setObject:@"Sample Campaign" forKey:AEPAdMetadataKeys.CAMPAIGN_ID];

[_tracker trackEvent:AEPMediaEventAdStart info:adObject metadata:adMetadata];
}
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyAdvertiser;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCampaignId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyPlacementId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeySiteId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeUrl;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPAdMetadataKeyAdvertiser
ACPMediaConstants.ACPAdMetadataKeyCampaignId
ACPMediaConstants.ACPAdMetadataKeyCreativeId
ACPMediaConstants.ACPAdMetadataKeyPlacementId
ACPMediaConstants.ACPAdMetadataKeySiteId
ACPMediaConstants.ACPAdMetadataKeyCreativeUrl
```
{% endtab %}
{% endtabs %}

### Player state constants

The following section defines some common player state constants:

{% tabs %}
{% tab title="Android" %}
```java
public class MediaConstants {

  public static final class PlayerState {
    public static final String FULLSCREEN = "fullscreen";
    public static final String PICTURE_IN_PICTURE = "pictureInPicture";
    public static final String CLOSED_CAPTION = "closedCaptioning";
    public static final String IN_FOCUS = "inFocus";
    public static final String MUTE = "mute";
  }

}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
```swift
public class MediaConstants: NSObject {
  @objc(AEPMediaPlayerState)
  public class PlayerState: NSObject {
        public static let FULLSCREEN = "fullscreen"
        public static let PICTURE_IN_PICTURE = "pictureInPicture"
        public static let CLOSED_CAPTION = "closedCaptioning"
        public static let IN_FOCUS = "inFocus"
        public static let MUTE = "mute"
    }
}
```

**Example**

**Swift**

```swift
let inFocusState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)
tracker.trackEvent(event: MediaEvent.StateStart, info: inFocusState, metadata: nil)
```

**Objective-C**

```objc
NSDictionary* inFocusState = [AEPMobileMedia createStateObjectWith:AEPMediaPlayerState.IN_FOCUS];
[_tracker trackEvent:AEPMediaEventStateStart info:muteState metadata:nil];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateFullScreen;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStatePictureInPicture;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateClosedCaption;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateInFocus;
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateMute;
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaConstants} from '@adobe/react-native-acpmedia';

ACPMediaConstants.ACPMediaPlayerStateFullScreen
ACPMediaConstants.ACPMediaPlayerStatePictureInPicture
ACPMediaConstants.ACPMediaPlayerStateClosedCaption
ACPMediaConstants.ACPMediaPlayerStateInFocus
ACPMediaConstants.ACPMediaPlayerStateMute
```
{% endtab %}
{% endtabs %}

### Media events

Defines the type of a tracking event.

{% tabs %}
{% tab title="Android" %}
```java
public class Media {

    /**
    * These enumeration values define the type of a tracking event
    */
    public enum Event {
      /**
      * Constant defining event type for AdBreak start
      */
      AdBreakStart,

      /**
      * Constant defining event type for AdBreak complete
      */
      AdBreakComplete,

      /**
      * Constant defining event type for Ad start
      */
      AdStart,

      /**
      * Constant defining event type for Ad complete
      */
      AdComplete,

      /**
      * Constant defining event type for Ad skip
      */
      AdSkip,

      /**
      * Constant defining event type for Chapter start
      */
      ChapterStart,

      /**
      * Constant defining event type for Chapter complete
      */
      ChapterComplete,

      /**
      * Constant defining event type for Chapter skip
      */
      ChapterSkip,

      /**
      * Constant defining event type for Seek start
      */
      SeekStart,

      /**
      * Constant defining event type for Seek complete
      */
      SeekComplete,

      /**
      * Constant defining event type for Buffer start
      */
      BufferStart,

      /**
      * Constant defining event type for Buffer complete
      */
      BufferComplete,

      /**
      * Constant defining event type for change in Bitrate
      */
      BitrateChange,

      /**
      * Constant defining event type for State start
      */
      StateStart,

      /**
      * Constant defining event type for State end
      */
      StateEnd
  }

}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
```swift
@objc(AEPMediaEvent)
public enum MediaEvent: Int, RawRepresentable {
 // event type for AdBreak start
    case AdBreakStart
 // event type for AdBreak Complete
    case AdBreakComplete
 // event type for Ad Start
    case AdStart
 // event type for Ad Complete
    case AdComplete
 // event type for Ad Skip
    case AdSkip
 // event type for Chapter Start
    case ChapterStart
 // event type for Chapter Complete
    case ChapterComplete
 // event type for Chapter Skip
    case ChapterSkip
 // event type for Seek Start
    case SeekStart
 // event type for Seek Complete
    case SeekComplete
 // event type for Buffer Start
    case BufferStart
 // event type for Buffer Complete
    case BufferComplete
 // event type for change in Bitrate
    case BitrateChange
 // event type for Player State Start
    case StateStart
 // event type for Player State End
    case StateEnd
}
```

**Example**

**Swift**

```swift
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Objective-C**

```objc
[_tracker trackEvent:AEPMediaEventBitrateChange info:nil metadata:nil];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
```objc
/**
 * These enumeration values define the type of a tracking event
 */
typedef NS_ENUM(NSInteger, ACPMediaEvent) {
    /**
     * Constant defining event type for AdBreak start
     */
    ACPMediaEventAdBreakStart,
    /**
     * Constant defining event type for AdBreak complete
     */
    ACPMediaEventAdBreakComplete,
    /**
     * Constant defining event type for Ad start
     */
    ACPMediaEventAdStart,
    /**
     * Constant defining event type for Ad complete
     */
    ACPMediaEventAdComplete,
    /**
     * Constant defining event type for Ad skip
     */
    ACPMediaEventAdSkip,
    /**
     * Constant defining event type for Chapter start
     */
    ACPMediaEventChapterStart,
    /**
     * Constant defining event type for Chapter complete
     */
    ACPMediaEventChapterComplete,
    /**
     * Constant defining event type for Chapter skip
     */
    ACPMediaEventChapterSkip,
    /**
     * Constant defining event type for Seek start
     */
    ACPMediaEventSeekStart,
    /**
     * Constant defining event type for Seek complete
     */
    ACPMediaEventSeekComplete,
    /**
     * Constant defining event type for Buffer start
     */
    ACPMediaEventBufferStart,
    /**
     * Constant defining event type for Buffer complete
     */
    ACPMediaEventBufferComplete,
    /**
     * Constant defining event type for change in Bitrate
     */
    ACPMediaEventBitrateChange,
    /**
     * Constant defining event type for State start
     */
    ACPMediaEventStateStart
    /**
     * Constant defining event type for State end
     */
    ACPMediaEventStateEnd
};
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
import {ACPMediaEvent} from '@adobe/react-native-acpmedia';

ACPMediaEvent.EventAdBreakStart
ACPMediaEvent.EventAdBreakComplete
ACPMediaEvent.EventAdStart
ACPMediaEvent.EventAdComplete
ACPMediaEvent.EventAdSkip
ACPMediaEvent.EventChapterStart
ACPMediaEvent.EventChapterComplete
ACPMediaEvent.EventChapterSkip
ACPMediaEvent.EventSeekStart
ACPMediaEvent.EventSeekComplete
ACPMediaEvent.EventBufferStart
ACPMediaEvent.EventBufferComplete
ACPMediaEvent.EventBitrateChange
ACPMediaEvent.EventStateStart
ACPMediaEvent.EventStateEnd
```
{% endtab %}
{% endtabs %}

### Media resume

Constant to denote that the current tracking session is resuming a previously closed session. This information **must** be provided when starting a tracking session.

{% tabs %}
{% tab title="Android" %}
#### Media resume

**Syntax**

```java
public class MediaConstants {

  public static final class MediaObjectKey {

      /**
      * Constant defining explicit media resumed property. Set this to true on MediaObject if resuming a previously closed session.
      */
      public static final String RESUMED;
  }

}
```

**Example**

```java
HashMap<String, Object> mediaObject = Media.createMediaObject("media-name", "media-id", 60D, MediaConstants.StreamType.VOD, Media.MediaType.Video);

// Attach media resumed information.
mediaObject.put(MediaConstants.MediaObjectKey.RESUMED, true);

_tracker.trackSessionStart(mediaObject, null);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### Media resume

**Syntax**

```swift
public class MediaConstants: NSObject {
 @objc(AEPMediaObjectKey)
 public class MediaObjectKey: NSObject {
        public static let RESUMED = "media.resumed"
    }
}
```

**Example**

**Swift**

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-name", id: "videoId", length: "60", streamType: MediaConstants.StreamType.VOD, mediaType: MediaType.Video)
mediaObject[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Objective-C**

```objc
NSDictionary *mediaObject = [AEPMobileMedia createMediaObjectWith:@"video-name" id:@"video-id" length:60 streamType:AEPMediaStreamType.VOD mediaType:AEPMediaTypeVideo];

// Attach media resumed information.    
NSMutableDictionary *obj  = [mediaObject mutableCopy];
[obj setObject:@YES forKey:AEPMediaObjectKey.RESUMED];

[_tracker trackSessionStart:obj metadata:nil];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Media resume

**Syntax**

```objc
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyMediaResumed;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objc
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName:@"media-name" mediaId:@"media-id" length:60 streamType:ACPMediaStreamTypeVod mediaType:ACPMediaTypeVideo];

// Attach media resumed information.
NSMutableDictionary *obj  = [mediaObject mutableCopy];
[obj setObject:@YES forKey:ACPMediaKeyMediaResumed];

[_tracker trackSessionStart:obj data:nil];
```

**Swift**

```swift
var mediaObject = ACPMedia.createMediaObject(withName: "media-name", mediaId: "media-id", length: 60, streamType: ACPMediaStreamTypeVod, mediaType:ACPMediaType.video)

// Attach media resumed information.
mediaObject[ACPMediaKeyMediaResumed] = true

_tracker.trackSessionStart(mediaObject, data: nil)
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

#### Media resume

```jsx
let mediaObject = ACPMedia.createMediaObject("media-name", "media-id", 60, ACPMediaConstants.ACPMediaStreamTypeVod, ACPMediaType.Video);
mediaObject[ACPMediaConstants.ACPMediaKeyMediaResumed] = true

tracker.trackSessionStart(mediaObject, null);
```
{% endtab %}
{% endtabs %}

