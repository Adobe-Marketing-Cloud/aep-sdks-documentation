# Media API reference

## Media API reference

### Create a media tracker

Creates a media tracker instance that tracks the playback session.

{% tabs %}
{% tab title="Android" %}
#### createTracker

The callback is invoked to return the created tracker instance. If an error occurs, `null` is returned.

**Syntax**

```java
public static void createTracker(AdobeCallback<MediaTracker> callback)
```

**Example**

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### createTracker

The callback will be invoked to return the created tracker instance. If an error occurs, `nil` is returned.

**Syntax**

```objectivec
+(void) createTracker: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;
```

**Examples**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

**Swift**

```swift
ACPMedia.createTracker({mediaTracker in
    // Use the instance for tracking media.
}
```
{% endtab %}
{% endtabs %}

### Create Media Object

Creates an instance of the Media object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Media name | Yes |
| `mediaId` | Media unique identifier | Yes |
| `length` | Media length | Yes |
| `streamType` | [Stream type](media-api-reference.md#stream-type) | Yes |
| `mediaType` | [Media type](media-api-reference.md#media-type) | Yes |

{% tabs %}
{% tab title="Android" %}
#### createMediaObject

Returns a HashMap instance that contains information about the media.

**Syntax**

```java
public static HashMap<String, Object> createMediaObject(String name,
                                                        String mediaId,
                                                        Double length,
                                                        String streamType,
                                                        MediaType mediaType);
```

**Example**

```java
HashMap<String, Object> mediaInfo = Media.createMediaObject("video-name",
                                                            "video-id",
                                                            60D,
                                                            MediaConstants.StreamType.VOD,
                                                            Media.MediaType.Video);
```
{% endtab %}

{% tab title="iOS" %}
#### createMediaObjectWithName

Returns an NSDictionary instance that contains information about the media.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createMediaObjectWithName: (NSString* _Nonnull) name
                                             mediaId: (NSString* _Nonnull) mediaId
                                              length: (double) length
                                          streamType: (NSString* _Nonnull) streamType
                                           mediaType: (ACPMediaType) mediaType;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
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
{% endtabs %}

### Create AdBreak Object

Creates an instance of the AdBreak object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Ad break name such as pre-roll, mid-roll, and post-roll. | Yes |
| `position` | The number position of the ad break within the content, starting with 1. | Yes |
| `startTime` | Playhead value at the start of the ad break. | Yes |

{% tabs %}
{% tab title="Android" %}
#### createAdBreakObject

Returns a HashMap instance that contains information about the ad break.

**Syntax**

```java
public static HashMap<String, Object> createAdBreakObject(String name, Long position, Double startTime);
```

**Example**

```java
HashMap<String, Object> adBreakObject = Media.createAdBreakObject("adbreak-name", 1L, 0D);
```
{% endtab %}

{% tab title="iOS" %}
#### createAdBreakObjectWithName

Returns an NSDictionary instance that contains information about the ad break.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createAdBreakObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                             startTime: (double) startTime;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *adBreakObject = [ACPMedia createAdBreakObjectWithName: @"adbreak-name"
                                                           position: 1
                                                          startTime: 0];
```

**Swift**

```swift
let adBreakObject = ACPMedia.createAdBreakObject(withName: "adbreak-name", position: 1, startTime: 0)
```
{% endtab %}
{% endtabs %}

### Create Ad Object

Creates an instance of the Ad object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Friendly name of the ad. | Yes |
| `adId` | Unique identifier for the ad. | Yes |
| `position` | The number position of the ad within the ad break, starting with 1. | Yes |
| `length` | Ad length | Yes |

{% tabs %}
{% tab title="Android" %}
#### createAdObject

Returns a HashMap instance that contains information about the ad.

**Syntax**

```java
public static HashMap<String, Object> createAdObject(String name, String adId, Long position, Double length);
```

**Example**

```java
HashMap<String, Object> adInfo = Media.createAdObject("ad-name", "ad-id", 1L, 15D);
```
{% endtab %}

{% tab title="iOS" %}
#### createAdObjectWithName

Returns an NSDictionary instance that contains information about the ad.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createAdObjectWithName: (NSString* _Nonnull) name
                                             adId: (NSString* _Nonnull) adId
                                         position: (double) position
                                           length: (double) length;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *adObject = [ACPMedia createAdObjectWithName: @"ad-name"
                                                     adId: @"ad-id"
                                                 position: 1
                                                   length: 15];
```

**Swift**

```swift
let adObject = ACPMedia.createAdObject(withName: "ad-name", adId: "ad-id", position: 1, length: 15)
```
{% endtab %}
{% endtabs %}

### Create Chapter Object

Creates an instance of the Chapter object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `name` | Chapter name | Yes |
| `position` | Chapter position | Yes |
| `length` | Chapter length | Yes |
| `startTime` | Chapter start time | Yes |

{% tabs %}
{% tab title="Android" %}
#### createChapterObject

Returns a HashMap instance that contains information about the chapter.

**Syntax**

```java
public static HashMap<String, Object> createChapterObject(String name,
                                                          Long position,
                                                          Double length,
                                                          Double startTime);
```

**Example**

```java
HashMap<String, Object> chapterInfo = Media.createChapterObject("chapter-name", 1L, 60D, 0D);
```
{% endtab %}

{% tab title="iOS" %}
#### createChapterObjectWithName

Returns an NSDictionary instance that contains information about the chapter.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createChapterObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                                length: (double) length
                                             startTime: (double) startTime;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *chapterObject = [ACPMedia createChapterObjectWithName: @"chapter-name"
                                                           position: 1
                                                             length: 60
                                                          startTime: 0];
```

**Swift**

```swift
let chapterObject = ACPMedia.createChapterObject(withName: "chapter-name", position: 1, length: 60, startTime: 0)
```
{% endtab %}
{% endtabs %}

### Create QoE Object

Creates an instance of the QoE object.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `bitrate` | Current bitrate | Yes |
| `startupTime` | Startup time | Yes |
| `fps` | FPS value | Yes |
| `droppedFrames` | Number of dropped frames | Yes |

{% tabs %}
{% tab title="Android" %}
#### createQoEObject

Returns a HashMap instance that contains information about the quality of experience.

**Syntax**

```java
public static HashMap<String, Object> createQoEObject(Long bitrate,
                                                      Double startupTime,
                                                      Double fps,
                                                      Long droppedFrames);
```

**Example**

```java
HashMap<String, Object> qoeInfo = Media.createQoEObject(10000000L, 2D, 23D, 10D);
```
{% endtab %}

{% tab title="iOS" %}
#### createQoEObjectWithBitrate

Returns an NSDictionary instance that contains information about the quality of experience.

**Syntax**

```objectivec
+ (NSDictionary* _Nonnull) createQoEObjectWithBitrate: (double) bitrate
                                          startupTime: (double) startupTime
                                                  fps: (double) fps
                                        droppedFrames: (double) droppedFrames;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *qoeObject = [ACPMedia createQoEObjectWithBitrate: 10000000
                                                   startupTime: 2
                                                           fps: 23
                                                 droppedFrames: 10];
```

**Swift**

```swift
let qoeObject = ACPMedia.createQoEObject(withBitrate: 10000000, startupTime: 2, fps: 23, droppedFrames: 10)
```
{% endtab %}
{% endtabs %}

## Media tracker API reference

### trackSessionStart

Track the intention to start playback. This starts a tracking session on the media tracker instance. For more information, see [Media Resume](media-api-reference.md#media-resume)

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `mediaInfo` | Media Information created using [createMediaObject](media-api-reference.md#createMediaObject) | Yes |
| `contextData` | Optional Media context data. Use [standard video constants](media-api-reference.md#standard-video-constants) or [standard audio constants](media-api-reference.md#standard-audio-constants) for standard metadata keys. | No |

{% tabs %}
{% tab title="Android" %}
#### trackSessionStart

**Syntax**

```java
public void trackSessionStart(Map<String, Object> mediaInfo, Map<String, String> contextData);
```

**Example**

```java
HashMap<String, Object> mediaObject = Media.createMediaObject("media-name", "media-id", 60D, MediaConstants.StreamType.VOD, Media.MediaType.Video);

HashMap<String, String> mediaMetadata = new HashMap<String, String>();
// Standard metadata keys provided by adobe.
mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, "Sample Episode");
mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, "Sample Show");

