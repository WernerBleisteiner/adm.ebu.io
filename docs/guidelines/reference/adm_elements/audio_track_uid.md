# audioTrackUID

## Description

The `audioTrackUID` uniquely identifies a track or asset within a file or recording of an audio scene. This element contains information about the bit depth and sample rate of the track. It also contains sub-elements that allow the model to be used for non-BW64 applications by performing the job of the 'chna' chunk. When using the model with MXF files the `audioMXFLookUp` sub-element (which contains sub-elements to refer to the audio essences in the file) is used.

## Example

```xml
<audioTrackUID UID="ATU_00000001" sampleRate="48000" bitDepth="24">
  <audioTrackFormatIDRef>AT_00010001_01</audioTrackFormatIDRef>
  <audioPackFormatIDRef>AP_00010002</audioPackFormatIDRef>
</audioTrackUID>
```

## Attributes

| Attribute  | Description                 | Example      | Required |
|------------|-----------------------------|--------------|----------|
| UID        | The actual UID value        | ATU_00000001 | Yes      |
| sampleRate | Sample rate of track in Hz  | 48000        | Optional |
| bitDepth   | Bit depth of track in bit   | 24	          | Optional |

## Sub-elements

| Element               | Description                                                   | Example        | Quantity |
|-----------------------|---------------------------------------------------------------|----------------|----------|
| audioMXFLookUp        | See [audioMXFLookUp](#audiomxflookup_subelements) sub-section |                | 0 or 1   |
| audioTrackFormatIDRef | Reference to an audioTrackFormat description                  | AT_00010001_01 | 0 or 1   |
| audioPackFormatIDRef  | Reference to an audioPackFormat description                   | AP_00010002    | 0 or 1   |

### audioMXFLoopUp sub-elements

MXF has different meanings for the terms ‘track’ and ‘channel’ from their use in the ADM. In MXF ‘track’ is the storage medium containing audio or video, and for audio this ‘track’ can be sub-divided into ‘channels’.

| Element       | Description                      | Type   | Example                                                                                |
|---------------|----------------------------------|--------|----------------------------------------------------------------------------------------|
| packageUIDRef	| Reference to an MXF package	UMID | string |	urn:smpte:umid:060a2b34.01010105.01010f20.13000000.540bca53.41434f05.8ce5f4e3.5b72c985 |
| trackIDRef    | Reference to an MXF track        | int    | MXFTRACK_3                                                                             |
| channelIDRef  | Reference to a channel track     | int    | MXFCHAN_1                                                                              |
