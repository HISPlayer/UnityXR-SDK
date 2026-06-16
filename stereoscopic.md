# Stereoscopic Video

HISPlayer SDK supports stereoscopic Side-By-Side (Left/Right) and Top/Bottom video rendering. **MV-HEVC** video codec is also supported with maximum resolution 1080p for smooth playback. 

## Material / RenderTexture / RawImage Render Mode
Use **Material** or **RenderTexture** Render Mode in HISPlayer multistream properties, after creating your RenderTexture and Material, please attach **HISPlayerStereoscopicShader** shader to your Material.

Set the 3D Layout option to **Left Right** or **Top Bottom** depending on your stereoscopic video format.

<p align="center">
  <img width="70%" alt="image" src="https://github.com/user-attachments/assets/04e2dbdf-d102-4e42-b0f6-acb50799444e">
</p>

If you use **RawImage** Render Mode, please attach the Material with HISPlayerStereoscopicShader above to the material attribute of the RawImage component.

<p align="center">
  <img width="70%" alt="image" src="https://github.com/user-attachments/assets/29d98b03-edc3-4008-8ba5-19109e2fc150">
</p>
