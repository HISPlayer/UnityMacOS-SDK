# HISPlayer API

## Public API

The following public APIs are provided by **HISPlayerManager**

* **public List < StreamProperties > multiStreamProperties**: List of properties for multi stream. However, currently HISPlayer MacOS SDK only supports single stream. Multi stream support will be added in the future. It starts with 0 elements. Adding more elements will be ignored until multi stream support is added.
* **public class StreamProperties**:
  * **public HISPlayerRenderMode renderMode**: Type of texture for rendering.
  * **public Material material**: Reference to the Unity Material.
  * **public RawImage rawImage**: Reference to the Unity Raw Image.
  * **public RenderTexture renderTexture**: Reference to the Unity Render Texture.
  * **public List<string> url**: List of the URLs for the stream.
  * **public bool autoPlay**: If true, the players will start playing automatically after set-up.
  * **public bool EnableRendering**: Determines if the stream will be rendered or not. The value can change in every moment for toggling between render or non-render mode. If true, the player will be rendered. It can change in runtime.

* **public enum HISPlayerRenderMode**: Type of texture for rendering.
    * **RenderTexture**
    * **Material**
    * **RawImage**
    * **NONE**
  
* **public enum HISPlayerEvent**: The list of events provided by HISPlayer SDK. You can use the event using the virtual functions in the next section.
  * **HISPLAYER_EVENT_PLAYBACK_READY**
  * **HISPLAYER_EVENT_PLAYBACK_PLAY**
  * **HISPLAYER_EVENT_PLAYBACK_PAUSE**
  * **HISPLAYER_EVENT_PLAYBACK_STOP**
  * **HISPLAYER_EVENT_PLAYBACK_SEEK**
  * **HISPLAYER_EVENT_PLAYBACK_BUFFERING**
  * **HISPLAYER_EVENT_VOLUME_CHANGE**
  * **HISPLAYER_EVENT_TEXT_RENDER**
  * **HISPLAYER_EVENT_END_OF_CONTENT**
  
* **public struct HISPlayerEventInfo**: The information of the triggered event.
  * **public HISPlayerEvent eventType**: The type of the event triggered.
  * **public int playerIndex**: The index of the player where the event is triggered.
  * **public float param1**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public float param2**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public float param3**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public float param4**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public string stringInfo**: Log information about the event.
 
* **public struct HISPlayerCaptionElement**: The information of the triggered event turns into caption’s format.
   * **public int playerIndex**: The index of the player where the event is triggered.
   * **public string caption**: The next generated caption text.

* **public struct HISPlayerTrack**:
   * **public string id**: Id of the track
   * **public int bitrate**: Bitrate of the track in bits per second.
   * **public int width**: Width of the track.
   * **public int height**: Height of the track.
   * **public int framerate**: Framerate of the track in frames per second.

* **public struct HISPlayerCaptionTrack**:
   * **public string id**: ID of the caption
   * **public string language**: Language of the caption

* **public struct HISPlayerAudioTrack**:
   * **public string id**: ID of the audio
   *  **public string language**: Language of the audio  

## Functions
The following functions are provided by **HISPlayerManager**. They are **not public** so it’s necessary to create a custom script which inherits from **HISPlayerManager**.

### Virtual functions
These functions can be overridden.
#### protected virtual void Awake()
MonoBehaviour function which will be called from the beginning of the scene. It can be overridden but to make the system work it’s necessary to call base.Awake() into the overridden function.
 
#### protected virtual void EventPlaybackReady(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_READY** is triggered.
This event occurs when the current playback of a stream is ready to be used.
Calling functions such as GetTracks before this event is triggered will provide null information.

#### protected virtual void EventPlaybackPlay(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_PLAY** is triggered.
This event occurs whenever an internal playback has been played.

#### protected virtual void EventPlaybackPause(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_PAUSE** is triggered.
This event occurs whenever an internal playback has been paused.

#### protected virtual void EventPlaybackStop(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_STOP** is triggered.
This event occurs whenever an internal playback has been stopped.
 
#### protected virtual void EventPlaybackSeek(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_SEEK** is triggered.
This event occurs whenever an internal playback has been sought to a new time position.
 
 <table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Value of the old track position in milliseconds.</td>
  </tr>
  <tr>
    <td>param2</td>
    <td>Value of the new track position in milliseconds.</td>
  </tr>
</table>

#### protected virtual void EventPlaybackBuffering(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_PLAYBACK_BUFFERING** is triggered.
This event occurs whenever an internal playback is buffering.

#### protected virtual void EventVolumeChange(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_VOLUME_CHANGE** is triggered.
This event occurs whenever the volume has been modified.

 <table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>New value for the volume.</td>
  </tr>
</table>

#### protected virtual void EventTextRender(HISPlayerCaptionElement subtitlesInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_TEXT_RENDER** is triggered.
This event occurs whenever a caption's text has been generated.

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>caption</td>
    <td>The next generated caption text.</td>
  </tr>
