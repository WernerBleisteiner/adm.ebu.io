# typeDefinitions for audio types

## Description

In `audioPackFormat` and `audioChannelFormat` the type of audio needs to be defined. Currently there are five types of audio: DirectSpeakers, Matrix, Objects, HOA and Binaural. The types are defined by two attributes: `typeDefinition`, which is a human-readable name, and `typeLabel`, which is a numerical label for the type. The table below describes each of the five types.

| typeDefinition | typeLabel | Description |
|----------------|-----------|-------------|
| DirectSpeakers | 0001	     | For channel-based audio, where each channel feeds a speaker directly |
| Matrix	       | 0002	     | For channel-based audio where channels are matrixed together, such as Mid-Side, Lt/Rt |
| Objects	       | 0003	     | For object-based audio where channels represent audio objects (or parts of objects), so include positional information |
| HOA	           | 0004	     | For scene-based audio where Ambisonics and HOA are used |
| Binaural	     | 0005	     | For binaural audio, where playback is over headphones |

It is not necessary to include both `typeDefinition` and `typeLabel` attributes in an `audioPackFormat` and `audioChannelFormat` definition, but at least one of them must be present.

## Example

This is how typeLabel and typeDefintion can be used in an audioPackFormat:

```xml
<audioPackFormat audioPackFormatID="AP_00031002"
                 audioPackFormatName="PackObj2"
                 typeLabel="0003" typeDefinition="Objects" importance="7">
  <audioChannelFormatIDRef>AC_00031003</audioChannelFormatIDRef>
</audioPackFormat>
```
