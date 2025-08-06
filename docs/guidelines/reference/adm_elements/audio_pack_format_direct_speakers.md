# audioPackFormat (DirectSpeakers)

The `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'DirectSpeakers' is used for traditional channel-based audio. Many `audioPackFormat` definitions with the 'DirectSpeakers' type are already defined in the [_Common Definitions_](../../tutorial/common_definitions.md), so they do not need to be defined explicitly when generating ADM metadata.

## Attributes

There are no additional attributes defined for the `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'DirectSpeakers'. See [Common Attributes](audio_pack_format.md#common-attributes) for the list of common ones.

## Sub-elements

There are no additional sub-elements defined for the `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'DirectSpeakers'. See [Common Sub-elements](audio_pack_format.md#common-sub-elements) for a list of the possible sub-elements. Even though it is defined as a common sub-element, the absoluteDistance sub-element is unlikely to be used in the 'DirectSpeakers' mode.

## Example

```xml
<audioPackFormat audioPackFormatID="AP_00010002"
                 audioPackFormatName="urn:itu:bs:2051:0:pack:stereo_(0+2+0)"
                 typeLabel="0001" typeDefinition="DirectSpeakers">
  <audioChannelFormatIDRef>AC_00010001</audioChannelFormatIDRef>
  <audioChannelFormatIDRef>AC_00010002</audioChannelFormatIDRef>
</audioPackFormat>
```