// Custom metadata keys
mediaMetadata.put("isUserLoggedIn", "false");
mediaMetadata.put("tvStation", "Sample TV Station");

_tracker.trackSessionStart(mediaInfo, mediaMetadata);
```
{% endtab %}

{% tab title="iOS" %}
#### trackSessionStart

**Syntax**

```objectivec
- (void) trackSessionStart: (NSDictionary* _Nonnull) mediaInfo data: (NSDictionary* _Nullable) contextData;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
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

**Swift**

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
{% endtabs %}

### trackPlay

Track media play or resume after a previous pause.

{% tabs %}
{% tab title="Android" %}
#### trackPlay

**Syntax**

```java
public void trackPlay();
```

**Example**

```java
_tracker.trackPlay();
```
{% endtab %}

{% tab title="iOS" %}
#### trackPlay

**Syntax**

```objectivec
- (void) trackPlay;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackPlay];
```

**Swift**

```swift
_tracker.trackPlay()
```
{% endtab %}
{% endtabs %}

### trackPause

Track media pause.

{% tabs %}
{% tab title="Android" %}
#### trackPause

**Syntax**

```java
public void trackPause();
```

**Example**

```java
_tracker.trackPause();
```
{% endtab %}

{% tab title="iOS" %}
#### trackPause

