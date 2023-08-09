# QuickStart Guide
Getting started with HISPlayer consists of implementing the following steps:

1. Import and configure package   

      1.1. Import package
 
      1.2. Configure Unity for MacOS
   
2. Create your own sample
   
    2.1 Setup HISPlayer Manager
   
    2.2 Attach Unity Resources
   
    2.3 Configure HISPlayer Properties

    2.4 Build and Run

It's also possible to import the [HISPlayer Sample](/import-sample.md) after completing step 1. The sample is a comprehensive example scene using the HISPlayerSDK to help demonstrate features like play, pause, seek, etc.

## 1.1 Import Package
Importing the package is the same as importing other normal packages in Unity. Select the package of HISPlayer SDK and import it.

**Assets > Import Package > Custom Package**

<p align="center">
<img width="450" src="https://github.com/HISPlayer/UnityMacOS-SDK/assets/47497948/9828a86c-37a8-4b9a-b9c4-ae80a84aa942">
</p>

## 1.2 Configure Unity for MacOS
It is necessary to set the **Color Space** as **Linear**.

To set it up go to **Project Settings > Player Settings > Other Settings**

## 2.1 Set up HISPlayer Manager
Create a script (for example **MacOSStreamController**) which is going to inherit from **HISPlayerManager**. It is needed to include the namespace by adding **‘using HISPlayerAPI;’** and add this component to a GameObject. It is recommended to create an **Empty GameObject** for this.

Call the **‘SetUpPlayer()’** function in order to initialize the stream environment internally. This function can be called whenever it’s needed.

For example, using the Awake function:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using HISPlayerAPI;

public class MacOSStreamController : HISPlayerManager
{
    protected override void Awake()
    {
        base.Awake();
        SetUpPlayer();
    }
}
```
It is strictly necessary to use **SetUpPlayer** before using anything else, because this function will initialize everything from the SDK in order to be able to use the rest of the functions (Play, Pause, Seek …).

## 2.2 Attach Unity Resources
Move to **Unity Editor** to attach all the resources. The rendering system is supporting **Material, RawImage, RenderTexture** and **NONE**  Unity’s components.

### <ins>Material</ins>
Move into Assets’ folder for creating a new **Material**. It is possible to create a new **Material** into **Assets > Create > Material**.

<p align="center">
<img width="450" src="https://github.com/HISPlayer/UnityMacOS-SDK/assets/47497948/2cd22826-c9a5-4991-a3ba-0672b3f72a62">
</p>

Attach the material to the GameObject which is going to be used as a screen.

<p align="center">
<img src="./assets/attach-material.png">
</p>

### <ins>Raw Image</ins>
This action will be related to Unity’s Canvas. If there is not a Canvas created yet, creating a **Raw Image** will create one automatically.

For the creation, select **GameObject > UI > Raw Image**

<p align="center">
<img width="450" src="https://github.com/HISPlayer/UnityMacOS-SDK/assets/47497948/ee108f5b-5b01-4a48-b351-e0da8cfb4f64">
</p>

Once it is created, it can be attached to the stream controller script without doing anything else.

### <ins>RenderTexture</ins>
First of all, check if the Resources folder exists and contains the RenderTextures folder. If it doesn’t exist then create it from zero. In this case, look for the Resources folder and copy its contents into the Unity Assets folder. This folder contains Unity RenderTexture resources. Another option is creating RenderTexture in Assets directly.

The **RenderTexture** has to be attached to the GameObject which will be a screen for rendering the multimedia stream.

For creating this object, select **GameObject > 3D Object > Quad**. Then select the GameObject and remove the material attached to its **Mesh Renderer** component, then replace it with the **RenderTexture** created. The **RenderTextures** folder provided by the SDK contains the **Material** folder and this material is the one which is needed to be used for the replacement . If the **RenderTexture** resource has been created from 0, then another option is to grab the **RenderTexture** from the **Assets** folder and drop it at the end of the GameObject’s Inspector, this will create a new material automatically.

<p align="center">
<img src="./assets/rendertexture.png">
</p>

Once all this process it’s done, associate the **RenderTexture** to the script component.

## 2.3 Configure HISPlayer Properties

### <ins>Multi Stream Properties</ins>
Use **Multi Stream Properties** to set all configurations needed for multi stream.However, currently HISPlayer MacOS SDK only supports single stream. Multi stream support will be added in the future. It starts with 0 elements. Adding more elements will be ignored until multi stream support is added. Each element added has its own configuration.
* **Render Mode**:
  * Material: Attach the **Material** asset created to the **Material** section of the element.
  * Raw Image: Attach the **RawImage** asset created to the **RawImage** section of the element.
  * RenderTexture: Attach the **RenderTexture** asset created before to the **RenderTexture** section of the element.
  * NONE: If the stream is not going to be rendered on any surface, select this option.
* **URL**: Add the **URL** associated to the stream. Each stream can have multiple URLs, therefore users can use the same render surface to play different URLs.
* **Auto Play**: Property to determine whether the player will start automatically after set up. The property only works for the beginning of the stream, it is not used to toggle play/pause.

## 2.4 Build and Run:
Once the configuration it’s done, open **‘Build Settings’** and press **‘Build And Run’**.
<p align="center">
<img src="./assets/build-and-run.png" width=60%>
</p>
