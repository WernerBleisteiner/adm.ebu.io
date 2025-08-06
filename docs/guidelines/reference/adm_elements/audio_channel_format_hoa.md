# audioChannelFormat - HOA

## Description

An `audioChannelFormat` represents a single sequence of audio samples on which some action may be performed, such as movement of an object, which is rendered in a scene. It is sub-divided in the time domain into one or more [`audioBlockFormat`](#audioblockformat)s.

In scene-based audio, a sound scene is represented by a set of coefficient signals. These coefficient signals are the linear weights of spatial orthogonal basis functions (such as spherical or circular harmonics functions). The scene can then be reproduced by rendering these coefficient signals to a target loudspeaker layout or headphones. The program production is decoupled from the reproduction and allows the creation of mixed program material while being agnostic to the number and position of the target loudspeakers. An example of scene-based audio is Higher-Order Ambisonics (HOA).

The [`typeDefinition`](type_definitions.md) described here is for the 'HOA' type, which is used for scene-based audio (such as Higher Order Ambisonics). Many `audioChannelFormat` definitions with the 'HOA' type are already defined in the [_Common Definitions_](../../tutorial/common_definitions.md), so they do not need to be defined explicitly when generating ADM metadata. Each component can be described by either a combination of degree, order values, and normalization, or an equation.

The other types of `audioChannelFormat`s are:

* [DirectSpeakers](audio_channel_format_direct_speakers.md)
* [Matrix](audio_channel_format_matrix.md)
* [Objects](audio_channel_format_objects.md)
* [Binaural](audio_channel_format_binaural.md)

When no equation is given, the HOA components are defined by the degree, order, and normalization values.
The equation field is for information only when present, and not intended to be parsed when degree, order, and normalization values are present. It is recommended that C-style mathematical notation be used for the equation element (e.g. ‘cos(A)*sin(E)’). Its purpose is to allow the description of customized or experimental HOA components that cannot be described by the order, degree, and normalization parameters alone.

## Example

```xml
<audioChannelFormat audioChannelFormatID="AC_00040003"
                    audioChannelFormatName="SN3D_ACN_2"
                    typeLabel="0004" typeDefinition="HOA">
  <audioBlockFormat audioBlockFormatID="AB_00040003_00000001">
    <degree>0</degree>
    <order>1</order>
    <normalization>SN3D</normalization>
  </audioBlockFormat>
</audioChannelFormat>
```

## Attributes

The common [`audioChannelFormat` attributes](audio_channel_format.md#common-attributes) are used for the [`typeDefinition`](type_definitions.md) 'HOA'.

## Sub-elements

The common [`audioChannelFormat` sub-elements](audio_channel_format.md#common-sub-elements) are used for the [`typeDefinition`](type_definitions.md) 'HOA'.

## audioBlockFormat

In addition to the common [`audioBlockFormat` attributes](audio_channel_format.md#audioblockformat) the following sub-elements are defined for the `audioBlockFormat` with [`typeDefinition`](type_definitions.md) 'HOA'.

### Sub-elements

| Element |	Description	| Example	| Quantity | Default | Required |
|---------|-------------|---------|----------|---------|----------|
| equation | An equation to describe the HOA component | cos(A)*sin(E) | 0 or 1 | - | Optional |
| order | Order of the HOA component | 1 | 0 or 1 | - | Yes |
| degree | Degree of the HOA component | −1 | 0 or 1 | - | Yes |
| normalization | Indicates the normalization scheme of the HOA component (N3D, SN3D, FuMa). | N3D | 0 or 1 | SN3D | Optional |
| nfcRefDist | Indicates the reference distance (in metres) of the loudspeaker setup for near-field compensation (NFC). If no nfcRefDist is defined or the value is 0, NFC is not necessary. | 2 | 0 or 1 | 0 | Optional |
| screenRef | Indicates whether the component is screen-related (flag is equal to 1) or not (flag is equal to 0) | 0 | 0 or 1 | 0 | Optional |
