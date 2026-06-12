# Audio Data Retrieval and Unity Audio Connection

It is possible to retrieve the raw Audio PCM data and connect it to Unity Audio Source component through [OnAudioFilterRead()](https://docs.unity3d.com/6000.1/Documentation/ScriptReference/MonoBehaviour.OnAudioFilterRead.html) to make spatial/3D audio. 

## Requirements
#### Unity version
- Supported Unity versions: 2022, 2023, Unity 6

It’s required to set **UnityAudio** property in MultistreamProperties to True through Unity editor or script.

<p align="center">
<img width=40% src="https://github.com/user-attachments/assets/e80ceca8-5e05-4ee9-be04-6269a795be51">
</p>

To get the audio data, you can choose either using **GetAudioData()** or **FillAudioData()** API. 
Please refer to below APIs section and HISPlayer Meta Quest Spatial Audio Sample section.

## Related APIs

**public bool UnityAudio (Read-only)**: Retrieves the audio data that can be connected to Unity AudioSource through OnAudioFilterRead() instead of direct device speaker output. Calling SetVolume API to control the audio volume will not work, please control the corresponding Unity Audio Source volume instead. It's false by default. To modify this value, please, use the Editor or the constructor **StreamProperties(loopPlayback, autoTransition, unityAudio)**.

#### float[][] GetAudioData(int playerIndex, int sampleSizePerChannel)
Retrieves the PCM audio data for each channel as an array of floats. The channel order matches the stream's audio channel layout (e.g., C, L, R, Ls, Rs).

**Parameters:**

- **playerIndex**: The index of the player in the multistream properties.
- **sampleSizePerChannel**: The requested data size for each audio channel.

<br>*Note: The channel format differs depending on the source audio stream's channel count and speaker mode. Please refer to [AudioSource channel mapping](#audiosource-channel-mapping).*

Please use this API when **UnityAudio** is set to true.

#### void FillAudioData(int playerIndex, float[] audioData, int inputChannelIndex, List&lt;int&gt; speakerChannelIndexes)
Fills the provided audio buffer with new PCM audio data.

**Parameters:**

- playerIndex: The index of the player in the multistream properties.
- audioData: The audio buffer to be filled with the new audio data.
- inputChannelIndex: The index of the audio channel. The order of the channel index must match the stream's audio channel layout (e.g., C=0, L=1, R=2, Ls=3, Rs=4).
- speakerChannelIndexes: A list of speaker output channel indices (e.g., L=0, R=1 for Stereo speaker mode).

<br>*Note: The channel format differs depending on the source audio stream's channel count and speaker mode. Please refer to [AudioSource channel mapping](#audiosource-channel-mapping).*

Please use this API when **UnityAudio** is set to true.

## AudioSource channel mapping
The following outlines the format and channel indices for multi-channel PCM audio data:
- 2 channel  L(0) + R(1) + …
- 3 channel : L(0) + R(1) + C(2) + …
- 5 channel : C(0) + L(1) + R(2) + Lr(3) + Rr(4) + …
- 5.1 channel: L(0) + R(1) + C(2) + LFE(3) + Ls(4) + Rs(5) + …

The following details the format and speakerChannelIndex values for each Unity speaker mode:
- Mono (1 channel): C(0) + ....
- Stereo (2 channels): L(0) + R(1) + ...
- Quad (4 channels): L(0) + R(1) + Lr(2) + Rr(3) + ...
- Surround (5 channels): L(0) + R(1) + C(2) + Lr(3) + Rr(4) + ...
- Surround 5.1 (6 channels): L(0) + R(1) + C(2) + LFE(3) + Lr(4) + Rr(5) + ... 
- Surround 7.1 (8 channels): L(0) + R(1) + C(2) + LFE(3) + Lr(4) + Rr(5) + Ls(6) + Rs(7) + ...
- Prologic DTS (2 channels): L(0) + R(1) + ...

The default speaker mode can be configured in Unity via: **Edit → Project Settings... → Audio → Default Speaker Mode**.
<p align="center">
    <img width=60% src="image-1.png">
</p>

### Sample Application Implementation
Our sample application includes the **GetAudioSource.cs** and **FillAudioSource.cs** scripts to demonstrate this functionality.
The sample is configured to use **Stereo** Speaker Mode and utilizes five separate AudioSource components (Center, Left, Right, Left Surround, Right Surround).

Because the speaker mode is Stereo:
The **Center AudioSource** needs to play through both the left and right speakers simultaneously. Therefore, its Input Channel Index is 0 (Center), and its Speaker Channel Indexes list is set to 0 (Left) and 1 (Right).
For the **Left AudioSource**, the Input Channel Index is 1 (Left), and its Speaker Channel Indexes list contains only 0 (Left).
The remaining AudioSource components follow this same routing logic based on their respective positions.

<p align="center">
    <img width=40% src="image.png">
</p>

## HISPlayer Meta Quest Spatial Audio Sample

Please download the sample here: [HISPlayer_MetaQuest_SpatialAudio_Sample.unitypackage](https://downloads.hisplayer.com/Unity/Quest/HISPlayer_MetaQuest_OVROverlay_SpatialAudio_SampleV2.unitypackage) and import it to your Unity project.

Before using the sample, make sure that you have imported HISPlayer SDK. If not, please follow the [**Quickstart Guide**](./setup-guide.md).

The sample plays local video with 5 audio channels that are connected to 5 AudioSources. You may modify the sample depending on your audio channel count. 
Please refer to the sample package which consists of the following Unity scenes in **HISPlayerSpatialAudioSample\Scenes**:
- **HISPlayerFillAudioSample**: Sample utilizing **FillAudioData()** API by passing the float[] data from each Unity Audio Source **OnAudioFilterRead()** which the data buffer will be filled automatically. To check the APIs usage, please refer to all scripts in **HISPlayerSpatialAudioSample\Scripts\Sample\Audio\FillAudioSample**.
- **HISPlayerGetAudioSample**: Sample utilizing **GetAudioData()** API in Unity Audio Source **OnAudioFilterRead()** for center channel, and the new audio data is shared to other channel classes. The new audio data will be copied to the float[] data of **OnAudioFilterRead()** for each channel. To check the APIs usage, please refer to all scripts in **HISPlayerSpatialAudioSample\Scripts\Sample\Audio\GetAudioSample**.
