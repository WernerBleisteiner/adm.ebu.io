# gain

The `gain` parameter appears in [`audioBlockFormat`](../audio_channel_format_objects.md#audioblockformat).

The `gain` parameter is a linear gain and controls the level of the audio signal in the object. At rendering the level of signal will be multiplied by the gain value. If the `gain` parameter is not set a value of 1.0 is assumed, so the audio signal’s level is not adjusted.

Ideally, the waveform that is being described should be at the desired level, so the `gain` parameter is not required (or set to 1.0), rather than relying on the `gain` parameter to adjust levels. 

When using the `gain` parameter in `audioBlockFormat` it can be used for fixed adjustments of the audio signal, and is useful when a single audio track is being used by more than one channel definition (for example, a single sound effect may be used by two different `audioChannelFormats`, but each requires different levels). 

