# Playing Local Files

HISPlayer MacOS for Unity can play local content from [**Unity Streaming Assets**](./local-files.md#Unity-Streaming-Assets) and the [**Persistent Data Path**](./local-files.md#Persistent-Data-Path) (application's path). 

<br>

## Unity Streaming Assets
To use this format, it’s necessary to create a new folder into the **Assets** folder of Unity named **StreamingAssets**.

<p align="center">
<img alt="image" src="https://github.com/HISPlayer/UnityMacOS-SDK/assets/32887298/442ab52e-ccbd-4044-b9b6-08e981ce42a0">
</p>

### Video File

Add a video content inside the folder and pass the name (**with the extension**) to the **Multi Stream Properties**.
&nbsp;

<p align="center">
<img src="https://github.com/HISPlayer/UnityMacOS-SDK/assets/32887298/e2ee47be-b12a-4c71-879c-a3fef85c3328">
</p>

<p align="center">
<img src="https://github.com/HISPlayer/UnityMacOS-SDK/assets/32887298/ba3eccda-c816-4eb0-9597-dc0c2ccd4cf6">
</p>

In case that subfolders are created inside StreamingAssets, the path of the file **must include the subfolder’s name** inside the field
of Multi Stream Properties, e.g, with a subfolder named **“MyVideos”** the following path must be used: 

**MyVideos/localPlayback.mp4** 
&nbsp;

## Persistent Data Path
The [Persistent Data Path](https://docs.unity3d.com/ScriptReference/Application-persistentDataPath.html) is the internal path of the application.
Unity allows you to access that folder from the C-sharp code with **Application.persistentDataPath**.

The returned path on macOS will be: **~/Library/Application Support/company name/product name**.

The HISPlayer SDK will take this path as the entry point to begin to search the desired local content.

### Video File

Add the video file that is stored inside the *Application.persistentDataPath* and pass the file name (**with the extension**) to the **Multi Stream Properties**.
In case that subfolders are created inside *Application.persistentDataPath* , the path of the file **must include the subfolder’s name** inside the field
of Multi Stream Properties, e.g, with a subfolder named **“MyVideos”** the following path must be used: 

**MyVideos/localPlayback.mp4** 
&nbsp;
