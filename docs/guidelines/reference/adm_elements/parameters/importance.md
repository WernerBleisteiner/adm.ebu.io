# importance

The `importance` parameter appears in [`audioBlockFormat`](../audio_channel_format_objects.md#audioblockformat), [`audioPackFormat`](../audio_pack_format_objects.md) and [`audioObject`](../audio_object.md).

The `importance` parameter allows a processor to discard objects below a certain level of importance, with 10 being the most, and 0 the least. Varying this parameter over successive blocks should be avoided. This parameter is useful when the size of the ADM metadata needs to be reduced and allow prioritisation to be made on what compromises can be made.

When the `importance` parameter is used in `audioObject` it can be used to remove less important sounds when the number of objects or tracks are needed to be reduced. For example, some background sound effects can be discarded to ensure main dialogue objects are retained.

When the `importance` parameter is used in `audioPackFormat` it can be used to compromise on spatial audio quality. Nested `audioPackFormat`s can be be used to exploit this feature. For example, an audio object with a main direct sound (in a parent `audioPackFormat` with high importance) and additional reverb sounds (in a child `audioPackFormat` with low importance), could have the reverb sound discarded which retains the main sound, but compromises quality.

The `importance` parameter in `audioBlockFormat` can be used in a similar way to `audioPackFormat` to allow spatial quality to be compromised, but care must be taken that the sound is not adversely repositioned as a result of discarding channels.   

