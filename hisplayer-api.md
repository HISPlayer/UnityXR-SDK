# HISPlayer API

## Public API
The following public APIs are provided by **HISPlayerManager**:

* **public string licenseKey**: License key for making the SDK works. License key is not required for Unity Editor usage.

* **public List <StreamProperties> multiStreamProperties**: List of properties for multi stream. Please, don't modify this list directly, use the **AddStream** or **RemoveStream** functions instead.
  
* **public class StreamProperties**:
    * **public StreamProperties(bool isLoopPlaybackEnabled = true, bool isAutoTransitionEnabled = false, bool isUnityAudioEnabled = false)**: Constructor of the class. The received parameters will set the value of **LoopPlayback**, **AutoTransition** and **UnityAudio** properties respectively. 
    * **public HISPlayerRenderMode renderMode**: Type of texture for rendering. **HISPlayerRenderMode.NONE** by default.
    * **public Material material**: Reference to the Unity Material.
    * **public RawImage rawImage**: Reference to the Unity Raw Image.
    * **public RenderTexture renderTexture**: Reference to the Unity Render Texture.
    * **public IntPtr externalSurface**: Reference to the external surface object.
    * **public List \<string\> url**: List of the URLs for the stream.
    * **public list \<string\> urlMimeTypes**: List of the HISPlayerMimeTypes attached to each URL from the url list.
    * **public list \<string\> extSubtitleUrl**: List of the URLs for the external subtitle attached to each URL from the url list.
    * **public bool autoPlay**: If true, the players will start playing automatically after set-up.
    * **public bool EnableRendering**: Determines if the stream will be rendered or not. The value can change in every moment for toggling between render or non-render mode. If true, the player will be rendered. It only can change in runtime.
    * **public bool FlipTextureVertically**: Flip the texture of the stream vertically. This applies for Material, RenderTexture and RawImage. This value should be called before **SetUpPlayer**  or **AddStream** functions. Only supported on Android.
    * **public bool LoopPlayback (Read-only)**: Loop the current playback. It's true by default. To modify this value, please, use the Editor or the constructor **StreamProperties(loopPlayback, autoTransition, unityAudio)**.
    * **public bool AutoTransition (Read-only)**: Change the playback to the next video in the playlist. This action won't have effect when loopPlayback is true. It's false by default. To modify this value, please use the Editor or the constructor **StreamProperties(loopPlayback, autoTransition, unityAudio)**.
    * **public bool UnityAudio (Read-only)**: Retrieves the audio data that can be connected to Unity AudioSource through OnAudioFilterRead() instead of direct device speaker output. Calling SetVolume API to control the audio volume will not work, please control the corresponding Unity Audio Source volume instead. It's false by default. To modify this value, please use the Editor or the constructor **StreamProperties(loopPlayback, autoTransition, unityAudio)**.
    * **public HISPlayerAmbisonicAudio AmbisonicAudio (Read-only)**: Ambisonics audio supporting ambiX format from first order to 3rd order, and TBE format. Enabling Ambisonic will disable Unity Audio. It's set to None or disabled by default. To modify this value, please use the Editor.
    * **public List \<string\> keyServerURI**: List of the DRM license key for each URL.
    * **public List \<DRM_Token\> DRMTokens**: List of the DRM tokens for each URL.

* **public struct DRM_Token**: Information for the DRM token:
    * **public string tokenKey**: Key of the token associated with the URL.
    * **public string tokenValue**: Value of the token associated with the key.

* **public enum HISPlayerRenderMode**: Type of texture for rendering:
    * **RenderTexture**
    * **Material**
    * **RawImage**
    * **NONE**
    * **ExternalSurface**

* **public enum HISPlayerStereoMode**: Type of stereoscopic mode for external surface rendering:
    * **None**
    * **LeftRight**
    * **TopBottom**

