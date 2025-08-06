# audioChannelFormat - DirectSpeakers

## Description

An `audioChannelFormat` represents a single sequence of audio samples on which some action may be performed, such as movement of an object, which is rendered in a scene. It contains one or more [`audioBlockFormat`](#audioblockformat)s, which sub-divide it in the time domain.

The [`typeDefinition`](type_definitions.md) described here is for the 'DirectSpeakers' type, which is used for traditional channel-based audio. Many `audioChannelFormat` definitions with the 'DirectSpeakers' type are already defined in the [_Common Definitions_](../../tutorial/common_definitions.md), so they do not need to be defined explicitly when generating ADM metadata.

The other types of `audioChannelFormat`s are:

* [Matrix](audio_channel_format_matrix.md)
* [Objects](audio_channel_format_objects.md)
* [HOA](audio_channel_format_hoa.md)
* [Binaural](audio_channel_format_binaural.md)

## Example

```xml
<audioChannelFormat audioChannelFormatID="AC_00010001"
                    audioChannelFormatName="FrontLeft"
                    typeLabel="0001" typeDefinition="DirectSpeakers">
  <audioBlockFormat audioBlockFormatID="AB_00010001_00000001">
    <speakerLabel>urn:itu:bs:2051:0:speaker:M+030</speakerLabel>
    <position coordinate="azimuth">30.0</position>
    <position coordinate="elevation">0.0</position>
    <position coordinate="distance">1.0</position>
  </audioBlockFormat>
</audioChannelFormat>
```

## Attributes

The common [`audioChannelFormat` attributes](audio_channel_format.md#common-attributes) are used for the [`typeDefinition`](type_definitions.md) 'DirectSpeakers'.

## Sub-elements

The common [`audioChannelFormat` sub-elements](audio_channel_format.md#common-sub-elements) are used for the [`typeDefinition`](type_definitions.md) 'DirectSpeakers'.

## audioBlockFormat

In addition to the common [`audioBlockFormat` attributes](audio_channel_format.md#audioblockformat) the following sub-elements are defined for the `audioBlockFormat` with [`typeDefinition`](type_definitions.md) 'DirectSpeakers'.

### Sub-elements

#### Polar coordinates

| Element	| Attributes | Description	   | Units       | Example | Quantity |
|---------|------------|-----------------|-------------|---------|----------|
| speakerLabel | | A reference to the label of the speaker position |	–	| M-30 | 0...* |
| position | coordinate=“azimuth” | Exact azimuth location of sound | Degrees | −30.0 | 1 |
| position | coordinate=“azimuth”<br/>bound="max"	| Max. azimuth location of sound | Degrees | −22.5 | 0 or 1 |
| position | coordinate=“azimuth”<br/>bound="min"	| Min. azimuth location of sound | Degrees | −30.0 | 0 or 1 |
| position | coordinate=“elevation”	| Exact elevation location of sound | Degrees | 0.0 | 1 |
| position | coordinate=“elevation”<br/>bound="max" | Max. elevation location of sound | Degrees | 5.0 | 0 or 1 |
| position | coordinate=“elevation”<br/>bound="min" | Min. elevation location of sound | Degrees | -5.0 | 0 or 1 |
| position | coordinate=“distance” | Exact normalised distance from origin | Normalised to 1 | 1.0 | 0 or 1 |
| position | coordinate=“distance”<br/>bound="max" | Max. normalised distance from origin | Normalised to 1 | 1.0 | 0 or 1 |
| position | coordinate=“distance”<br/>bound="min" | Min. normalised distance from origin | Normalised to 1 | 0.8 | 0 or 1 |

The distance measure is normalised, as absolute speaker distances from the origin are rarely used, but an absolute reference distance is available in `audioPackFormat`.

#### Cartesian coordinates

The coordinates are usually based on the polar system, as this is the common way of describing channel and speaker locations. However it is also possible to use the Cartesian coordinate system by using different coordinate attributes (‘X’, ‘Y’ and ‘Z’).

| Element	| Attributes | Description	   | Units       | Example | Quantity |
|---------|------------|-----------------|-------------|---------|----------|
| speakerLabel | | A reference to the label of the speaker position |	–	| M-30 | 0...* |
| position | coordinate=“X”| Exact X left to right location of sound | Normalised Units | -0.2 | 1 |
| position | coordinate=“X”<br/>bound="max" |	Max. X left to right location of sound | Normalised Units | -0.1 | 0 or 1 |
| position | coordinate=“X”<br/>bound="min"	| Min. X left to right location of sound | Normalised Units | -0.3 | 0 or 1 |
| position | coordinate=“Y”| Exact Y front to back location of sound | Normalised Units | 0.1 | 1 |
| position | coordinate=“Y”<br/>bound="max" | Max. Y front to back location of sound | Normalised Units | 0.2 | 0 or 1 |
| position | coordinate=“Y”<br/>bound="min" | Min. Y front to back location of sound | Normalised Units | 0.0 | 0 or 1 |
| position | coordinate=“Z”| Exact Z top to bottom location of sound | Normalised Units | -0.5 | 1 |
| position | coordinate=“Z”<br/>bound="max" | Max. Z top to bottom location of sound | Normalised Units | -0.4 | 0 or 1 |
| position | coordinate=“Z”<br/>bound="min" | Min. Z top to bottom location of sound | Normalised Units | -0.6 | 0 or 1 |
| position | [screenEdgeLock](#screenedgelock-attribute) | Defines a speaker position at a screen edge	| left, right, top, bottom | left	| 0 … 2 |

#### screenEdgeLock attribute

The `screenEdgeLock` attribute allows a speaker to be positioned on the edge of the screen. The attribute can be used in combination with the coordinate=“elevation” and/or the coordinate=“azimuth” attribute and it is set to a string stating at which edge of the screen to the speaker position should be assumed to be (if screen-size information is available), so it is either “left”, “right”, “top”, “bottom”. The coordinate attribute must still be included so it is clear which dimension is being set, and to provide an alternative position should the screen not exist or no screen-size information be available.

The example XML code below illustrates how a speaker positioned on the right edge of the screen can be defined (with an alternative position of −29.0 degrees should the screen not exist).

```xml
<audioBlockFormat ...>
  <speakerLabel>M-SC</speakerLabel>
  <position coordinate="azimuth" screenEdgeLock=”right”>-29.0</position>
  <position coordinate="elevation">0.0</position>
  <position coordinate="distance">1.0</position>
</audioBlockFormat>
```

If two `screenEdgeLock` positions are required (for corners of the screen) then the two position ADM elements must be used as shown in the example below. This is because XML does not allow multiple attributes of the same name within the same element.

```xml
  <position coordinate="azimuth" screenEdgeLock=”right”>-29.0</position>
  <position coordinate="elevation" screenEdgeLock=”top”>15.0</position>
```
