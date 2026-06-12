# Stereoscopic Video

HISPlayer SDK v5.1.0 and above support stereoscopic Side-By-Side (Left/Right) and Top/Bottom video rendering. **MV-HEVC** video codec is also supported with maximum resolution 1080p for smooth playback. 

There are 2 ways to render stereoscopic video depending on the selected **Render Mode**.

## External Surface Render Mode
If you use **External Surface** Render Mode in HISPlayer multistream properties, please use below API in your script:
#### void SetStereoscopicRendering(int playerIndex, HISPlayerStereoMode stereoMode, ref bool overrideRect, ref Rect srcRectLeft, ref Rect srcRectRight, ref Rect destRectLeft, ref Rect destRectRight)
Set stereoscopic rendering side by side or top/bottom. Only supported with external surface rendering mode. You may call this API after calling **SetUpPlayer** API. The parameters marked with ref keyword can be retrieved from public properties of OVROverlay. Usage example: 
```
SetStereoscopicRendering(streamIndex, HISPlayerStereoMode.LeftRight, ref overlay.overrideTextureRectMatrix, ref overlay.srcRectLeft, ref overlay.srcRectRight, ref overlay.destRectLeft, ref overlay.destRectRight);
```

## Material / RenderTexture / RawImage Render Mode
If you use **Material** or **RenderTexture** Render Mode in HISPlayer multistream properties, after creating your RenderTexture and Material, please attach **HISPlayerStereoscopicShader** shader to your Material.

Set the 3D Layout option to **Left Right** or **Top Bottom** depending on your stereoscopic video format.

<p align="center">
  <img width="70%" alt="image" src="https://github.com/user-attachments/assets/04e2dbdf-d102-4e42-b0f6-acb50799444e">
</p>

If you use **RawImage** Render Mode, please attach the Material with HISPlayerStereoscopicShader above to the material attribute of the RawImage component.

<p align="center">
  <img width="70%" alt="image" src="https://github.com/user-attachments/assets/29d98b03-edc3-4008-8ba5-19109e2fc150">
</p>

## HISPlayer Meta Quest Stereo Sample

Before using the sample, make sure that you have imported HISPlayer SDK. If not, please follow the [**Quickstart Guide**](./setup-guide.md).

Please download the sample here: [HISPlayer_MetaQuest_Stereo_Sample.unitypackage](https://downloads.hisplayer.com/Unity/Quest/HISPlayer_MetaQuest_Stereo_Sample.unitypackage) and import it to your Unity project.

The sample includes 2 scenes:
* **HISPlayerMetaQuestStereoExtSurface**: Render a local stereoscopic Side-By-Side video with **ExternalSurface** Render Mode. This render mode is recommended for better performance. **SetStereoscopicRendering** API is called in the script. 
* **HISPlayerMetaQuestStereoRT**: Render a local stereoscopic Side-By-Side video with **Render Texture** Render Mode. **HISPlayerStereoscopicShader.shader** is used.

To use the sample, follow below steps:
* Open **Assets\HISPlayerMetaQuestStereoSample\Scenes\ISPlayerMetaQuestStereoExtSurface.unity** or **Assets\HISPlayerMetaQuestStereoSample\Scenes\HISPlayerMetaQuestStereoRT.unity**.
* Import TextMeshPro. Go to Unity Window > TextMeshPro > Import TMP Essential Resources.
* If you received a license key from HISPlayer, input the license key through the Inspector Unity window: **StreamController** GameObject > HISPlayerSample component > **License Key**
* Open File > Build Settings > Add Open Scenes
* Build and Run

To check how to set up the SDK and API usage, please refer to Assets/HISPlayerMetaQuestStereoSample/Scripts/Sample/HISPlayerSample.cs and StreamController GameObject in the Editor.

## HISPlayer Meta Quest MV-HEVC Sample

Before using the sample, make sure that you have imported HISPlayer SDK. If not, please follow the [**Quickstart Guide**](./setup-guide.md).

Please download the sample here: [HISPlayer_MetaQuest_MV-HEVC_Sample.unitypackage](https://downloads.hisplayer.com/Unity/Quest/HISPlayer_MetaQuest_MV-HEVC_Sample.unitypackage) and import it to your Unity project.

The sample includes 2 scenes:
* **HISPlayerMetaQuestMvHevcExtSurface**: Render a local stereoscopic Side-By-Side MV-HEVC video with **ExternalSurface** Render Mode. This render mode is recommended for better performance. **SetStereoscopicRendering** API is called in the script. 
* **HISPlayerMetaQuestMvHevcRT**: Render a local stereoscopic Side-By-Side MV-HEVC video with **Render Texture** Render Mode. **HISPlayerStereoscopicShader.shader** is used.

To use the sample, follow below steps:
* Open **Assets\HISPlayerMetaQuestMVHEVCSample\Scenes\ISPlayerMetaQuestMvHevcExtSurface.unity** or **Assets\HISPlayerMetaQuestMVHEVCSample\Scenes\HISPlayerMetaQuestMvHevcRT.unity**.
* Import TextMeshPro. Go to Unity Window > TextMeshPro > Import TMP Essential Resources.
* If you received a license key from HISPlayer, input the license key through the Inspector Unity window: **StreamController** GameObject > HISPlayerSample component > **License Key**
* Open File > Build Settings > Add Open Scenes
* Build and Run

To check how to set up the SDK and API usage, please refer to Assets/HISPlayerMetaQuestMVHEVCSample/Scripts/Sample/HISPlayerSample.cs and StreamController GameObject in the Editor.