* **public enum HISPlayerMimeTypes**: The list of the supported MIME Types:
   * **URL_EXTENSION**: The MIME type will be extracted from the URL extension
   * **HLS**: The "application/x-mpegURL" MIME type will be used
   * **DASH**: The "application/dash+xml" MIME type will be used. Not supported for iOS and macOS      

* **public enum HISPlayerEvent**: The list of events provided by HISPlayer SDK. The events can be used with the virtual functions in the next section:
    * **HISPLAYER_EVENT_PLAYBACK_READY**
    * **HISPLAYER_EVENT_PLAYLIST_CHANGE**
    * **HISPLAYER_EVENT_VIDEO_SIZE_CHANGE**
    * **HISPLAYER_EVENT_PLAYBACK_PLAY**
    * **HISPLAYER_EVENT_PLAYBACK_PAUSE**
    * **HISPLAYER_EVENT_PLAYBACK_STOP**
    * **HISPLAYER_EVENT_PLAYBACK_SEEK**
    * **HISPLAYER_EVENT_VOLUME_CHANGE**
    * **HISPLAYER_EVENT_END_OF_PLAYLIST**
    * **HISPLATER_EVENT_ON_TRACK_CHANGE**
    * **HISPLAYER_EVENT_ON_STREAM_RELEASE**
    * **HISPLAYER_EVENT_TEXT_RENDER**
    * **HISPLAYER_EVENT_AUTO_TRANSITION**
    * **HISPLAYER_EVENT_PLAYBACK_BUFFERING**
    * **HISPLAYER_EVENT_NETWORK_CONNECTED**
    * **HISPLAYER_EVENT_TIMELINE_UPDATED**
    * **HISPLAYER_EVENT_END_OF_CONTENT**

* **public enum HISPlayerError**: The list of errors provided by HISPlayer SDK. The errors can be used with the virtual functions in the next section:
   * **HISPLAYER_ERROR_LICENSE_EXPIRED** (no function on this)
   * **HISPLAYER_ERROR_NOT_VALID_APPID** (no function on this)
   * **HISPLAYER_ERROR_GENERAL_LICENSE_ERROR** (no function on this)
   * **HISPLAYER_ERROR_ANDROID_API_NOT_SUPPORTED** (no function on this)
   * **HISPLAYER_ERROR_LICENSE_DISABLED** (no function on this)
   * **HISPLAYER_ERROR_IMPRESSIONS_LIMIT_REACHED** (no function on this)
   * **HISPLAYER_ERROR_PLAYBACK_DURATION_LIMIT_REACHED** (no function on this)
   * **HISPLAYER_ERROR_PLATFORM_NOT_REGISTERED** (no function on this)
   * **HISPLAYER_ERROR_NETWORK_FAILED**

 * **public enum LogLevel**: The current logging level to filter which log messages are output.
   * **DEBUG** (Level 0): Logs messages useful for debugging and troubleshooting purposes, typically only visible during development.
   * **INFO** (Level 1): Provides general informational messages about the application’s execution.
   * **WARNING** (Level 2): Indicates potential issues or situations that may require attention.
   * **ERROR** (Level 3): Indicates critical errors that may prevent the application from functioning correctly.
   * **NONE** (Level 4): No log messages will appear.

 * **public enum HISPlayerAmbisonicAudio**: Type of ambisonics audio format:
   * **NONE**: No ambisonics audio
   * **AMBIX_4Channels**: 4 channels of first order ambiX
   * **AMBIX_4Channels_2HeadLockedChannels**: 4 channels of first order ambiX with 2 channels of head-locked audio
   * **AMBIX_9Channels**: 9 channels of second order ambiX
   * **AMBIX_9Channels_2HeadLockedChannels**: 9 channels of second order ambiX with 2 channels of head-locked audio
   * **AMBIX_16Channels**: 16 channels of third order ambiX
   * **AMBIX_16Channels_2HeadLockedChannels**: 16 channels of third order ambiX with 2 channels of head-locked audio
   * **TBE_4Channels**: 4 channels of hybrid TBE ambisonics
   * **TBE_4Channels_2HeadLockedChannels**: 4 channels of hybrid TBE ambisonics and 2 channels of head-locked stereo audio
   * **TBE_6Channels**: 6 channels of hybrid TBE ambisonics
   * **TBE_6Channels_2HeadLockedChannels**: 6 channels of hybrid TBE ambisonics and 2 channels of head-locked stereo audio
   * **TBE_8Channels**: 8 channels of hybrid TBE ambisonics
   * **TBE_8Channels_2HeadLockedChannels**: 8 channels of hybrid TBE ambisonics and 2 channels of head-locked stereo audio

