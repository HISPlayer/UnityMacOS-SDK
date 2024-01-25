# HISPlayer Unity MacOS SDK Release Notes

### Version 3.3.0
##### January 25, 2024
- [**Added**] New API to change video content using the URL string as a paremeter:
    - **ChangeVideoContent(int playerIndex, string url)**
- [**Improvement**] Optimized error logs

### Version 3.2.0
##### December 7, 2023
- [**Added**] AutoTransition and LoopPlayback APIs
- [**Added**] Unity 2023 support

### Version 3.1.0
##### October 11, 2023
- [**Improvement**] Improvement of software robustness

### Version 3.0.0
##### September 5, 2023
The macOS SDK is moved to multiplatform HISPlayerSDK (Android, iOS, macOS, WebGL, Windows)

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
