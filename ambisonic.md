# Ambisonics Audio

HISPlayer SDK supports Ambisonics audio with ambiX format from first order to 3rd order, and TBE format to capture sound in all directions. 
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

For more details, please refer to below APIs section.

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