* **public struct HISPlayerEventInfo**: The information of the triggered event.
   * **public HISPlayerEvent eventType**: The type of the event triggered.
   * **public int playerIndex**: The index of the player where the event is triggered.
   * **public float param1**: This will have different meanings depending on the event. If there is no information about the parameter, it will have the default value -1.
   * **public float param2**: This will have different meanings depending on the event. If there is no information about the parameter, it will have the default value -1.
   * **public float param3**: This will have different meanings depending on the event. If there is no information about the parameter, it will have the default value -1.
   * **public float param4**: This will have different meanings depending on the event. If there is no information about the parameter, it will have the default value -1.
   * **public string stringInfo**: Log information about the event.

* **public struct HISPlayerErrorInfo**: The information of the triggered error.
   * **public HISPlayerError errorType**: The type of the error triggered.
   * **public int playerIndex**: The index of the player where the error is triggered.
   * **public float param1**: This will have different meanings depending on the error. If there is no information about the parameter, it will have the default value -1.
   * **public string stringInfo**: Log information about the error.

* **public struct HISPlayerTrack**:
   * **public string id**: Id of the track.
   * **public int bitrate**: Bitrate of the track in bits per second.
   * **public int width**: Width of the track.
   * **public int height**: Height of the track.
   * **public int framerate**: Framerate of the track in frames per second.

* **public struct HisPlayerAudioTrack**:
   * **public string id**: ID of the audio track.
   * **public string language**: Language of the audio.

* **public struct HISPlayerCaptionTrack**:
   * **public string id**: ID of the caption.
   * **public string language**: Language of the caption.
 
* **public enum HISPlayerCaptionAlignment**:
   * **LEFT**
   * **RIGHT**
   * **CENTER**
 
* **public struct HISPlayerCaptionElement**: The information of the triggered event turns into caption’s format.
   * **public int playerIndex**: The index of the player where the event is triggered.
   * **public string caption**: The next generated caption text.
   * **public float position**: The horizontal position of the text along the inline (left-right) axis, as a 0.0–1.0 fraction of the display.
   * **public HISPlayerCaptionAlignment alignment**: The information of how text is aligned within the cue box (left, right, center)
   * **public float line**: The vertical position of the text cue box, interpreted as either a 0.0–1.0 fraction.
 
* **public struct VideoSourceOptions**: The information of optional parameters for **AddVideoContent** and **ChangeVideoContent** APIs.
   * **public string extSubtitleURL**: The external subtitle URL.
   * **public string keyServerURI**: The DRM license key for each URL.
   * **public string tokenKey**: The key of the token associated with the URL.
   * **public string tokenValue**: The value of the token associated with the key.
   * **public HISPlayerMimeTypes mimeType**: The MIME type to be used.

## Functions
The following functions are provided by **HISPlayerManager**. They are not public so it’s necessary to create a custom script which inherits from **HISPlayerManager**.

### Virtual functions - These functions can be overridden

#### protected virtual void Awake()
MonoBehaviour function which will be called from the beginning of the scene. It can be overridden but to make the system work it’s necessary to call **base.Awake()** into the overridden function.

