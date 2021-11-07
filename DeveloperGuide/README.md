# Developer Guide, Hello World
This guide is intended for unity developers who want to use STT & TTS on Android & iOS.
There are 2 way to use STTS Unity Plugin. First is making code use our API. Second is using C# Script which already made.

## Using 'STTSProvider' Component
You can easily use STT & TTS on Unity using **STTSProvider** Component in your Unity Project.


## Using API - C# Code Level
### Creating STTS Instance
Do not instantiate this class directly, Instead, call **STTSFactory** class's **GetInstance()** function
```
using STTSCore.Engine;
using STTSCore.Utility;

STTS stts = STTSFactory.GetInstance();
```

### Init the STTS
Initializes the STTS Instance by providing language setting & GameObject Name
```
stts.init(STTSLangTypes.KO, gameObject.name);
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

// STT Result Event - iOS
public void EventNotify(string result)
{
    Debug.Log("[EventNotify] Result: " + result);
    if (result != null)
        // Do what do you want. the result parameter is the result of STT
}
```

- Android
```
// for aos
stts.SetResultCallback("STTListener");

// STT Result Event - Android
void STTListener(string result)
{
    Debug.Log("[STT] Result: " + result);
    if (result != null)
        // Do what do you want. the result parameter is the result of STT
}
```

In Android, you should use **SetResultCallback** method and input the Callback Method Name. 

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