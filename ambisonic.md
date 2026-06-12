# Ambisonics Audio

HISPlayer SDK v5.0.0 and above supports Ambisonics audio with ambiX format from first order to 3rd order, and TBE format to capture sound in all directions. 
It supports headset rotation listener, so the ambisonics audio is locked to the game world when users move the headset around. 

## Requirements
#### Unity version
- Supported Unity versions: Unity 6

It’s required to set **AmbisonicAudio** property in MultistreamProperties through Unity editor. 
<p align="center">
<img width=60% src="https://github.com/user-attachments/assets/631d643c-051c-477e-8345-527a7dbcc21d">
</p>

* Ambisonics audio cannot be combined with [UnityAudio](./audio-retrieval.md) usage. 
* Only Opus audio codec is supported. Opus is the recommended codec for Ambisonic audio.
* MKV video container is recommended.
* Recommended audio sample rate is 48000Hz.
* Multistream mode with ambisonics is not supported.

For more details, please refer to below APIs section and HISPlayer Meta Quest Ambisonic Sample section.

## Related APIs

**public enum HISPlayerAmbisonicAudio**: Type of ambisonics audio format:
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

**public HISPlayerAmbisonicAudio AmbisonicAudio**: Ambisonics audio supporting ambiX format from first order to 3rd order, and TBE format. Enabling Ambisonic will disable Unity Audio. It's set to None or disabled by default. To modify this value, please use the Editor.

## HISPlayer Meta Quest Ambisonic Sample

Before using the sample, make sure that you have imported HISPlayer SDK. If not, please follow the [**Quickstart Guide**](./setup-guide.md).

Please download the sample here: [HISPlayerMetaQuestAmbisonicSample.unitypackage](https://downloads.hisplayer.com/Unity/Quest/HISPlayerMetaQuestAmbisonicSample.unitypackage) and import it to your Unity project.

* Open **Assets\HISPlayerMetaQuestAmbisonicSample\Scenes\HISPlayerMetaQuestAmbisonicSample.unity**.
* Import TextMeshPro. Go to Unity Window > TextMeshPro > Import TMP Essential Resources.
* If you received a license key from HISPlayer, input the license key through the Inspector Unity window: **StreamController** GameObject > HISPlayerSample component > **License Key**
* Open File > Build Settings > Add Open Scenes
* Build and Run

To check how to set up the SDK and API usage, please refer to Assets/HISPlayerMetaQuestAmbisonicSample/Scripts/Sample/HISPlayerSample.cs and StreamController GameObject in the Editor.

The sample includes 3 local videos in StreamingAssets:
* 3rd order ambisonics (16 channels) ambiX format
* 2nd order ambisonics (9 channels) ambiX format
* 8 channels + 2 channels head-locked stereo TBE format 

By default the sample plays local video with 3rd order ambisonics (16 channels) ambiX format. 