#### protected virtual void EventPlaybackReady(HisPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_READY** is triggered.
This event occurs when the current playback of a stream is ready to be used.
Calling functions such as GetTracks before this event is triggered will provide null information.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Number of tracks of the playback.</td>
  </tr>
</table>

#### protected virtual void EventPlaylistChange(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYLIST_CHANGE** is triggered.
This event occurs whenever the current playlist has been modified. It could happen when an URL has been  added or deleted.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Playlist length.</td>
  </tr>
</table>

#### protected virtual void EventVideoSizeChange(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_VIDEO_SIZE_CHANGE** is triggered.
This event occurs whenever the internal video size of the current track changes.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Width of the video.</td>
  </tr>
   <tr>
    <td>param2</td>
    <td>Heigth of the video.</td>
  </tr>
</table>

#### protected virtual void EventPlaybackPlay(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_PLAY** is triggered.
This event occurs whenever an internal playback has been played.

#### protected virtual void EventPlaybackPause(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_PAUSE** is triggered.
This event occurs whenever an internal playback has been paused.

#### protected virtual void EventPlaybackStop(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_STOP** is triggered.
This event occurs whenever an internal playback has been stopped.

#### protected virtual void EventPlaybackSeek(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_SEEK** is triggered.
This event occurs whenever an internal playback has been sought to a new time position.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Value of the old track position in milliseconds.</td>
  </tr>
   <tr>
    <td>param2</td>
    <td>Value of the new track position in milliseconds.</td>
  </tr>
</table>

#### protected virtual void EventVolumeChange(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_VOLUME_CHANGE** is triggered.
This event occurs whenever the volume has been modified.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>New value for the volume.</td>
  </tr>
</table>

#### protected virtual void EventEndOfPlaylist(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_END_OF_PLAYLIST** is triggered.
This event occurs whenever an internal playlist reaches the end of the list.

#### protected virtual void EventOnTrackChange(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_ON_TRACK_CHANGE** is triggered.
This event occurs whenever the tracks of the stream have changed. This event is not triggered by the ABR feature.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Number of video tracks available.</td>
  </tr>
   <tr>
    <td>param2</td>
    <td>Number of subtitles tracks available.</td>
  </tr>
   <tr>
    <td>param2</td>
    <td>Number of audio tracks available.</td>
  </tr>
</table>

#### protected virtual void EventOnStreamRelease(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_ON_STREAM_RELEASE** is triggered.
This event occurs whenever a player/stream has been released.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Number of players after releasing.</td>
  </tr>
</table>

#### protected virtual void EventTextRender(HISPlayerCaptionElement subtitlesInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_TEXT_RENDER** is triggered.
This event occurs whenever a caption's text has been generated.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>caption</td>
    <td>The next generated caption text.</td>
  </tr>
  <tr>
    <td>position</td>
    <td>The horizontal position of the text along the inline (left-right) axis, as a 0.0–1.0 fraction of the display.</td>
  </tr>
  <tr>
    <td>alignment</td>
    <td>The information of how text is aligned within the cue box (left, right, center).</td>
  </tr>
    <tr>
    <td>line</td>
    <td>The vertical position of the text cue box, interpreted as either a 0.0–1.0 fraction.</td>
  </tr>
</table>

#### protected virtual void EventAutoTransition(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPlayerEvent.HISPLAYER_EVENT_AUTO_TRANSITION** is triggered.
This event occurs when the playback has changed to the next video in the playlist automatically.

#### protected virtual void EventPlaybackBuffering(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_BUFFERING** is triggered.
This event occurs whenever an internal playback is buffering.

#### protected virtual void EventEndOfContent(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPlayer_EVENT_END_OF_CONTENT** is triggered.
This event occurs whenever an internal playback reaches the end of the video content.

#### protected virtual void EventNetworkConnected(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPlayerEvent.HISPLAYER_EVENT_NETWORK_CONNECTED** is triggered.
This event occurs whenever the network has been reconnected.

