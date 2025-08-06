# audioPackFormat (HOA)

The `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'HOA' is used for scene-based audio (such as Higher Order Ambisonics). Many `audioPackFormat` definitions with the 'HOA' type are already defined in the [_Common Definitions_](../../tutorial/common_definitions.md), so they do not need to be defined explicitly when generating ADM metadata.

It is common that a pack of HOA components/signals will share the same normalization, NFC compensation and/or screen-relation. However, when the parameters are specified within an `audioBlockFormat`, these values overwrite those given in the `audioPackFormat`.

## Attributes

There are no additional attributes defined for the `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'HOA'. See [Common Attributes](audio_pack_format.md#common-attributes) for the list of common ones.

## Sub-elements

In addition to the [common sub-elements](audio_pack_format.md#common-sub-elements) the following sub-elements are defined for the `audioPackFormat` with [`typeDefinition`](type_definitions.md) 'HOA'.

| Sub-element      | Description                                                       | Example | Quantity | Default |
|------------------|-------------------------------------------------------------------|---------|----------|---------|
| audioChannelFormatIDRef | Reference to an audioChannelFormat | AC_00040001 | 0...* | - |
| audioPackFormatIDRef | Reference to an audioPackFormat | AP_00040002 | 0...* | - |
| absoluteDistance | Absolute distance in metres | 4.5 | 0 or 1 | - |
| normalization | Indicates the normalization scheme of the HOA content (N3D, SN3D, FuMa). | N3D | 0 or 1 | SN3D |
| nfcRefDist | Indicates the reference distance (in metres) of the loudspeaker setup for near-field compensation (NFC). If no nfcRefDist is defined or the value is 0, NFC is not necessary. | 2	| 0 or 1 | 0 |
| screenRef | Indicates whether the content is screen-related (flag is equal to 1) or not (flag is equal to 0) | 0 | 0 or 1	| 0	|

## Example

```xml
<audioPackFormat audioPackFormatID="AP_00040001"
                 audioPackFormatName="3D_order1_SN3D_ACN"
                 typeLabel="0004" typeDefinition="HOA">
  <audioChannelFormatIDRef>AC_00040001</audioChannelFormatIDRef>
  <audioChannelFormatIDRef>AC_00040002</audioChannelFormatIDRef>
  <audioChannelFormatIDRef>AC_00040003</audioChannelFormatIDRef>
  <audioChannelFormatIDRef>AC_00040004</audioChannelFormatIDRef>
</audioPackFormat>
```
