# Media API Reference

## Create Media Tracker

Creates media tracker instance to track the playback session.

{% tabs %}
{% tab title="Android" %}
### createTracker

The callback will be invoked to return the created tracker instance, or in case of error, `null` is returned.

#### Syntax

```java
public static void createTracker(AdobeCallback<MediaTracker> callback)
```

#### Example

```java
AdobeCallback<MediaTracker> createdClb = new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

{% endtab %}

{% tab title="iOS" %}
### createTracker

The callback will be invoked to return the created tracker instance, or in case of error, `nil` is returned.

#### Syntax

```objectivec
+(void) createTracker: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;
```

#### Example

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

## Create Media Object

Create an instance of Media object.

| Variable Name | Description                   | Required |
|---------------|-------------------------------|----------|
| name          | Media name                    | Yes      |
| mediaId       | Media unique identifier       | Yes      |
| length        | Media length                  | Yes      |
| streamType    | [Stream type](#stream-type) | Yes      |
| mediaType     | [Media type](#media-type)   | Yes      |

{% tabs %}
{% tab title="Android" %}

### createMediaObject

Returns a HashMap instance which contains information about the media.

#### Syntax

```java
public static HashMap<String, Object> createMediaObject(String name, String mediaId, Double length, String streamType, MediaType mediaType);
```

#### Example

```java
HashMap<String, Object> mediaInfo = Media.createMediaObject("video-name", "video-id", 60D, MediaConstants.StreamType.VOD, Media.MediaType.Video);
```

{% endtab %}

{% tab title="iOS" %}

### createMediaObjectWithName

Returns a NSDictionary instance which contains information about the media.

#### Syntax

```objectivec
+ (NSDictionary* _Nonnull) createMediaObjectWithName: (NSString* _Nonnull) name
                                             mediaId: (NSString* _Nonnull) mediaId
                                              length: (double) length
                                          streamType: (NSString* _Nonnull) streamType
                                           mediaType: (ACPMediaType) mediaType;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *mediaObject = [ACPMedia createMediaObjectWithName: @"video-name"
                                                        mediaId: @"video-id"
                                                         length: 60,
                                                     streamType: ACPMediaStreamTypeVod
                                                      mediaType: ACPMediaTypeVideo];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}

## Create AdBreak Object

Create an instance of AdBreak object.

| Variable Name | Description                                                              | Required |
|---------------|--------------------------------------------------------------------------|----------|
| name          | Ad break name such as pre-roll, mid-roll, and post-roll.                 | Yes      |
| position      | The number position of the ad break within the content, starting with 1. | Yes      |
| startTime     | Playhead value at the start of the ad break.                             | Yes      |

{% tabs %}
{% tab title="Android" %}

### createAdBreakObject

Returns a HashMap instance which contains information about the adbreak.

#### Syntax

```java
public static HashMap<String, Object> createAdBreakObject(String name, Long position, Double startTime);
```

#### Example

```java
HashMap<String, Object> adBreakInfo = Media.createAdBreakObject("adbreak-name", 1L, 0D);
```

{% endtab %}

{% tab title="iOS" %}

### createAdBreakObjectWithName

Returns a NSDictionary instance which contains information about the adbreak.

#### Syntax

```objectivec
+ (NSDictionary* _Nonnull) createAdBreakObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                             startTime: (double) startTime;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *adBreakObject = [ACPMedia createAdBreakObjectWithName: @"adbreak-name"
                                                         position: 1,
                                                        startTime: 0];
```

**Swift**

```swift
TBD
```

{% endtab %}
{% endtabs %}

## Create Ad Object

Create an instance of Ad object.

| Variable Name | Description                                                         | Required |
|---------------|---------------------------------------------------------------------|----------|
| name          | Friendly name of the ad.                                            | Yes      |
| adId          | Unique identifier for the ad.                                       | Yes      |
| position      | The number position of the ad within the ad break, starting with 1. | Yes      |
| length        | Ad length                                                           | Yes      |

{% tabs %}
{% tab title="Android" %}

### createAdObject

Returns a HashMap instance which contains information about the ad.

#### Syntax

```java
public static HashMap<String, Object> createAdObject(String name, String adId, Long position, Double length);
```

#### Example

```java
HashMap<String, Object> adInfo = Media.createAdObject("ad-name", "ad-id", 1L, 15D);
```

{% endtab %}

{% tab title="iOS" %}

### createAdObjectWithName

Returns a NSDictionary instance which contains information about the ad.

#### Syntax

```objectivec
+ (NSDictionary* _Nonnull) createAdObjectWithName: (NSString* _Nonnull) name
                                             adId: (NSString* _Nonnull) adId
                                         position: (double) position
                                           length: (double) length;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *adObject = [ACPMedia createAdObjectWithName: @"ad-name"
                                                        adId: @"ad-id"
                                                    position: 1,
                                                      length: 15];
```

**Swift**

```swift
TBD
```

{% endtab %}
{% endtabs %}