#### protected virtual void EventTimelineUpdated(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPlayerEvent.HISPLAYER_EVENT_TIMELINE_UPDATED** is triggered.
This event occurs whenever the timeline of the current video has been updated. In the case of live content this may happen every certain time during the playback. This may change the current video position value from GetVideoPosition().

#### protected virtual void ErrorInfo(HISPlayerErrorInfo errorInfo)
Override this method to add custom logic when an error callback is triggered. Please, refer to the **HISPlayerError** list.

#### protected virtual void ErrorNetworkFailed(HISPlayerErrorInfo errorInfo)
Override this method to add custom logic when **HISPlayerError.HISPLAYER_ERROR_NETWORK_FAILED** is triggered.
This error occurs when the Internet connection fails.

### Non-virtual functions 
These functions can’t be overridden and they can be used only inside the inherited script. If it’s needed to use some of these functions into the Unity scene, for example with buttons, it is needed to create a public function which connects the button with the API.

#### void SetUpPlayer()
Initialize the player video stream system internally. It is necessary to use this function before anything else.

#### void Release()
Free all resources internally. In the SDK v4.3.0 and below, it's necessary to call this function before changing between Unity scenes or before quitting the application. In the SDK v4.4.0 and above, the release is called automatically when changing scenes or quitting the application and it's not required to call this function. 

#### void Play(int playerIndex)
Play a certain stream giving a **playerIndex**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void Pause(int playerIndex)
Pause a certain stream giving a **playerIndex**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void Stop(int playerIndex)
Stop a certain stream giving a **playerIndex**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void Seek(int playerIndex, long milliseconds)
Seek a certain stream to a certain time giving a **playerIndex** and the time of the video to be sought in **milliseconds**. The stream is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SeekToFrame(int playerIndex, long frameNumber)
Seek a certain stream to a certain frame giving a **playerIndex** and the frame number of the video to be sought. The stream is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SetVolume(int playerIndex, float volume)
Modify the volume of a certain stream giving a **playerIndex**. The **volume** of the track value ranges between 0.0f and 1.0f. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void AddStream(StreamProperties newStream)
Add a new stream to the list multiStreamProperties. The stream must be added using this function instead of changing the list manually.

#### void AddVideoContent(int playerIndex, string url, HISPlayerMimeTypes mimeType = HISPlayerMimeTypes.URL_EXTENSION (optional))
Add new content to a certain player. If the **enableDRM** variable is true, a video content with an empty license will be added. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **url** is the link to the new video. Please, make sure the string is correct. This function supports local file paths. The parameter **mimeType** is optional and indicates which MIME type will be used for the new url.

#### void AddVideoContent(int playerIndex, string url, string keyServerUri,  string tokenKey = “” (optional), string tokenValue = “” (optional), HISPlayerMimeTypes mimeType = HISPlayerMimeTypes.URL_EXTENSION(optional))
Add new content to a certain player and its respective key server uri and tokens if needed (tokenKey and tokenValue are optional parameters). The **enableDRM** variable must be true for using this function. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **url** is the link to the new video. The **keyServerUri** is the license key associated with the URL. Please, make sure the string is correct. This function supports local file paths. The **mimeType** parameter is optional and indicates which MIME type will be used for the new url.

#### void AddVideoContent(int playerIndex, string url, VideoSourceOptions options = default)
Add new content to a certain player with **VideoSourceOptions** which contains optional parameters. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **url** is the link to the new video. The **VideoSourceOptions** contains the following optional parameters:
   * **public string extSubtitleURL**: The external subtitle URL.
   * **public string keyServerURI**: The DRM license key for each URL.
   * **public string tokenKey**: The key of the token associated with the URL.
   * **public string tokenValue**: The value of the token associated with the key.
   * **public HISPlayerMimeTypes mimeType**: The MIME type to be used.