</table>

#### protected virtual void EventEndOfContent(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when **HISPlayerEvent.HISPLAYER_EVENT_END_OF_CONTENT** is triggered.
This event occurs whenever an internal playlist reaches the end of the list.

### Non-virtual functions
These functions can’t be overridden and they can be used only inside the inherited script. If it’s needed to use some of these functions into the Unity scene, for example with buttons, it is needed to create a public function which connects the button with the API.

#### protected void SetUpPlayer()
Initialize the player video stream system internally. It is necessary to use this function before anything else.

#### protected void Release()
Free all resources internally.

#### protected void Play(int playerIndex)
Play a certain stream giving a **playerIndex**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected void Pause(int playerIndex)
Pause a certain stream giving a **playerIndex**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected void Stop(int playerIndex)
Stop a certain stream giving a **playerIndex**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected void Seek(int playerIndex, long milliseconds)
Seek a certain stream to a certain time giving a **playerIndex** and the time of the track to be sought in **milliseconds**. The stream is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected void SetVolume(int playerIndex, float volume)
Modify the volume of a certain stream giving a **playerIndex**. The **volume** of the track value ranges between 0.0f and 1.0f. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected void AddVideoContent(int playerIndex, string url)
Add new content to a certain player given the url. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **url** is the link to the new video. Please, make sure the string is correct.

#### protected void ChangeVideoContent(int playerIndex, int urlIndex)
Change the video’s url  of a certain player. The next playback will start paused. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **urlIndex*** is associated with the index of the element in the list of urls.

#### protected void RemoveVideoContent(int playerIndex, int urlIndex)
Remove content from a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **urlIndex*** is associated with the index of the element in the list of urls.

#### protected long GetVideoPosition(int playerIndex)
Provides information about the timeline position in **milliseconds**, of **the current video** of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected long GetVideoDuration(int playerIndex)
Provides information about the total duration in **milliseconds**, of **the current video** of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected long GetVideoWidth(int playerIndex)
Provides information about the **width** of **the current video** of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected long GetVideoHeight(int playerIndex)
Provides information about the height of **the current video** of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected HISPlayerTrack[] GetTracks(int playerIndex)
Provides information about a track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected int GetTrackBitrate(int playerIndex, int trackIndex)
Get the bitrate of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected int GetTrackWidth(int playerIndex, int trackIndex)
Get the width of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected int GetTrackHeight(int playerIndex, int trackIndex)
Get the height of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected int GetTrackID(int playerIndex, int trackIndex)
Get the ID of a certain track of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### protected int GetTrackCount(int playerIndex)
Get the number of tracks of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public void SelectTrack(int playerIndex, int trackIndex)
Select a certain track of a certain stream to be used as the main track. The possible tracks can be obtained from the tracks returned from the method **GetTracks**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public void EnableCaptions(int playerIndex, bool enabled)
Enables the captions of the stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public HISPlayerCaptionTrack[] GetCaptionTrackList(int playerIndex)
Provide information about all the captions of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public int GetCaptionsCount(int playerIndex)
Obtain the number of captions of a  certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public string GetCaptionID(int playerIndex, int ccTrackIndex)
Obtain the ID of a certain caption of a certain player. The playerIndex is associated with the index of the element of Multi Stream Properties, e.g. the index 0 is the element 0 in the list.

#### public string GetCaptionLanguage(int playerIndex, int ccTrackIndex)
Obtain the language of a certain caption of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public void SelectCaptionTrack(int playerIndex, int ccTrackIndex)
Select a certain caption of a certain stream to be used. The possible caption tracks can be obtained from the tracks returned from the method **GetCaptionTrackList**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public HisPlayerAudioTrack[] GetAudioTrackList(int playerIndex)
Provide information about all the audio tracks of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public int GetAudioCount(int playerIndex)
Obtain the number of audio of a certain stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public string GetAudioID(int playerIndex, int audioTrackIndex)
Obtain the ID of a certain audio of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public string GetAudioLanguage(int playerIndex, int audioTrackIndex)
Obtain the language of a certain audio of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public void SelectAudioTrack(int playerIndex, int audioTrackIndex)
Select a certain audio-track of a certain stream to be used. The possible caption tracks can be obtained from the tracks returned from the method **GetAudioTrackList**. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public void SetMaxBitrate(int playerIndex, int bitrate)
Set a new maximum bitrate (in bits per second) of a specific track. The possible tracks can be obtained from the tracks returned from the method **GetTracks**. This action doesn't disable ABR. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public void SetPlaybackSpeedRate(int playerIndex, float speed)
Modify the **speed rate** of a certain stream giving a playerIndex. The value of the player's speed must be greater (>) than 0.0f and less than or equal (<=) to 8.0f. The default value of player's speed is 1.0f. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.

#### public float GetPlaybackSpeedRate(int playerIndex)
Obtain the **speed rate** of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.
