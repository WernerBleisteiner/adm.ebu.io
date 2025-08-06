# audioFormatExtended

## Description

AudioFormatExtended is the parent element, containing all the ADM elements.

## Example

```xml
<audioFormatExtended version=”ITU-R_BS.2076-1”>
  ...
</audioFormatExtended>
```

## Attributes

| Attribute  | Description                 | Example  | Required |
|------------|-----------------------------|----------|----------|
| version    | ADM version name | “ITU-R_BS.2076-1” | Optional |


## Sub-elements

| Element | Description |
|---------|-------------|
| [audioProgramme](audio_programme.md) | Description of the whole audio programme. |
| [audioContent](audio_content.md) | Description of the content of some audio within the programme. |
| [audioObject](audio_object.md) | The link between the actual audio tracks and their format. |
| [audioPackFormat](audio_pack_format.md) | A description of a pack of channels that relate together. |
| [audioChannelFormat](audio_channel_format.md) | A description of an audio channel. |
| [audioStreamFormat](audio_stream_format.md) | A description of an audio stream. |
| [audioTrackFormat](audio_track_format.md) | A description of an audio track. |
| [audioTrackUID](audio_track_uid.md) | The unique identifier for an actual audio track. |