Usage example: `AddVideoContent(playerIndex, "https://...", new VideoSourceOptions { extSubtitleURL = "https://...",  keyServerURI = "https://..."})`

#### void ChangeVideoContent(int playerIndex, int urlIndex)
Change the video’s URL  of a certain player. The next playback will start paused if **autoPlay** is disabled. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **urlIndex** is associated with the index of the element in the list of URLs.

#### void ChangeVideoContent(int playerIndex, string url)
Change the video’s URL of a certain player given a new URL. The next playback will start paused if **autoPlay** is disabled. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The parameter **url** is the link to the new video. Please, make sure the new URL is correctly written. This function supports local file paths. This function will replace the Playlist with the new URL.

#### void ChangeVideoContent(int playerIndex, string url, HISPlayerMimeTypes mimeType)
Change the video’s URL of a certain player given a new URL. The next playback will start paused if **autoPlay** is disabled. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The parameter **url** is the link to the new video. Please, make sure the new URL is correctly written. This function supports local file paths. This function will replace the Playlist with the new URL. The **mimeType** indicates which MIME type will be used for the new url.

#### void ChangeVideoContent(int playerIndex, string url, string keyServerUri, string tokenKey = “” (optional), string tokenValue= “” (optional), HISPlayerMimeTypes, mimeType = HISPlayerMimeTypes.URL_EXTENSION(optional))
Change the video’s URL of a certain player given a new URL with DRM protection (tokenKey and tokenValue are optional parameters). The next playback will start paused if **autoPlay** is disabled. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The parameter **url** is the link to the new video. The **keyServerUri** is the license key associated with the URL. Please, make sure the parameters are correctly written. This function supports local file paths. This function will replace the Playlist with the new element. The **mimeType** parameter is optional and indicates which MIME type will be used for the new url.

#### void ChangeVideoContent(int playerIndex, string url, VideoSourceOptions options = default)
Change the video’s URL of a certain player given a new URL with **VideoSourceOptions** which contains optional parameters. The next playback will start paused if **autoPlay** is disabled. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The parameter **url** is the link to the new video. The **VideoSourceOptions** contains the following optional parameters:
   * **public string extSubtitleURL**: The external subtitle URL.
   * **public string keyServerURI**: The DRM license key for each URL.
   * **public string tokenKey**: The key of the token associated with the URL.
   * **public string tokenValue**: The value of the token associated with the key.
   * **public HISPlayerMimeTypes mimeType**: The MIME type to be used.

Usage example: `ChangeVideoContent(playerIndex, "https://...", new VideoSourceOptions { extSubtitleURL = "https://...",  keyServerURI = "https://..."})`

#### void RemoveVideoContent(int playerIndex, int urlIndex)
Remove content from a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.  The **urlIndex** is associated with the index of the element in the list of URLs.

#### void RemoveStream(int playerIndex)
Remove a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SetPlaybackSpeedRate(int playerIndex, float speed)
Modify the **speed rate** of a certain stream giving a **playerIndex**. The value of the player's speed must be greater (>) than 0.0f and less than or equal (<=) to 8.0f. The default value of player's speed is 1.0f. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### float GetPlaybackSpeedRate(int playerIndex)
Obtain the **speed rate** of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### long GetVideoPosition(int playerIndex)
Provides information about the timeline position in **milliseconds**, of the current video of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### long GetVideoDuration(int playerIndex)
Provides information about the total duration in **milliseconds**, of the current video of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### long GetProgramDateTimeEpoch(int playerIndex)
Get the epoch time (in seconds since 1970) of the first EXT-X-PROGRAM-DATE-TIME tag of a certain player in seconds. Only available for HLS manifests that have the tag information. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### string GetProgramDateTimeString(int playerIndex)
Get the EXT-X-PROGRAM-DATE-TIME value seen in the manifest of a certain player. Only available for HLS manifests that have the tag information. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### HISPlayerTrack[] GetTracks(int playerIndex)
Provides the list of the video tracks of the current video playing on a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetTrackBitrate(int playerIndex, int trackIndex)
Get the bitrate of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetTrackWidth(int playerIndex, int trackIndex)
Get the width of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetTrackHeight(int playerIndex, int trackIndex)
Get the height of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 of the list.