## Create Chapter Object

Create an instance of Chapter object.

| Variable Name | Description        | Required |
|---------------|--------------------|----------|
| name          | Chapter name       | Yes      |
| position      | Chapter position   | Yes      |
| length        | Chapter length     | Yes      |
| startTime     | Chapter start time | Yes      |

{% tabs %}
{% tab title="Android" %}

### createChapterObject

Returns a HashMap instance which contains information about the chapter.

#### Syntax

```java
public static HashMap<String, Object> createChapterObject(String name, Long position, Double length, Double startTime);
```

#### Example

```java
HashMap<String, Object> chapterInfo = Media.createChapterObject("chapter-name", 1L, 60D, 0D);
```

{% endtab %}

{% tab title="iOS" %}

### createChapterObjectWithName

Returns a NSDictionary instance which contains information about the chapter.

#### Syntax

```objectivec
+ (NSDictionary* _Nonnull) createChapterObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                                length: (double) length
                                             startTime: (double) startTime;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *chapterObject = [ACPMedia createChapterObjectWithName: @"chapter-name"
                                                      position: 1
                                                        length: 60,
                                                     startTime: 0];
```

**Swift**

```swift
TBD
```

{% endtab %}
{% endtabs %}

## Create QoE Object

Create an instance of QoE object.


| Variable Name | Description              | Required |
|---------------|--------------------------|----------|
| bitrate       | Current bitrate          | Yes      |
| startupTime   | Startup time             | Yes      |
| fps           | FPS value                | Yes      |
| droppedFrames | Number of dropped frames | Yes      |

{% tabs %}
{% tab title="Android" %}

### createQoEObject

Returns a HashMap instance which contains information about the quality of experience.

#### Syntax

```java
public static HashMap<String, Object> createQoEObject(Long bitrate, Double startupTime, Double fps, Long droppedFrames);
```

#### Example

```java
HashMap<String, Object> qoeInfo = Media.createQoEObject(10000000L, 2D, 23D, 10D);
```

{% endtab %}

{% tab title="iOS" %}

### createQoEObjectWithBitrate

Returns a NSDictionary instance which contains information about the quality of experience.

#### Syntax

```objectivec
+ (NSDictionary* _Nonnull) createQoEObjectWithBitrate: (double) bitrate
                                          startupTime: (double) startupTime
                                                  fps: (double) fps
                                        droppedFrames: (double) droppedFrames;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
NSDictionary *qoeObject = [ACPMedia createQoEObjectWithBitrate: 10000000
                                                   startupTime: 2
                                                           fps: 23,
                                                 droppedFrames: 10];
```

**Swift**

```swift
TBD
```

{% endtab %}
{% endtabs %}

# Media Tracker API Reference

## trackSessionStart

Track the intention to start playback. This starts a tracking session on the media tracker instance.

{% tabs %}
{% tab title="Android" %}
### trackSessionStart

#### Syntax

```java
public void trackSessionStart(Map<String, Object> mediaInfo, Map<String, String> contextData);
```

#### Example

```java 
_tracker.trackSessionStart(mediaInfo, mediaMetadata);
```

{% endtab %}

{% tab title="iOS" %}
### trackSessionStart

#### Syntax

```objectivec
- (void) trackSessionStart: (NSDictionary* _Nonnull) mediaInfo data: (NSDictionary* _Nullable) contextData;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackSessionStart:mediaObject data:videoMetadata];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}

## trackPlay

TBD

{% tabs %}
{% tab title="Android" %}
### trackPlay

#### Syntax

```java
public void trackPlay();
```

#### Example

```java 
_tracker.trackPlay();
```

{% endtab %}

{% tab title="iOS" %}
### trackPlay

#### Syntax

```objectivec
- (void) trackPlay;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackPlay];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}


## trackPause

TBD

{% tabs %}
{% tab title="Android" %}
### trackPause

#### Syntax

```java
public void trackPause();
```

#### Example

```java 
_tracker.trackPause();
```

{% endtab %}

{% tab title="iOS" %}
### trackPause

#### Syntax

```objectivec
- (void) trackPause;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackPause];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}


## trackComplete

TBD

{% tabs %}
{% tab title="Android" %}
### trackComplete

#### Syntax

```java
public void trackComplete();
```

#### Example

```java 
_tracker.trackComplete();
```

{% endtab %}

{% tab title="iOS" %}
### trackComplete

#### Syntax

```objectivec
- (void) trackComplete;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackComplete];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}


## trackSessionEnd

TBD

{% tabs %}
{% tab title="Android" %}
### trackSessionEnd

#### Syntax

```java
public void trackSessionEnd();
```

#### Example

```java 
_tracker.trackSessionEnd();
```

{% endtab %}

{% tab title="iOS" %}
### trackSessionEnd

#### Syntax