**Syntax**

```objectivec
- (void) trackPause;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackPause];
```

**Swift**

```swift
_tracker.trackPause()
```
{% endtab %}
{% endtabs %}

### trackComplete

Track media complete. Call this method only when the media has been completely viewed.

{% tabs %}
{% tab title="Android" %}
#### trackComplete

**Syntax**

```java
public void trackComplete();
```

**Example**

```java
_tracker.trackComplete();
```
{% endtab %}

{% tab title="iOS" %}
#### trackComplete

**Syntax**

```objectivec
- (void) trackComplete;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackComplete];
```

**Swift**

```swift
_tracker.trackComplete()
```
{% endtab %}
{% endtabs %}

### trackSessionEnd

Track the end of a viewing session. Call this method even if the user does not view the media to completion.

{% tabs %}
{% tab title="Android" %}
#### trackSessionEnd

**Syntax**

```java
public void trackSessionEnd();
```

**Example**

```java
_tracker.trackSessionEnd();
```
{% endtab %}

{% tab title="iOS" %}
#### trackSessionEnd

**Syntax**

```objectivec
- (void) trackSessionEnd;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackSessionEnd];
```

**Swift**

```swift
_tracker.trackSessionEnd()
```
{% endtab %}
{% endtabs %}

### trackError

Track an error in media playback.

| Variable Name | Description | Required |
| :--- | :--- | :---: |
| `errorId` | Error Information | Yes |

{% tabs %}
{% tab title="Android" %}
#### trackError

**Syntax**

```java
public void trackError(String errorId);
```

**Example**

```java
_tracker.trackError("errorId");
```
{% endtab %}

{% tab title="iOS" %}
#### trackError

**Syntax**

```objectivec
- (void) trackError: (NSString* _Nonnull) errorId;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackError:@"errorId"];
```

**Swift**

```swift
_tracker.trackError("errorId")
```
{% endtab %}
{% endtabs %}

### trackEvent

Method to track media events.