#### int GetVideoWidth(int playerIndex)
Get the width of the current track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetVideoHeight(int playerIndex)
Get the height of the current track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### string GetTrackID(int playerIndex, int trackIndex)
Get the ID of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetTrackCount(int playerIndex)
Get the number of tracks of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void EnableCaptions(int playerIndex, bool enabled)
Enables the captions of the stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### HISPlayerCaptionTrack[] GetCaptionTrackList(int playerIndex)
Provide information about all the captions of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetCaptionsCount(int playerIndex)
Obtain the number of captions of a  certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### string GetCaptionID(int playerIndex, int ccTrackIndex)
Obtain the ID of a certain caption of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### string GetCaptionLanguage(int playerIndex, int ccTrackIndex)
Obtain the language of a certain caption of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SelectCaptionTrack(int playerIndex, int ccTrackIndex)
Select a certain caption of a certain stream to be used. Before using this functions is recommended to use GetCaptionTrackList in order to know all the information about the captions. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SetMaxBitrate(int playerIndex, int bitrate)
Set a new maximum bitrate (in bits per second) of a specific track. This doesn't disable ABR. The possible tracks can be obtained from the tracks returned from the method GetTracks. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SetMinBitrate(int playerIndex, int bitrate)
Set a new minimum bitrate (in bits per second) of a specific track. This doesn't disable ABR. The possible tracks can be obtained from the tracks returned from the method GetTracks. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SelectTrack(int playerIndex, int trackIndex)
Select a certain track of a certain stream to be used as the main track. This action will disable ABR, to enable it again you can use **EnableABR** API. The possible tracks can be obtained from the tracks returned from the method **GetTracks**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### int GetNetworkBandwidth()
Returns the current network bandwidth. This value is an estimation in kbps.
   
#### HisPlayerAudioTrack[] GetAudioTrackList(int playerIndex)
Provide information about all the audio tracks of a certain stream. The playerIndex is associated with the index of the element of Multi Stream Properties, e.g. the index 0 is the element 0 in the list.

#### int GetAudioCount(int playerIndex)
Obtain the number of audio of a  certain stream. The playerIndex is associated with the index of the element of Multi Stream Properties, e.g. the index 0 is the element 0 in the list.
   
#### string GetAudioID(int playerIndex, int audioTrackIndex)
Obtain the ID of a certain audio of a certain player. The playerIndex is associated with the index of the element of Multi Stream Properties, e.g. the index 0 is the element 0 in the list.

#### string GetAudioLanguage(int playerIndex, int audioTrackIndex)
Obtain the language of a certain audio of a certain player. The playerIndex is associated with the index of the element of Multi Stream Properties, e.g. the index 0 is the element 0 in the list.

#### void SelectAudioTrack(int playerIndex, int audioTrackIndex)
Select a certain audio-track of a certain stream to be used. Before using this functions is recommended to use GetAudioTrackList in order to know all the information about the audio-tracks. The playerIndex is associated with the index of the element of Multi Stream Properties, e.g. the index 0 is the element 0 in the list.

#### void EnableABR(int playerIndex)
Enables the ABR to change automatically between tracks. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void DisableABR(int playerIndex)
Disables the ABR to prevent the player from changing tracks regardless of bandwidth. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### bool IsPlaying(int playerIndex)
Check whether the certain player is playing. Returns True if the player is playing. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### bool IsMuted(int playerIndex)
Check whether the certain player is muted. Returns True if the player is muted. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### float GetVolume(int playerIndex)
Get the current audio volume of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### string GetWidevineSecurityLevel(int playerIndex). Get the security level of the loaded Widevine DRM protected content as a string. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### float[][] GetAudioData(int playerIndex, int sampleSizePerChannel)
Get the audio PCM data of each channel in float array. The order of the channel is the same as the order of the stream's audio channel layout, e.g. C L R Ls Rs. The **playerIndex** is the index of the player in multistream properties, the **sampleSizePerChannel** is the requested data size of each audio channel. Please use this API when **UnityAudio** is set to true.

