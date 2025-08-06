# audioChannelFormat

## Description

An `audioChannelFormat` represents a single sequence of audio samples on which some action may be performed, such as movement of an object, which is rendered in a scene. It contains one or more [`audioBlockFormat`](#audioblockformat)s, which sub-divide it in the time domain. The [`typeDefinition/typeLabel`](type_definitions.md) is used to define the type of channel.

The types of `audioChannelFormat`s are:

* [DirectSpeakers](audio_channel_format_direct_speakers.md)
* [Matrix](audio_channel_format_matrix.md)
* [Objects](audio_channel_format_objects.md)
* [HOA](audio_channel_format_hoa.md)
* [Binaural](audio_channel_format_binaural.md)

## Common Attributes

| Attribute            | Description                 | Example  | Required |
|----------------------|-----------------------------|----------|----------|
| audioChannelFormatName | Name of the channel | FrontLeft | Yes |
| audioChannelFormatID | ID of the channel. The yyyy digits of AC_yyyyxxxx_represent the type of audio contained in the channel. The xxxx digits should match the audioStreamFormat xxxx digits. | AC_00010001 | Yes |
| typeLabel | Descriptor of the type of channel | 0001 | Optional |
| typeDefinition | Description of the type of channel | DirectSpeakers | Optional |


\*	At least one of `typeLabel` or `typeDefinition` is required.

The typeDefinition of the `audioChannelFormat` specifies the type of audio it is describing, and also determines which parameters are used within its `audioBlockFormat` children.

## Common Sub-elements

| Sub-element      | Description                                                | Attributes | Quantity |
|------------------|------------------------------------------------------------|------------|----------|
| audioBlockFormat | Time division of channel containing dynamic metadata  | |	1...* |
| frequency | Sets a high or low cut-off frequency for the audio in Hz | typeDefinition = “lowPass" or “highPass" |	0...2 |

## audioBlockFormat

An `audioBlockFormat` represents a single sequence of `audioChannelFormat` samples with fixed parameters, including position, within a specified time interval.

### Attributes

| Attribute	| Description |	Example	| Required | Default |
|-----------|-------------|---------|----------|---------|
| audioBlockFormatID | ID for block	| AB_00010001_00000001 | Yes |
| rtime	| Start [time](#time-format) of block (relative to the start time of the parent audioObject) | 00:00:00.00000 | Optional | 00:00:00.00000 |
| duration | Duration [time](#time-format) of block. | 00:00:10.00000 | Optional | unbounded duration |

The last 8 hexadecimal digits in the `audioBlockFormatID` contain the index for the block within the channel, starting at 00000001 for the first block.
If `rtime` is not used then the block starts at 00:00:00.00000. If `duration` is not used then the block lasts for the whole duration of the channel.
If there is only one `audioBlockFormat` within an `audioChannelFormat` it is assumed to be a ‘static’ object that lasts the duration of the channel, therefore `rtime` and `duration` should be omitted. When there is more than one `audioBlockFormat` within an `audioChannelFormat` it is assumed to be a ‘dynamic’ object, therefore both `rtime` and `duration` should be used.

#### Time Format

The time is shown in the format ‘hh:mm:ss.zzzzz’ which indicate hours, minutes, seconds and fractional seconds.

### Sub-elements

The sub-elements within `audioBlockFormat` depend upon the [`typeDefinition/typeLabel`](type_definitions.md) of the `audioChannelFormat`.
