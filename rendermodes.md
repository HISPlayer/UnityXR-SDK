# Render Modes

HISPlayer supports multiple rendering modes to suit different use cases and platforms. The recommended mode for XR/VR applications is **External Surface** for optimal performance & latency and DRM L1 support. Other modes like **RenderTexture**, **Material**, and **RawImage** are also available.

## External Surface

This mode uses **XR Video Layers**, which are managed inside the HISPlayer SDK for high resolution video rendering performance and DRM L1 support. It is the preferred choice for immersive experiences on Android XR headsets (e.g., Meta Quest, Pico, Galaxy XR, etc).

### Setup

1. Create an empty GameObject.
<p align="center">
  <img width="543" height="257" alt="image" src="https://github.com/user-attachments/assets/d4d4709a-9549-48b9-a928-25477b6f6d5e" />
</p>


> Important: There is no need to add any additional components. The HISPlayer SDK will automatically add the XR Video Layer component internally.
    
2. In your script (inheriting from `HISPlayerManager`), set the `renderMode` to `HISPlayerRenderMode.ExternalSurface` in the `MultiStreamProperties`.

<p align="center">
  <img width="544" height="652" alt="image" src="https://github.com/user-attachments/assets/4316d6c2-3b93-40c2-9e5d-cdcbf2383203" />
</p>

3. Set the XR Layer properties related to External Surface:
    * **Video Screen**: Attach the Unity Game Object's Transform where video will be rendered.
    * **Order**: Order of the rendered video relative to the whole Unity scene: 1 (Default) or higher will render the video over everything the camera renders. -1 or lower will render the video behind everything. Never put 0 which is the order of Unity's own Default Scene Layer. Set unique value across multiple streams to avoid multipe video rendering order conflict. Stereo layer takes two orders - this one and the next.
    * **Projection**: Select the projection type. **Quad** is a flat/rectilinear screen placed by the Video Screen above. **Equirect360** and **Equirect180** wrap it around the viewer for 360/180° video.
    * **Stereo Mode**: Select stereoscopic mode. **None** for Monoscopic video. **Left Right** or **Top Bottom** for stereoscopic video. A stereo layer occupies two composition orders - the one above and the next one up.
    * **Match Video Aspect**: Match the render surface quad to the video's aspect ratio. For example a 21:9 film is not stretched to fill a 16:9 quad. The quad never grows past the Video Screen's scale. **Quad only**.
    * **Radius**: Radius in metres of the equirect sphere. 0 is default for 360 video to make it infinite. **Equirect 360/180 only**.

> Important: Do not set the `StreamProperties.externalSurface` property. This property is set automatically by the SDK.


## RenderTexture

This mode renders video to a `RenderTexture`, which can then be displayed on any 3D object or UI element. It is suitable for both XR and non‑XR projects.

### Setup

1. Create a **RenderTexture** asset via **Assets > Create > RenderTexture**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/bc948402-e5aa-45eb-aeae-ad2541282448" alt="texto" width="50%" style="height: auto;" />
</p>

2. Create a **Material**, assign the **RenderTexture** to its `_MainTex property`, and ensure it uses the `HISPlayer/HISPlayerDefaultShader` shader for correct video rendering.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0bdf3ff0-1fb5-44bd-8208-a02246bf4cd4" alt="texto" width="50%" style="height: auto;" />
</p>

3. Set the `renderMode` to `HISPlayerRenderMode.RenderTexture` in the `MultiStreamProperties` and assign the **RenderTexture** to the `renderTexture` field in your `HISPlayerManager` script.

<p align="center">
  <img src="https://github.com/user-attachments/assets/721fcfd2-bb79-433b-baac-d098be16b1ca" alt="texto" width="50%" style="height: auto;" />
</p>

4. Assign the created Material to the MeshRenderer (or the appropriate renderer component) of the GameObject that will display the video.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b68f8b03-8214-44c7-85a4-b3cb31470130" alt="texto" width="50%" style="height: auto;" />
</p>

> **Tip:** Pre‑configured assets are available in the package:
> - **RenderTexture:** `Packages/HISPlayerSDK/HisPlayer/Resources/RenderTextures/HISPlayerRenderTexture.renderTexture`
> - **Material:** `Packages/HISPlayerSDK/HisPlayer/Resources/Materials/HISPlayerDefaultMaterialRenderTexture.mat` (already uses the correct shader)

### Linear Color Space

For **Linear Color Space** projects, it is essential to use the **`HISPlayer/HISPlayerDefaultShader`** shader in your Material to correct color issues. The pre‑configured Material (`HISPlayerDefaultMaterialRenderTexture.mat`) already includes this shader.

## Material

This mode renders video directly onto a standard Unity **Material**, which can be applied to any 3D object with a `MeshRenderer`.

### Setup

1. Create a **Material** and ensure it uses the `HISPlayer/HISPlayerDefaultShader` shader for correct video rendering.

<p align="center">
  <img src="https://github.com/user-attachments/assets/6361eead-28fc-45e7-9e85-05d43e5068a6" alt="texto" width="50%" style="height: auto;" />
</p>

2. Set the `renderMode` to `HISPlayerRenderMode.Material` in the `MultiStreamProperties` and assign the **Material** to the `material` field in your `HISPlayerManager` script.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b9a87c0b-4617-4708-8c96-3f26e928010b" alt="texto" width="50%" style="height: auto;" />
</p>

3. Assign the created Material to the MeshRenderer (or the appropriate renderer component) of the GameObject that will display the video.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b68f8b03-8214-44c7-85a4-b3cb31470130" alt="texto" width="50%" style="height: auto;" />
</p>

> **Tip:** Pre‑configured assets are available in the package:
> - **Material:** `Packages/HISPlayerSDK/HisPlayer/Resources/Materials/HISPlayerDefaultMaterial.mat` (already uses the correct shader)

### Linear Color Space

For **Linear Color Space** projects, it is essential to use the **`HISPlayer/HISPlayerDefaultShader`** shader in your Material to correct color issues. The pre‑configured Material (`HISPlayerDefaultMaterial.mat`) already includes this shader.

## RawImage

This mode renders video to a **RawImage** component on a Unity UI Canvas, ideal for 2D overlays or in‑game menus.

### Setup

1. Create a **RawImage** UI element (**GameObject > UI > Raw Image**). A Canvas will be created automatically if none exists.
2. Set the `renderMode` to `HISPlayerRenderMode.RawImage` in the `MultiStreamProperties` and assign the **RawImage** to the `rawImage` field in your `HISPlayerManager` script.

<p align="center">
  <img src="https://github.com/user-attachments/assets/c3d4af99-547e-4508-b92b-989fa45b0df0" alt="texto" width="50%" style="height: auto;" />
</p>

### Linear Color Space

No additional shader changes are required for Raw Image mode.
