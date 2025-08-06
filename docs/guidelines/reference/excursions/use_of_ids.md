# Use of IDs

The ID attributes in each of the elements have three main purposes:

- to provide a unique identification for each defined element,
- to allow the elements to reference each other,
- and to provide a logical numerical representation of the contents of the element.

The IDs for each element follows the following format:

| Element                                                       | ID format            |
|---------------------------------------------------------------|----------------------|
| [audioProgramme](../adm_elements/audio_programme.md)          | APR_wwww             |
| [audioContent](../adm_elements/audio_content.md)              | ACO_wwww             |
| [audioObject](../adm_elements/audio_object.md)                | AO_wwww              |
| [audioTrackUID](../adm_elements/audio_track_uid.md)           | ATU_zzzzzzzz         |
| [audioPackFormat](../adm_elements/audio_pack_format.md)       | AP_yyyyxxxx          |
| [audioChannelFormat](../adm_elements/audio_channel_format.md) | AC_yyyyxxxx          |
| [audioStreamFormat](../adm_elements/audio_stream_format.md)   | AS_yyyyxxxx          |
| [audioTrackFormat](../adm_elements/audio_track_format.md)     | AT_yyyyxxxx_zz       |

The yyyy part is a four digit hexadecimal number that represents the type of element it is, by using the typeLabel values. Currently there are 5 defined [type label values](../adm_elements/type_definitions.md) and the possibility to define user custom types.

The xxxx part is a four-digit hexadecimal number, which identifies the description within a particular type. Values in the range 0001-0FFF are reserved for common definition such as ‘FrontLeft’ or ‘Stereo’. Common definitions are specified in [Recommendation ITU-R BS.2094](https://www.itu.int/rec/R-REC-BS.2094/en). Values in the range 1000-FFFF are for custom definitions, which will be particularly used in object-based audio where all the objects will be custom definitions.

The `audioChannelFormatID` values in the range 0001-0FFF specify the channel with respect to the channel label and channel configuration. The set of defined common definitions for `audioChannelFormatID`s for typical speaker positions is found in [ITU-R BS.2094](https://www.itu.int/rec/R-REC-BS.2094/en). Some examples of these common definitions are shown below:

| ID of channel | Name of channel     | SpeakerLabel                    |
|---------------|---------------------|---------------------------------|
| AC_00010001   | FrontLeft           | urn:itu:bs:2051:0:speaker:M+030 |
| AC_00010002   | FrontRight          | urn:itu:bs:2051:0:speaker:M-030 |
| AC_00010003   | FrontCentre         | urn:itu:bs:2051:0:speaker:M+000 |
| AC_00010004   | LowFrequencyEffects | urn:itu:bs:2051:0:speaker:LFE   |
| AC_00010005   | SurroundLeft        | urn:itu:bs:2051:0:speaker:M+110 |
| AC_00010006   | SurroundRight       | urn:itu:bs:2051:0:speaker:M-110 |

The `audioPackFormatID` specifies the channel configuration. The set of defined common definitions for `audioPackFormatID`s for typical speaker configurations is found in [ITU-R BS.2094](https://www.itu.int/rec/R-REC-BS.2094/en). Some examples of the common definitions are shown below:

| ID of pack  | Name of pack   |
|-------------|----------------|
| AP_00010002 | Stereo_(0+2+0) |
| AP_00010003 | 5.1_(0+5+0)    |

The zzzzzzzz part of the `audioBlockFormatID` is an 8-digit hexadecimal number that acts as an index/counter for the blocks within the channel. This index should start at 1 for the first block. The yyyyxxxx values should match those of the parent `audioChannelFormat` ID.
The zz part of the `audioTrackFormatID` is a 2-digit hexadecimal number that acts as an index/counter for the tracks within the stream. The yyyyxxxx values should match those of the reference `audioStreamFormat` ID.

The `audioProgrammeID`, `audioContentID` and `audioObjectID` formats do not have a type and so have no yyyy values. Even though there is initially no intention to have common definitions for these elements the values for wwww will be in the hexadecimal range 1000-FFFF because they will always be custom values. However, keeping the common range of values (0000-0FFF) set aside for now may be useful in future; for example, EBU R 123 configurations may use them.

IDs with a zero value should not be used for any definitions, as they are reserved for elements that should be ignored and are undefined. For example, AT_00000000_00 is for an `audioTrackFormat` that has no definition and should be ignored. This can be useful for audio files that contain unused tracks (e.g. an 8-track file containing 5-channel audio), so the 'chna' chunk can reference AT_00000000_00 in the `audioTrackFormat` fields for those unused tracks.

Both upper and lower-case hex digits (a-f and A-F) must be supported when reading IDs. Therefore, IDs with the same digits, but with a different case are treated to be identical. For example, AC_0001000a and AC_0001000A are the same ID.
