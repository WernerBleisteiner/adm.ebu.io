# audioProgramme

## Description

The `audioProgramme` is the top level element in the ADM structure. An `audioProgramme` represents an entire programme, or a version of a programme. A file can contain more than one `audioProgramme`, though it is recommended that they are all different versions of the same programme (e.g. different language versions), rather than completely different programmes.

An `audioProgramme` element references one or more [`audioContent`](audio_content.md) elements that are combined to create a full programme. It contains start and end times for the programme, which can be used for alignment with video times. Loudness metadata is also included to allow the programme’s loudness to be recorded. There is also provision to include information about the dimensions of the screen used in production, should it be required (obviously not for audio only productions).

When more than one `audioProgramme` is included in a file, and there is no other information to decide which one to choose for playback, then the default `audioProgramme` is the one with the lowest ID value.

## Example

In the example below, the programme called "Documentary" is set with a start time of 00:10:00.00000 and an end time of 00:40:00.00000. It contains three [`audioContent`](audio_content.md) sub-elements, loudness and reference screen metadata.

```xml
<audioProgramme audioProgrammeID="APR_1001"
                audioProgrammeName="Documentary"
                start="00:10:00.00000" end="00:40:00.00000">
  <audioContentIDRef>ACO_1001</audioContentIDRef>
  <audioContentIDRef>ACO_1002</audioContentIDRef>
  <audioContentIDRef>ACO_1003</audioContentIDRef>
  <loudnessMetadata>
     <integratedLoudness>-23.0</integratedLoudness>
   </loudnessMetadata>
   <audioProgrammeReferenceScreen>
     <aspectRatio>1.778</aspectRatio>
     <screenCentrePosition X="0.0" Y="1.0" Z="0.2"/>
     <screenWidth X="0.3"/>
   </audioProgrammeReferenceScreen>
</audioProgramme>
```

## Attributes

| Attribute              | Description                 | Example        | Required |
|------------------------|-----------------------------|----------------|----------|
| audioProgrammeId       | ID of the programme         | APR_1001       | Yes      |
| audioProgrammeName     | Name of the programme       | My Programme   | Yes      |
| audioProgrammeLanguage | Language of the programme   | en             | Optional |
| start                  | Start time of the programme | 00:10:00.00000 | Optional |
| end                    | End time of the programme   | 00:11:00.00000 | Optional |
| maxDuckingDepth        | Maximum of allowed ducking  |                | Optional |

## Sub-elements

| Sub-element                   | Description                                              | Example  | Quantity |
|-------------------------------|----------------------------------------------------------|----------|----------|
| audioContentIDRef             | Reference(s) to audioContent(s)                          | ACO_1001 | 1...*    |
| [loudnessMetadata](loudness_metadata.md)   | Measured loudness of the programme                       |          | 0 or 1   |
| [audioProgrammeReferenceScreen](#audioprogrammereferencescreen) | Specification of a reference/production/monitoring screen size for the audioProgramme. If the reference screen-size is not given, a default screen-size is implicitly defined. |          | 0 or 1   |

### audioProgrammeReferenceScreen

| Element | Description | Type | Quantity |
| ------- | ----------- | ---- | -------- |
| aspectRatio | Aspect radio of reference screen | float | 0 or 1 |
| [screenCentrePosition](#screencentreposition) | Position of the centre of the screen | screenCentrePositionType | 0 or 1 |
| [screenWidth](#screenwidth) | Width of the screen | screenWidthType | 0 or 1 |


### screenCentrePosition

| Attribute | Description | Type | Required |
| --------- | ----------- | ---- | -------- |
| azimuth | Azimuth of the centre of the screen | float | No |
| elevation | Elevation of the centre of the screen | float | No |
| distance | Distance of the centre of the screen | float | No |
| X | X position of the centre of the screen | float | No |
| Y | Y position of the centre of the screen | float | No |
| Z | Z position of the centre of the screen | float | No |


### screenWidth

| Attribute | Description |Type | Required |
| --------- | ----------- |---- | -------- |
| azimuth | Azimuth measure of screen width | float | No |
| X | X measure of screen width | float | No |