```objectivec
- (void) trackSessionEnd;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackSessionEnd];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}

## trackError

TBD

{% tabs %}
{% tab title="Android" %}
### trackError

#### Syntax

```java
public void trackError(String errorId);
```

#### Example

```java 
_tracker.trackError("errorId");
```

{% endtab %}

{% tab title="iOS" %}
### trackError

#### Syntax

```objectivec
- (void) trackError: (NSString* _Nonnull) errorId;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackError:@"errorId"];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}

## trackEvent

TBD

{% tabs %}
{% tab title="Android" %}
### trackEvent

#### Syntax

```java
  public void trackEvent(Media.Event event, Map<String, Object> info, Map<String, String> contextData) {
```

#### Example

```java
_tracker.trackEvent(Media.Event.BufferStart, null, null);
```

{% endtab %}

{% tab title="iOS" %}
### trackEvent

#### Syntax

```objectivec
  - (void) trackEvent: (ACPMediaEvent) event info: (NSDictionary* _Nullable) info data:
    (NSDictionary* _Nullable) data;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker trackEvent:ACPMediaEventBufferStart info:nil data:nil];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}

## updateCurrentPlayhead

Method to update current playhead.


| Variable Name | Description|
|---------------|------------|
| time          | Current position of the playhead. For VOD, value is specified in seconds from the beginning of the media item. For live streaming, return playhead position if available or the current UTC time in seconds otherwise. |

{% tabs %}
{% tab title="Android" %}
### updateCurrentPlayhead

#### Syntax

```java
public void updateCurrentPlayhead(double time);
```

#### Example

```java 
_tracker.updateCurrentPlayhead(1);
```

{% endtab %}

{% tab title="iOS" %}
### updateCurrentPlayhead

#### Syntax

```objectivec
- (void) updateCurrentPlayhead: (double) time;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[_tracker updateCurrentPlayhead: 1];
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}

## updateQoEObject

Method to update current QoS information.


| Variable Name | Description|
|---------------|------------|
| qoeObject     | Map instance containing current QoS information. This method can be called multiple times during a playback session. Player implementation must always return the most recently available QoS data. |

{% tabs %}
{% tab title="Android" %}
### updateQoEObject

#### Syntax

```java
public void updateQoEObject(Map<String, Object> qoeObject);
```

#### Example

```java 
TBD
```

{% endtab %}

{% tab title="iOS" %}
### updateQoEObject

#### Syntax

```objectivec
- (void) updateQoEObject: (NSDictionary* _Nonnull) qoeObject;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
TBD
```

**Swift**

```swift
TBD
```
{% endtab %}
{% endtabs %}


# Media Constants

## Media Type

This defines the type of a media that is currently tracked.

{% tabs %}
{% tab title="Android" %}
```java 
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

## Stream Type

This defines the stream type of the content that is currently tracked.

{% tabs %}
{% tab title="Android" %}
```java 
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

## Standard Video Constants

This defines the standard metadata keys for video streams.

{% tabs %}
{% tab title="Android" %}
```java 

/**
 * These constant strings define standard video metadata keys.
 */

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

```
{% endtab %}

{% tab title="iOS" %}
```objectivec

/**
 * These constant strings define standard video metadata keys.
 */

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


## Standard Audio Constants

This defines the standard metadata keys for audio streams.

{% tabs %}
{% tab title="Android" %}
```java 

/**
 * These constant strings define standard audio metadata keys.
 */

public static final class AudioMetadataKeys {
  public static final String ARTIST = "a.media.artist";
  public static final String ALBUM = "a.media.album";
  public static final String LABEL = "a.media.label";
  public static final String AUTHOR = "a.media.author";
  public static final String STATION = "a.media.station";
  public static final String PUBLISHER = "a.media.publisher";
}

```
{% endtab %}

{% tab title="iOS" %}
```objectivec

/**
 * These constant strings define standard audio metadata keys.
 */

FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyArtist;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAlbum;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyLabel;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyAuthor;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyStation;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyPublisher;

```

{% endtab %}
{% endtabs %}


## Standard Ad Constants

This defines the standard metadata keys for ads.

{% tabs %}
{% tab title="Android" %}
```java 

/**
 * These constant strings define standard metadata keys for ads.
 */

public static final class AdMetadataKeys {
  public static final String ADVERTISER = "a.media.ad.advertiser";
  public static final String CAMPAIGN_ID = "a.media.ad.campaign";
  public static final String CREATIVE_ID = "a.media.ad.creative";
  public static final String PLACEMENT_ID = "a.media.ad.placement";
  public static final String SITE_ID = "a.media.ad.site";
  public static final String CREATIVE_URL = "a.media.ad.creativeURL";
}


```
{% endtab %}

{% tab title="iOS" %}
```objectivec

/**
 * These constant strings define standard metadata keys for ads.
 */

FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyAdvertiser;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCampaignId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyPlacementId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeySiteId;
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyCreativeUrl;

```

{% endtab %}
{% endtabs %}

## Media Events

This defines the type of a tracking event.

{% tabs %}
{% tab title="Android" %}
```java 

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
