# Migrating to AEPMedia reference

This document is a reference comparison of AEPMedia (3.x) APIs against their equivalent ACPMedia (2.x) APIs.

The AEPMedia extension is implemented purely in Swift and is compatible with the AEPCore Swift SDK. To ensure a smooth transition from the ACPMedia SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application.  If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## AEPMedia classes

| Type          | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| ------------- | :-------------- | --------------------- | --------------------- |
| Primary Class | Media           | AEPMobileMedia        | ACPMedia              |



## AEPMedia APIs

### extensionVersion

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static var extensionVersion: String
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% endtabs %}

### createTracker

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createTracker()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (id<AEPMediaTracker> _Nonnull) createTracker;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+(ACPMediaTracker* _Nullable) createTracker;
```

{% endtab %}
{% endtabs %}

### createTrackerWithConfig

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createTrackerWith(config: [String: Any]?)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (id<AEPMobileMediaTracker> _Nonnull) createTrackerWithConfig:(NSDictionary<NSString *,id) * _Nullable) config;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (ACPMediaTracker* _Nullable) createTrackerWithConfig: (NSDictionary* _Nullable) config;
```

{% endtab %}

{% endtabs %}

### createMediaObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createMediaObjectWith(name: String, id: String, length: Double, streamType: String, mediaType: MediaType) -> [String: Any]?
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (NSDictionary*<NSString *,id> *_Nullable) createMediaObjectWith: (NSString *, _Nonnull) name 
                                                               id: (NSString * _Nonnull) id
                                                           length: (double) length
                                                       streamType: (NSString * _Nonnull) streamType
                                                        mediaType: (enum AEPMediaType) mediaType;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (NSDictionary* _Nonnull) createMediaObjectWithName: (NSString* _Nonnull) name
                                             mediaId: (NSString* _Nonnull) mediaId
                                              length: (double) length
                                          streamType: (NSString* _Nonnull) streamType
                                           mediaType: (ACPMediaType) mediaType;
```

{% endtab %}

{% endtabs %}

### createAdBreakObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createAdBreakObjectWith(name: String, position: Int, startTime: Double) -> [String: Any]?
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (NSDictionary<NSString * ,id> * _Nullable) createAdBreakObjectWith: (NSString * _Nonnull) name
                                                             position: (NSInteger) position
                                                            startTime: (double) startTime,
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (NSDictionary* _Nonnull) createAdBreakObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                             startTime: (double) startTime;
```

{% endtab %}

{% endtabs %}

### createAdObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createAdObjectWith(name: String, id: String, position: Int, length: Double) -> [String: Any]?
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (NSDictionary<NSString * ,id>) * _Nullable) createAdObjectWith: (NSString * _Nonnull) name
                                                              id: (NSString * _Nonnull) id
                                                        position: (NSInteger) position
                                                          length: (double) length;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (NSDictionary* _Nonnull) createAdObjectWithName: (NSString* _Nonnull) name
                                             adId: (NSString* _Nonnull) adId
                                         position: (double) position
                                           length: (double) length;
```

{% endtab %}

{% endtabs %}

### createChapterObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createChapterObjectWith(name: String, position: Int, length: Double, startTime: Double) -> [String: Any]?
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (NSDictionary<NSString * ,id>) * _Nullable) createChapterObjectWith: (NSString * _Nonnull) name
                                                             position: (NSInteger) position
                                                               length: (double) length
                                                            startTime: (double) startTime;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (NSDictionary* _Nonnull) createChapterObjectWithName: (NSString* _Nonnull) name
                                              position: (double) position
                                                length: (double) length
                                             startTime: (double) startTime;
```

{% endtab %}

{% endtabs %}

### createQoEObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createQoEObjectWith(bitrate: Double, startupTime: Double, fps: Double, droppedFrames: Double) -> [String: Any]?
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (NSDictionary<NSString * ,id>) * _Nullable) createQoEObjectWith: (double) bitrate
                                                        startTime: (double) startTime
                                                              fps: (double) fps 
                                                    droppedFrames: (double) droppedFrames;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (NSDictionary* _Nonnull) createQoEObjectWithBitrate: (double) bitrate
                                          startupTime: (double) startupTime
                                                  fps: (double) fps
                                        droppedFrames: (double) droppedFrames;
```

{% endtab %}

{% endtabs %}

### createStateObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func createStateObjectWith(stateName: String) -> [String: Any]
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (NSDictionary<NSString * ,id>) * _Nullable) createStateObjectWith: (NSString * _Nonnull) stateName;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (NSDictionary* _Nonnull) createStateObjectWithName: (NSString* _Nonnull) stateName;
```

{% endtab %}

{% endtabs %}

## Media tracker API reference

### trackEvent

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func trackEvent(event: MediaEvent, info: [String: Any]?, metadata: [String: String]?)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackEvent: (enum AEPMediaEvent) event
               info: (NSDictionary* <NSString *,id> * _Nullable) info
               data: (NSDictionary* <NSString *,NSString> * _Nullable) data;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
  - (void) trackEvent: (ACPMediaEvent) event
                 info: (NSDictionary* _Nullable) info
                 data: (NSDictionary* _Nullable) data;
```

{% endtab %}

{% endtabs %}

### trackSessionStart

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public func trackSessionStart(info: [String: Any], metadata: [String: String]? = nil)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackSessionStart:(NSDictionary<NSString *,id> * _Nonnull) mediaInfo metadata:(NSDictionary<NSString *,NSString *> * _Nullable) data;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) trackSessionStart: (NSDictionary* _Nonnull) mediaInfo data: (NSDictionary* _Nullable) contextData;
```

{% endtab %}

{% endtabs %}

