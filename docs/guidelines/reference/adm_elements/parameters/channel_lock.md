# channelLock

The `channelLock` parameter appears in [`audioBlockFormat`](../audio_channel_format_objects.md#audioblockformat) only for the 'Objects' typeDefinition.

If the `channelLock` flag is set to 1 then the renderer will send the audio signal to the nearest (in terms of 3D position) channel or speaker position. A typical application for this is where the exact location of the object is not critical, but the need for un-processed reproduction of that signal takes priority.

The optional `maxDistance` attribute defines the radius r, 0 ≤ r ≤ 2, of a sphere around the object’s position. If one or more speakers exist in the defined sphere or on its surface, the object snaps to the nearest speaker. If `maxDistance` is undefined, a default value of infinity is assumed, meaning that the object should snap to the nearest of all speakers (unconditioned `channelLock`).


