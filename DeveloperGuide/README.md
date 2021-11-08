# Developer Guide, Hello World
This guide is intended for unity developers who want to use STT & TTS on Android & iOS.
There are 2 way to use STTS Unity Plugin. First is making code use our API. Second is using C# Script which already made.

## Using API - C# Code Level
You can easily learn to it from the STTSDemo Script File in DemoScene(Demo Scene location: Assets/STTS/Scenes/DemoScene)

### Creating STTS Instance
Do not instantiate this class directly, Instead, call **STTSFactory** class's **GetInstance()** function. and you should implement **STTSCallback** interface.
```
using STTSCore.Engine;
using STTSCore.Utility;

public class STTSDemo : MonoBehaviour, STTSCallback
{
    STTS stts = STTSFactory.GetInstance();
}
```

### Init the STTS
Initializes the STTS Instance by providing language setting & GameObject Name
```
stts.init(STTSLangTypes.EN_USA, gameObject.name);
```
Parameter
- 1st parameter(langType): The Language Setting
- 2nd parameter(gameObjName): The Unity GameObject with C# Component on it

### STT API
#### Register the Callback
Register the callback method that receives the result value. Registering the callback is the different on iOS & Android.
- iOS
```
// for ios
STTS.onEvent += EventNotify;
STTS.onErrorEvent += ErrorCallback;

// STT Result Event
public void EventNotify(string result)
{
    Debug.Log("[EventNotify] Result: " + result);
    if (result != null)
        // Do what do you want. the result parameter is the result of STT
}

// Error Event
public void ErrorCallback(string error)
{
    Debug.Log("[Exception] Error: " + error);
}
```

- Android
You should implement STTSCallback Function
```
// STT Result Event
public void STTResultCallback(string result)
{
    Debug.Log("[STT] Result: " + result);
    if (result != null)
        sttResultText.text = result;
}

// Error Event
public void ErrorCallback(string error)
{
    Debug.Log("[Exception] Error: " + error);
}
```

**Callback Method Must be in the Same Location as STTS Init Function**

#### Start STT
```
stts.StartSpeechToText();
```

#### Stop STT
```
stts.StopSpeechToText();
```

### TTS API
#### Start TTS
```
stts.StartTextToSpeech(STTSLangTypes.KO, ttsInputField.text, 0.4f, 0.5f);
```
- 1st parameter(langType): Set Language(English, Korean, ...)
- 2nd parameter(text): Text that device will speak
- 3rd parameter(speed): Audio Speed Value
- 4th parameter(pitch): Audio Pitch Value

### Release the STTS
```
stts.ReleaseSTTS();
```