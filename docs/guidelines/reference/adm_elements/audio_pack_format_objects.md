# audioPackFormat (Objects)

The `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'Objects' is used for object-based audio.

### Attributes

There are no additional attributes defined for the `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'Objects'. See [Common Attributes](audio_pack_format.md#common-attributes) for the list of common ones.

### Sub-elements

There are no additional sub-elements defined for the `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'Objects'. See [Common Sub-elements](audio_pack_format.md#common-sub-elements) for a list of the possible sub-elements. Even though it is defined as a common sub-element, the absoluteDistance sub-element is unlikely to be used in the 'Objects' mode.

### Example

```xml
<audioPackFormat audioPackFormatID="AP_00031002"
                 audioPackFormatName="PackObj2"
                 typeLabel="0003" typeDefinition="Objects" importance="7">
  <audioChannelFormatIDRef>AC_00031003</audioChannelFormatIDRef>
</audioPackFormat>
```
