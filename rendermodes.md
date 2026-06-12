# Material / RawImage / RenderTexture Rendering Mode
It is also possible to render the video to **Material**  / **RawImage** / **RenderTexture** without the recommended **externalSurface** render mode with OVR component.

## <ins>Material</ins>
Create a new Material from **Assets > Create > Material** and attach it to the GameObject that is going to be used as screen and to the stream controller component. 

You can also use the **Resources > Materials > HISPlayerDefaultMaterial.mat** we provide in our package. 

In the HISPlayer multistream properties, set the **RenderMode** as **Material**.

<p align="center">
<img width=50% alt="image" src="https://github.com/HISPlayer/UnityAndroid-SDK/assets/47497948/eacab2a8-7cee-4218-add9-98672f250540">
<img width=50% alt="image" src="https://github.com/HISPlayer/UnityAndroid-SDK/assets/47497948/756b60e7-46f6-4efd-9ced-4221a2a782df">
</p>

### Linear Color Space Usage
If you use Linear Color Space in the Unity project settings, please use **HISPlayerDefaultMaterial.mat** in **Packages/HISPlayerSDK/HisPlayer/Resources/Materials/**. 
It uses the **HISPlayerDefaultShader.shader** that will fix color issue with Linear Color Space.

## <ins>Raw Image</ins>
This action will be related to Unity’s Canvas. If there is not a Canvas created yet, creating a **Raw Image** will create one automatically.

For the creation, select **GameObject > UI > Raw Image**. Once it is created, attach it to the stream controller component.

In the HISPlayer multistream properties, set the **RenderMode** as **RawImage**.

<p align="center">
<img width="600" alt="image" src="https://github.com/HISPlayer/UnityAndroid-SDK/assets/47497948/af854bfb-215e-4ec5-bc6e-2c3ad4f0321b">
</p>

### Linear Color Space Usage
If you use Linear Color Space in the Unity project settings, please attach **HISPlayerDefaultMaterialRawImage.mat** in **Packages/HISPlayerSDK/HisPlayer/Resources/Materials/** to the material attribute of the RawImage component.
It uses the **HISPlayerDefaultShaderRawImage.shader** that will fix color issue with Linear Color Space.

## <ins>RenderTexture</ins>
For this you can use the RenderTexture we provide or create a RenderTexture from zero. In the first case, go to the Resources folder of our package and attach the **Resources > Materials > HISPlayerDefaultMaterialRenderTexture.mat** to the GameObject that is going to be used as screen and the **Resources > RenderTextures > HISPlayerRenderTexture.renderTexture** to the stream controller component.

For creating it from zero, select **Assets > Create > Render Texutre** and then create a **Material** referencing the **Render Texture**. This last action can be done automatically by grabbing the **Render Texture** and dropping it at the end of a GameObject's Inspector with the component **Mesh Renderer** with **Material field empty**. This will create the new material inside a **Materials** folder. 

Once all this process it’s done, associate the **RenderTexture** to the script component.

In the HISPlayer multistream properties, set the **RenderMode** as **RenderTexture**.

<p align="center">
<img src="https://github.com/HISPlayer/UnityiOS-SDK/assets/47497948/a0f26bc1-c7b1-432e-ad87-1a2d203d32c8">
</p>

### Linear Color Space Usage
If you use Linear Color Space in the Unity project settings, please use **HISPlayerDefaultRenderTexture.renderTexture** in **Packages/HISPlayerSDK/HisPlayer/Resources/RenderTextures/**. 
This file is a custom RenderTexture with the attached **HISPlayerDefaultMaterialRenderTexture.mat** that will fix color issue with Linear Color Space.