### trackPlay

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func trackPlay()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackPlay;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) trackPlay;
```

{% endtab %}

{% endtabs %}

### trackPause

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func trackPause()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackPause;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) trackPause;
```

{% endtab %}

{% endtabs %}

### trackComplete

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func trackComplete()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackComplete;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) trackComplete;
```

{% endtab %}

{% endtabs %}

### trackSessionEnd

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func trackSessionEnd()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackSessionEnd;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) trackSessionEnd;
```

{% endtab %}

{% endtabs %}

### trackError

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func trackError(errorId: String)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) trackError: (NSString* _Nonnull) errorId;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) trackError: (NSString* _Nonnull) errorId;
```

{% endtab %}

{% endtabs %}

### updateCurrentPlayhead

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func updateCurrentPlayhead(time: Double)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) updateCurrentPlayhead: (double) time;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) updateCurrentPlayhead: (double) time;
```

{% endtab %}

{% endtabs %}

### updateQoEObject

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
func updateQoEObject(qoe: [String: Any])
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
- (void) updateQoEObject: (NSDictionary*<NSString *,id> _Nonnull) qoeObject;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
- (void) updateQoEObject: (NSDictionary* _Nonnull) qoeObject;
```

{% endtab %}

{% endtabs %}

## Media constants

### Media type

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public enum MediaType: Int, RawRepresentable {
 //Constant defining media type for Video streams
 case Audio
 //Constant defining media type for Audio streams
 case Video
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
@objc(AEPMediaType)
public enum MediaType: Int, RawRepresentable {
 //Constant defining media type for Video streams
 case Audio
 //Constant defining media type for Audio streams
 case Video
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
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

### Stream type

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public class StreamType: NSObject {
     // Constant defining stream type for VOD streams.
        public static let VOD = "vod"
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
public class MediaConstants: NSObject {
  @objc(AEPMediaStreamType)
  public class StreamType: NSObject {
     // Constant defining stream type for VOD streams.
        public static let VOD = "vod"
  }
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
/**
 * Constant defining stream type for VOD streams
 */
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaStreamTypeVod;

```

{% endtab %}

{% endtabs %}

{% hint style="info" %}
For the full list of constant type, refer to [Media API reference]((media-api-reference#stream-type)).
{% endhint %}

### Standard video constants

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public class VideoMetadataKeys: NSObject {
        public static let SHOW = "a.media.show"
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
public class MediaConstants: NSObject {
  @objc(AEPVideoMetadataKeys)
  public class VideoMetadataKeys: NSObject {
        public static let SHOW = "a.media.show"
  }
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
FOUNDATION_EXPORT NSString* _Nonnull const ACPVideoMetadataKeyShow;
```

{% endtab %}

{% endtabs %}

{% hint style="info" %}
For the full list of constant type, refer to [Media API reference](media-api-reference#standard-video-constants).
{% endhint %}

### Standard audio constants

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public class AudioMetadataKeys: NSObject {
        public static let ARTIST = "a.media.artist"
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
public class MediaConstants: NSObject {
  @objc(AEPAudioMetadataKeys)
  public class AudioMetadataKeys: NSObject {
        public static let ARTIST = "a.media.artist"
  }
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
FOUNDATION_EXPORT NSString* _Nonnull const ACPAudioMetadataKeyArtist;
```

{% endtab %}

{% endtabs %}

{% hint style="info" %}
For the full list of constant type, refer to [Media API reference](media-api-reference#standard-audio-constants).
{% endhint %}

### Standard ad constants

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
 public class AdMetadataKeys: NSObject {
        public static let ADVERTISER = "a.media.ad.advertiser"
 }
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
public class MediaConstants: NSObject {
  @objc(AEPAdMetadataKeys)
  public class AdMetadataKeys: NSObject {
        public static let ADVERTISER = "a.media.ad.advertiser"
 }
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
FOUNDATION_EXPORT NSString* _Nonnull const ACPAdMetadataKeyAdvertiser;
```

{% endtab %}

{% endtabs %}

{% hint style="info" %}
For the full list of constant type, refer to [Media API reference](media-api-reference#standard-ad-constants).
{% endhint %}

### Player State constants

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public class PlayerState: NSObject {
        public static let FULLSCREEN = "fullscreen"
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
public class MediaConstants: NSObject {
  @objc(AEPMediaPlayerState)
  public class PlayerState: NSObject {
        public static let FULLSCREEN = "fullscreen"
  }
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaPlayerStateFullScreen;
```

{% endtab %}

{% endtabs %}

{% hint style="info" %}
For the full list of constant type, refer to [Media API reference](media-api-reference#player-state-constants).
{% endhint %}

### Media events

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
public enum MediaEvent: Int, RawRepresentable {
 // event type for AdBreak start
    case AdBreakStart
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
@objc(AEPMediaEvent)
public enum MediaEvent: Int, RawRepresentable {
// event type for AdBreak start
    case AdBreakStart
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
typedef NS_ENUM(NSInteger, ACPMediaEvent) {
    /**
     * Constant defining event type for AdBreak start
     */
    ACPMediaEventAdBreakStart,
}
```

{% endtab %}

{% endtabs %}

{% hint style="info" %}
For the full list of constant type, refer to [Media API reference](media-api-reference#media-events).
{% endhint %}

### Media resume

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
 public class MediaObjectKey: NSObject {
        public static let RESUMED = "media.resumed"
    }
}
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
public class MediaConstants: NSObject {
 @objc(AEPMediaObjectKey)
 public class MediaObjectKey: NSObject {
        public static let RESUMED = "media.resumed"
    }
}
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
FOUNDATION_EXPORT NSString* _Nonnull const ACPMediaKeyMediaResumed;
```

{% endtab %}

{% endtabs %}









