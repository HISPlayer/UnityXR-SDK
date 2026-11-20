# Download Video Content for Offline Playback

The HISPlayer SDK supports downloading video content for offline playback. 
If you received a license key from HISPlayer, input the license key through the Unity Inspector window: **DownloadController GameObject > HISPlayer Download Sample (Script)** component > **License Key**.

<p align="center">
<img src="image-3.png" width="400">
</p>

### Script

Please check the `Assets/OpenXRSample/Scripts/Sample/HISPlayerDownloadSample.cs` script. The script must inherit from `HISPlayerDownloadManager`. It is also necessary to add the `using HISPlayerAPI;` dependency.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;
using HISPlayerAPI;

public class HISPlayerDownloadSample : HISPlayerDownloadManager
{
    ...
}
```

It is necessary to call `SetUpDownloader()` before calling any other APIs. This function initializes everything required to use the HISPlayer Download APIs.

## Download Video Content

There are three download APIs. `DownloadAdaptiveStream()` downloads adaptive streaming content such as HLS and DASH, and `DownloadAdaptiveStreamWithDRM()` downloads Widevine DRM protected adaptive streaming content. `DownloadProgressive()` downloads progressive files.

### Adaptive Video Content (HLS, DASH) Download
Adaptive content downloading supports both non-DRM and Widevine DRM content.
Adaptive streaming content is composed of several different bitrate tracks. The downloaded content will include only one bitrate track because the content will be played locally.

#### Select a Bitrate Track
With the `maxWidth` and `maxHeight` parameters, you can specify the track to download. The SDK will internally select the highest bitrate track that meets your `maxWidth` and `maxHeight` values.

#### Download Widevine DRM Content
Use `DownloadAdaptiveStreamWithDRM()` to download Widevine DRM content. Together with the content, the SDK acquires an offline licence from the license server, so the content can be played later without a network connection.
The `useDRML1` parameter selects the Widevine security level of the offline licence: `true` for L1, `false` for L3. Choose the level according to the render mode that will play the content offline:
* **L1**: the content can be played offline only in **External Surface** render mode.
* **L3**: the content can be played offline in every render mode, including **External Surface**.

A content URL can hold only one download. If you download the same URL again, for example with another security level, the new download replaces the existing one.

#### Select Audio and Subtitle Tracks
Content can include multiple audio and subtitle tracks. 
With the `audioLanguages` and `subtitleLanguages` parameters, you can specify which tracks will be downloaded.
Each parameter accepts a comma-separated language string. For example, if the content includes English, Korean, and French audio tracks and you want to download only the English and Korean tracks, you can set `audioLanguages` to `"en, kr"`. If you want to download all tracks, you can set the parameter to `NULL` or `"ALL"`.

### Progressive Video Content Download
The `DownloadProgressive()` API downloads a progressive file (for example, an MP4) for offline playback.

## Manage Downloaded Content
All downloaded content is identified by its content URL.
Downloaded files are stored in the local application's cache folder.
Therefore, if the application is uninstalled, all downloaded contents are removed as well.
We provide several APIs to manage downloaded content. Please refer to the [**HISPlayer API**](/hisplayer-api.md) for more details.

## Offline Playback

When playing content, the SDK internally checks whether the content has already been downloaded. If the content is available locally, it will play in offline mode. For partially downloaded content, the player will utilize the locally downloaded segments and seamlessly switch to streaming for any missing segments.

Downloaded Widevine DRM content is played with the offline licence stored at download time, at the security level selected for that download (L1 or L3). The DRM settings used for online playback do not change this level.