#### void FillAudioData(int playerIndex, float[] audioData, int inputChannelIndex, List&lt;int&gt; speakerChannelIndexes)
Fill the audio buffer with new audio PCM data. The **playerIndex** is the index of the player in multistream properties. The **audioData** is the audio buffer that will be filled with new audio data. The **inputChannelIndex** is the index of the audio channel. The order of the channel index must be the same as the order of the stream's audio channel layout, e.g. C=0, L=1, R=2, Ls=3, Rs=4. The **speakerChannelIndexes** is a list of speaker output channel indices (e.g., L=0, R=1 for Stereo speaker mode). Please use this API when **UnityAudio** is set to true.

#### int GetAudioSessionId(int playerIndex)
Provide the audio session identifier. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### void SynchronizeMultiStreams(int primaryPlayerIndex, int secondaryPlayerIndex, long offsetMs = 0)
Synchronizes the playback of secondary stream following the primary stream. The **primaryPlayerIndex** is the index of the main stream, the **secondaryIndexPlayer** is the index of the second stream that will be synchronized following the main stream. The **offsetMs** (Optional) is the time offset of the secondary player to synchronize with main player in milliseconds. Default value is 0 means both players playback are synchronized to the same timestamp. Put positive value if the secondary player should be played from a point ahead the main player’s current position. Put negative value if the secondary player should be played from a point behind the main player’s current position. The secondary stream will automatically seek following the main stream current time plus the offset. You may call this API after calling **SetUpPlayer**.

#### void SetLogLevel(LogLevel logLevel)
Establishes the amount of logs to be shown. The log levels are represented as an enum of integers. Every type of log whose representative integer is greater or equal to the established log level will be shown. This API should be called before **SetUpPlayer** or **AddStream** APIs.

#### string[] GetAvailableCodecs()
Get the available codecs list on the device. You may call this API before or after **SetUpPlayer**.

#### void SetExternalSurface(int playerIndex, IntPtr surface)
Set the external surface of a certain player to be used. This API will change the internal external surface if it already has been set before. Use this API when you change the overlay shape by passing the new surface. Please call this API after **SetUpPlayer** and you have a valid new surface.

#### void ReleaseExternalSurface(int playerIndex)
Release the external surface from a certain player. This API is optional, only call it before destroying the surface during runtime. Please call this API after **SetUpPlayer**.

#### void SetStereoscopicRendering(int playerIndex, HISPlayerStereoMode stereoMode, ref bool overrideRect, ref Rect srcRectLeft, ref Rect srcRectRight, ref Rect destRectLeft, ref Rect destRectRight)
Set stereoscopic rendering side by side or top/bottom. Only supported with external surface rendering mode. You may call this API after calling **SetUpPlayer**. The parameters marked with ref keyword can be retrieved from public properties such as OVROverlay for Meta Quest. Usage example: 
```
SetStereoscopicRendering(streamIndex, HISPlayerStereoMode.LeftRight, ref overlay.overrideTextureRectMatrix, ref overlay.srcRectLeft, ref overlay.srcRectRight, ref overlay.destRectLeft, ref overlay.destRectRight);
```

#### void EnableSurfaceCopy(int playerIndex, RenderTexture targetTexture)
Enable copy video output frame to RenderTexture. External surface is copied to **targetTexture**. The targetTexture can be applied to any Unity mesh (e.g., a Cube, Quad). Please call this API after **SetUpPlayer**.
