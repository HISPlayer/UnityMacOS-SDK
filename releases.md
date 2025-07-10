# HISPlayer Unity MacOS SDK Release Notes

### Version 4.8.0
##### July 7, 2025
- [**Improvement**] Enhancement to InspectorGUI to dynamically show/hide certain options.

### Version 4.5.0
##### December 4, 2024
- [**Added**] AddStream and RemoveStream APIs

### Version 4.4.0
##### September 10, 2024
- [**Added**] Release API is called automatically when stopping the Editor, changing scenes or closing the app
- [**Added**] EventVideoSizeChange - eventInfo.param3 is catching the internal rotation value of the original video

### Version 4.3.0
##### August 8, 2024
- [**Added**] **HISPLAYER_EVENT_VIDEO_SIZE_CHANGE** and **EventVideoSizeChange**.
    - This event occurs whenever the internal video size of the current track changes
- [**Added**] New HISPlayer Video Uploader feature. Turn local videos into streaming videos such as HLS or DASH. This videos are going to be stored in our server for you. Please, on the Editor refer to:
    - [HISPlayer Video Upload documentation](https://hisplayer.github.io/UnityVideoUpload/#/)
- [**Improvement**] Optimized HISPlayer Settings log messages
- [**Improvement**] Optimized Event and Error listeners
- [**Improvement**] Optimized license checking
- [**Improvement**] Optimized HISPlayer API function commentaries to be more clear
- [**Improvement**] Optimized runtime log messages

### Version 3.4.1
##### April 23, 2024
- [**Improvement**] Improvement of software robustness

### Version 3.4.0
##### April 10, 2024
- [**Added**] Local Playback Persistent Datapath support
- [**Added**] HISPLAYER_ERROR_PLATFORM_NOT_REGISTERED error event
- [**Added**] URL_EXTENSION, HLS and DASH MIME Types support. Please, refer to HISPlayerMimeTypes on [HISPlayer API](https://hisplayer.github.io/UnityMacOS-SDK/#/hisplayer-api)
    -  URL_EXTENSION (Default)
    -  HLS
    -  DASH
-  [**Added**] HISPlayerError.HISPLAYER_ERROR_NETWORK_FAILED and ErrorNetworkFailed(HISPlayerErrorInfo errorInfo) event callback
    - It indicates if there is no Internet when starting the application     
- [**Improvement**] Optimized HISPlayer Settings
    - A warning message will be displayed in case a field required by HISPlayer SDK is missing

### Version 3.3.0
##### January 25, 2024
- [**Added**] New API to change video content using the URL string as a parameter:
    - **ChangeVideoContent(int playerIndex, string url)**
- [**Improvement**] Optimized error logs

### Version 3.2.0
##### December 7, 2023
- [**Added**] AutoTransition and LoopPlayback APIs
- [**Added**] Unity 2023 support

### Version 3.1.1
##### November 23, 2023
- [**Improvement**] Improvement of software robustness

### Version 3.1.0
##### October 11, 2023
- [**Improvement**] Improvement of software robustness

### Version 3.0.0 (Multiplatform SDK)
##### September 5, 2023
The macOS SDK is moved to multiplatform HISPlayerSDK (Android, iOS, macOS, WebGL, Windows)

Starting from version 3.0.0, the macOS SDK is part of multiplatform SDK

### Version 1.2.0
##### August 21, 2023
- [**Added**] License key input field.

### Version 1.1.0
##### August 8, 2023
- [**Added**] Playback Speed Controller. Values must be greater than 0 and less than or equal to 8.
    - void SetPlaybackSpeedRate(int playerIndex, float speed)
    - float GetPlaybackSpeedRate(int playerIndex)

### Version 1.0.0
##### May 12, 2023
- [**Added**] Initial release of HISPlayer MacOS SDK for Unity.