| Variable Name | Description |
| :--- | :--- |
| `event` | [Media event](media-api-reference.md#media-events) |
| `info` | For AdBreakStart event, AdBreak information is created using [Create AdBreak Object](media-api-reference.md#create-adbreak-object).  For AdStart event, Ad information is created using [Create Ad Object](media-api-reference.md#create-ad-object).  For ChapterStart event, Chapter information is created using [Create Chapter Object](media-api-reference.md#create-chapter-object).  This is not required for other events. |
| `data` | Optional context data can be provided for AdStart and ChapterStart events. This is not required for other events. |

{% tabs %}
{% tab title="Android" %}
#### trackEvent

**Syntax**

```java
  public void trackEvent(Media.Event event,
                         Map<String, Object> info,
                         Map<String, String> data);
```

**Examples**

**Tracking AdBreaks**

```java
// AdBreakStart
  HashMap<String, Object> adBreakObject = Media.createAdBreakObject("adbreak-name", 1L, 0D);
  _tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null);

// AdBreakComplete
  _tracker.trackEvent(Media.Event.AdBreakComplete, null, null);
```

**Tracking Ads**

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

**Tracking Chapters**

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

**Tracking Playback events**

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

**Tracking Bitrate change**

```java
// If the new bitrate value is available provide it to the tracker.
  HashMap<String, Object> qoeObject = Media.createQoEObject(2000000L, 2D, 25D, 10D);
  _tracker.updateQoEObject(qoeObject);

// Bitrate change
  _heartbeat.trackEvent(Media.Event.BitrateChange, null, null);
```
{% endtab %}

{% tab title="iOS" %}
#### trackEvent

**Syntax**

```objectivec
  - (void) trackEvent: (ACPMediaEvent) event
                 info: (NSDictionary* _Nullable) info
                 data: (NSDictionary* _Nullable) data;
```

**Examples**

**Tracking AdBreaks**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
// AdBreakStart
  NSDictionary* adBreakObject = [ACPMedia createAdBreakObjectWithName:@"adbreak-name" position:1 startTime:0];
  [_tracker trackEvent:ACPMediaEventAdBreakStart mediaObject:adBreakObject data:nil];

// AdBreakComplete
  [_tracker trackEvent:ACPMediaEventAdBreakComplete mediaObject:nil data:nil];
```

**Swift**

```swift
// AdBreakStart
  let adBreakObject = ACPMedia.createAdBreakObject(withName: "adbreak-name", position: 1, startTime: 0)
  _tracker.trackEvent(ACPMediaEvent.adBreakStart, mediaObject: adBreakObject, data: nil)

// AdBreakComplete
  _tracker.trackEvent(ACPMediaEvent.adBreakComplete, mediaObject: nil, data: nil)
```

**Tracking Ads**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
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

**Swift**

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

**Tracking Chapters**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
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

**Swift**

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

**Tracking Playback events**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
// BufferStart
  [_tracker trackEvent:ACPMediaEventBufferStart info:nil data:nil];

// BufferComplete
  [_tracker trackEvent:ACPMediaEventBufferComplete info:nil data:nil];

// SeekStart
  [_tracker trackEvent:ACPMediaEventSeekStart info:nil data:nil];

// SeekComplete
  [_tracker trackEvent:ACPMediaEventSeekComplete info:nil data:nil];
```

**Swift**

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

**Tracking Bitrate change**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
// If the new bitrate value is available provide it to the tracker.
  NSDictionary* qoeObject = [ACPMedia createQoEObjectWithBitrate:2000000 startupTime:2 fps:25 droppedFrames:10];
  [_tracker updateQoEObject:qoeObject];

// Bitrate change
  [_tracker trackEvent:ACPMediaEventBitrateChange info:nil data:nil];
```

**Swift**

```swift
// If the new bitrate value is available provide it to the tracker.
  let qoeObject = ACPMedia.createQoEObject(withBitrate: 2000000, startupTime: 2, fps: 25, droppedFrames: 10)
  _tracker.updateQoEObject(qoeObject)

// Bitrate change
  _tracker.trackEvent(ACPMediaEvent.bitrateChange, mediaObject: nil, data: nil)
```
{% endtab %}
{% endtabs %}

### updateCurrentPlayhead

Provide media tracker with current media playhead. For accurate tracking, call this multiple times when the playhead changes.

| Variable Name | Description |
| :--- | :--- |
| `time` | Current playhead in seconds. For VOD, the value is specified in seconds from the beginning of the media item. For live streaming, return the playhead position if available, or the current UTC time in seconds if not available. |

{% tabs %}
{% tab title="Android" %}
#### updateCurrentPlayhead

**Syntax**

```java
public void updateCurrentPlayhead(double time);
```

**Example**

```java
_tracker.updateCurrentPlayhead(1);
```
{% endtab %}

{% tab title="iOS" %}
#### updateCurrentPlayhead

**Syntax**

```objectivec
- (void) updateCurrentPlayhead: (double) time;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker updateCurrentPlayhead:1];
```

**Swift**

```swift
_tracker.updateCurrentPlayhead(1)
```
{% endtab %}
{% endtabs %}

### updateQoEObject

Provide media tracker with current QoE information. For accurate tracking, call this multiple times when the media player provides updated QoE information.

| Variable Name | Description |
| :--- | :--- |
| `qoeObject` | Current QoE information that was created by using [Create QoE Object](media-api-reference.md#create-qoe-object). |

{% tabs %}
{% tab title="Android" %}
#### updateQoEObject

**Syntax**

```java
public void updateQoEObject(Map<String, Object> qoeObject);
```

**Example**

```java
HashMap<String, Object> qoeObject = Media.createQoEObject(1000000L, 2D, 25D, 10D);
_tracker.updateQoEObject(qoeObject);
```
{% endtab %}

{% tab title="iOS" %}
#### updateQoEObject

**Syntax**

```objectivec
- (void) updateQoEObject: (NSDictionary* _Nonnull) qoeObject;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary* qoeObject = [ACPMedia createQoEObjectWithBitrate:1000000 startupTime:2 fps:25 droppedFrames:10];
[_tracker updateQoEObject:qoeObject];
```

**Swift**

```swift
let qoeObject = ACPMedia.createQoEObject(withBitrate: 1000000, startupTime: 2, fps: 25, droppedFrames: 10)
_tracker.updateQoEObject(qoeObject)
```
{% endtab %}
{% endtabs %}

## Media constants

### Media Type

This defines the type of a media that is currently tracked.

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

{% tab title="iOS" %}
```objectivec
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
{% endtabs %}

### Stream Type

This defines the stream type of the content that is currently tracked.

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

{% tab title="iOS" %}
```objectivec
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
{% endtabs %}

### Standard video constants

This defines the standard metadata keys for video streams.

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

{% tab title="iOS" %}
```objectivec
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
{% endtabs %}

### Standard audio constants

This defines the standard metadata keys for audio streams.

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

{% tab title="iOS" %}
```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyArtist;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAlbum;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyLabel;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAuthor;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyStation;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyPublisher;
```
{% endtab %}
{% endtabs %}

### Standard ad constants

This defines the standard metadata keys for ads.

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

{% tab title="iOS" %}
```objectivec
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyAdvertiser;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCampaignId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyPlacementId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeySiteId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeUrl;
```
{% endtab %}
{% endtabs %}

### Media events

This defines the type of a tracking event.

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
  }

}
```
{% endtab %}

{% tab title="iOS" %}
```objectivec
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
};
```
{% endtab %}
{% endtabs %}

### Media resume

Constant to denote the current tracking session is resuming a previously closed session. This information must be provided when starting a tracking session.

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

_heartbeat.trackSessionStart(mediaObject, null);
```
{% endtab %}

{% tab title="iOS" %}
#### Media Resume

**Syntax**

```objectivec
  FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyMediaResumed;
```

**Example**

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
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
{% endtabs %}

