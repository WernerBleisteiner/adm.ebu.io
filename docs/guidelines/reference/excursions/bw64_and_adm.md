# BW64 and ADM

While the ADM is designed to be a general model, its relationship with the BW64 file specified in [Recommendation ITU-R BS.2088](https://www.itu.int/rec/R-REC-BS.2088/en) is important to explain.

BW64 is the successor of RF64 specified in [EBU TECH 3306](https://tech.ebu.ch/publications/tech3306). So it already contains necessary  extensions to support files which are bigger than 4 GB. Apart from that an BW64 file is able to contain the ADM metadata and link it with the audio tracks in the file. To do that a BW64 specifies two new RIFF chunks – the 'axml' chunk and the 'chna' chunk.

## 'axml' Chunk Brief Description

The 'axml' chunk contains the ADM metadata in the XML file format.

## 'chna' Chunk Brief Description

A more detailed description of the <chna\> chunk can be found [here](chna_chunk.md).

The 'chna' (short for ‘channel allocation’) chunk contains a set of IDs for each track in the file to link them with the ADM metadata.

For each track in the chunk the following IDs are given:

 - `audioTrackFormatID` – the ID of the description of a particular audioTrackFormat element. As `audioTrackFormat` also refers to `audioStreamFormat` and either `audioPackFormat` or `audioChannelFormat`, this ID is enough to describe the format for a particular track.
 - `audioPackFormatID` – the ID of the description of a particular `audioPackFormat`. As most `audioChannelFormat`s need to be assigned to an `audioPackFormat` (e.g. ‘FrontLeft’ channel in ‘5.1’ pack), it must be specified in the \<chna\> chunk with this ID.
 - `audioTrackUID` – the unique ID that identifies the track. The content descriptor `audioObject` requires knowledge of which tracks in the file are being described, so contains a list of `audioTrackUID` references which correspond to audio tracks in the file.

The `audioPackFormatID` does not have to match the type audio the `audioTrackFormatID` in each track. A situation where they may differ is when an encoding matrix definition is being used, where the audioTrackFormatIDs will refer to the ‘DirectSpeakers’ input channels to the matrix, and the `audioPackFormatID` will refer to ‘Matrix’ type encoding matrix pack.

To enable tracks to contain more than one `audioTrackFormatID`, in order to allow different formats in the track at different times, the track number can be allocated multiple IDs. An example of such as allocation is below:

| Track No | audioTrackUID     | audioTrackFormatID    | audioPackFormatID    |
|----------|-------------------|-----------------------|----------------------|
| 1        | ATU_00000001      | AT_00010001_01        | AP_00010001          |
| 2        | ATU_00000002      | AT_00031001_01        | AP_00031001          |
| 2        | ATU_00000003      | AT_00031002_01        | AP_00031002          |

Here, track number two has two audioTrackUIDs as the `audioTrackFormat`s and `audioPackFormat`s assigned to it are used at different times in the file. The times of allocation would have to be found be inspecting the `audioObject` elements that cover those `audioTrackUID`s. An example of this is a programme where tracks 1 and 2 contain the theme tune which lasts for the first minute of the file. These tracks are free after this first minute, so some audio objects from the main body of the programme are stored in them subsequently. As the theme tune and the audio objects have completely different formats and contents they require different `audioTrackUID`s.
