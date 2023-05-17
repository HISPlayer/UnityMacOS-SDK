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
  * **public bool enableRendering**: Determines if the stream will be rendered or not. The value can change in every moment for toggling between render or non-render mode. If true, the player will be rendered. It can change in runtime.

* **public enum HISPlayerRenderMode**: Type of texture for rendering.
    * **RenderTexture**
    * **Material**
    * **RawImage**
    * **NONE**
  
* **public enum HISPlayerEvent**: The list of events provided by HISPlayer SDK. You can use the event using the virtual functions in the next section.
  * **HISPlayer_EVENT_PLAYBACK_PLAY**
  * **HISPlayer_EVENT_PLAYBACK_PAUSE**
  * **HISPlayer_EVENT_PLAYBACK_STOP**
  * **HISPlayer_EVENT_PLAYBACK_SEEK**
  * **HISPlayer_EVENT_PLAYBACK_READY**
  * **HISPlayer_EVENT_END_OF_CONTENT**
  * **HISPlayer_EVENT_PLAYBACK_BUFFERING**
  
* **public struct HISPlayerEventInfo**: The information of the triggered event.
  * **public HISPlayerEvent eventType**: The type of the event triggered.
  * **public int playerIndex**: The index of the player where the event is triggered.
  * **public float param1**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public float param2**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public float param3**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public float param4**: This will have different meanings depending on the event (see more information in [Functions](#Functions)). If there is no information about the parameter, it will have the default value -1.
  * **public string stringInfo**: Log information about the event.

## Functions
The following functions are provided by **HISPlayerManager**. They are **not public** so it’s necessary to create a custom script which inherits from **HISPlayerManager**.

### Virtual functions
These functions can be overridden.
#### protected virtual void Awake()
MonoBehaviour function which will be called from the beginning of the scene. It can be overridden but to make the system work it’s necessary to call base.Awake() into the overridden function.
 
#### protected virtual void EventPlaybackReady(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_PLAYBACK_READY is triggered.
This event occurs when the current playback of a stream is ready to be used.
Calling functions such as GetTracks before this event is triggered will provide null information.
 <table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>Number of tracks of the playback.</td>
  </tr>
</table>
 

#### protected virtual void EventPlaybackPlay(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_PLAYBACK_PLAY is triggered.
This event occurs whenever an internal playback has been played.
  <table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>param1</td>
    <td>PLAY = 1, PAUSE = 0.</td>
  </tr>
</table>

#### protected virtual void EventPlaybackPause(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_PLAYBACK_PAUSE is triggered.
This event occurs whenever an internal playback has been paused.

#### protected virtual void EventPlaybackStop(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_PLAYBACK_STOP is triggered.
This event occurs whenever an internal playback has been stopped.
 
#### protected virtual void EventPlaybackSeek(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_PLAYBACK_SEEK is triggered.
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

#### protected virtual void EventEndOfContent(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_END_OF_CONTENT is triggered.
This event occurs whenever an internal playlist reaches the end of the list.

#### protected virtual void EventPlaybackBuffering(HISPlayerEventInfo eventInfo)
Override this method to add custom logic when HISPlayerEvent.HISPlayer_EVENT_PLAYBACK_BUFFERING is triggered.
This event occurs whenever an internal playback is buffering.

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
#### protected void AddStream(StreamProperties newStream)
Add a new stream to the list **multiStreamProperties**. The stream must be added using this function instead of changing the list manually.
#### protected string GetPlayerDebugLog(int playerIndex)
Provides a log message obtained from a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.
#### protected long GetVideoPosition(int playerIndex)
Provides information about the timeline position in milliseconds, of the current video of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.
#### protected long GetVideoDuration(int playerIndex)
Provides information about the total duration in milliseconds, of the current video of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.
#### protected long GetVideoWidth(int playerIndex)
Provides information about the width of the current video of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.
#### protected long GetVideoHeight(int playerIndex)
Provides information about the height of the current video of a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list.
