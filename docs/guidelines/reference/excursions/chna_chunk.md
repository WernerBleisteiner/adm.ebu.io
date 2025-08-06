# CHNA Chunk

## Description

The <chna\> chunk is a chunk that is specifically defined for the use with ADM. The <chna\> chunk consists of a header followed by the number of tracks and number of track UIDs used. This is followed by an array of ID structures that each contains IDs corresponding to ADM element IDs.

The size of the chunk depends upon the number of track UIDs to be defined. The number of ID structures must be equal to or greater than the number of track UIDs used. By allowing the number of ID structures to exceed the number of UIDs, it can facilitate updating and adding new IDs to the chunk without having to change the size of the chunk. For example, it may not be clear how many UIDs will be generated at the beginning, so if the number of ID structures in the chunk is set to 64 (as this is considered by the implementer to be more than enough for their task); the software then generates 55 UIDs (an example number of initial UIDs) which fill up the first 55 ID structures, so the remaining 9 ID structures are set to zero values.

The ADM IDs within the chunk can either refer to ADM metadata carried in the <axml\> chunk, or in an external common definition file. If the last four hexadecimal digits of the IDs are value of 0x0FFF and below then they are defined as common definitions in [Recommendation ITU-R BS.2094](https://www.itu.int/rec/R-REC-BS.2094/en) (for example channel definitions for ‘FrontLeft’ and ‘FrontRight’). Any IDs with values of 0x1000 and above are defined as custom definitions, so will be contained in the <axml\> chunk within the file.

The _audioID_ structure contains an index to the track used in the <data\> chunk (which contains the audio samples), starting with the value of 1 for the first track. It contains a UID for the track, which the ADM metadata will contain. The audio elements of a track may be differently in the course of a file; in this case, there will be a different UID for each definition. Therefore it is possible to have multiple UIDs for each track. The other two values in the structure are references to the IDs of the ADM’s `audioTrackFormat` and `audioPackFormat` elements.

```c
struct chna_chunk
{
    CHAR    ckID[4];        // {'c','h','n','a'}
    DWORD   ckSize;         // size of the <chna> chunk
    WORD    numTracks;      // number of tracks used
    WORD    numUIDs;        // number of track UIDs used
    audioID ID[N];          // IDs for each track  (where N >= numUIDs)
};

struct audioID
{
    WORD    trackIndex;     // index of track in file
    CHAR    UID[12];        // audioTrackUID value
    CHAR    trackRef[14];   // audioTrackFormatID reference
    CHAR    packRef[11];    // audioPackFormatID reference
    CHAR    pad;            // padding byte to ensure even number of bytes
}
```

## Elements of the <chan\> Chunk

| Element | Description |
|---------|-------------|
| ckID | This is the 4 character array {‘c’,‘h‘,‘n‘,‘a‘}  for chunk identification. |
| ckSize | This is the size of the data section of the chunk in bytes. (It does not include the 8 bytes used by ckID and ckSize.) |
| numTracks | The number of tracks used in the file. Even if a track contains more than one set of IDs, it is still just one track. |
| numUIDs | The number of UIDs used in the file. As it is possible to give a single track multiple UIDs (covering different time periods), this could be a greater value than numTracks. This value should match the number of defined IDs in ID. |
| ID | The structure containing the set of audio reference IDs for the track. This array contains N IDs, where N >= numUIDs. When numUIDs is less than N the contents of the unused track IDs are set to zero. When reading the chunk the value of N can be derived from ckSize, as ckSize = 4 + (N * 40), so N = (ckSize – 4) / 40. |
| trackIndex | The index of the track in the file, starting at 1. This corresponds directly to the order of the tracks interlaced in the <data\> chunk. |
| UID | The `audioTrackUID` value of the track. The character array has the format ATU_xxxxxxxx where x is a hexadecimal digit. |
| trackRef | The `audioTrackFormatID` reference of the track. The character array has the format AT_xxxxxxxx_xx where x is a hexadecimal digit. |
| packRef | The `audioPackFormatID` reference of the track. The character array has the format AP_xxxxxxxx where x is a hexadecimal digit. When `audioPackFormatID` is not required (when `audioStreamFormat` is referring to an `audioPackFormat` rather than an `audioChannelFormat`) this field should be filled with null values. |
| pad | A single byte to ensure the _audioID_ structure has an even number of bytes. |

When an _ID_ is not being used the _trackIndex_ should be given the value of zero and the other fields should be given null strings that are the same length as the usual _ID_ string used. So the null string for _packRef_ would consist of 11 null characters (ASCII value zero) and _trackRef_ would consist of 14 null characters. 

## Examples

### Simple stereo file

The majority of audio files in existence are still 2-channel stereo files, with the first track containing the left channel, and the second track containing the right channel. The ADM has a definition of a left channel with an ID of AT_00010001_01, and the right channel with an ID of AT_00010002_01. The stereo pack definition has the _ID_ of AP_00010002.

The pseudo-code is shown below:
```c
ckID = {‘c’,’h’,’n’,’a’};
ckSize = 84;
numTracks = 2;
numUIDs = 2;
ID[0]={ trackIndex=1; UID=“ATU_00000001”; trackRef=“AT_00010001_01”; packRef=“AP_00010002”; pad=‘\0`; };
ID[1]={ trackIndex=2; UID=“ATU_00000002”; trackRef=“AT_00010002_01”; packRef=“AP_00010002”; pad=‘\0`; };
```

The number of ID structures is 2, so there are no unused ID structures in this example.

### Simple object-based example

Audio objects may only cover a sub-section of time in the audio file. To save space, non-overlapping objects may share the same track. This is where multiple UIDs in the same track would occur. This example also uses more _ID_ structures (32 in this case) than _numUIDs_ to show how unused _ID_ structures are set to zero. 

```c
ckID = {‘c’,’h’,’n’,’a’};
ckSize = 1284;
numTracks = 2;
numUIDs = 4;
ID[0]={ trackIndex=1; UID=“ATU_00000001”; trackRef=“AT_00031001_01”; packRef=“AP_00031001”; pad=‘\0`; };
ID[1]={ trackIndex=1; UID=“ATU_00000002”; trackRef=“AT_00031003_01”; packRef=“AP_00031002”; pad=‘\0`; };
ID[2]={ trackIndex=1; UID=“ATU_00000003”; trackRef=“AT_00031004_01”; packRef=“AP_00031003”; pad=‘\0`; };
ID[3]={ trackIndex=2; UID=“ATU_00000004”; trackRef=“AT_00031002_01”; packRef=“AP_00031001”; pad=‘\0`; };
ID[4]={ trackIndex=0; UID=[‘\0’]*12;      trackRef=[‘\0’]*14;        packRef=[‘\0’]*11;     pad=‘\0`; };
   :
ID[31]={ trackIndex=0; UID=[‘\0’]*12;      trackRef=[‘\0’]*14;        packRef=[‘\0’]*11;     pad=‘\0`; };
```

The first track contains 3 _UIDs_, so will contain 3 different objects (with the _trackRefs_ of AT_00031001_01, AT_00031003_01 and AT_00031004_01) at different time locations within the file. The second track contains one _UID_, so contains one object. This object has the same _packRef_ (AP_00031001) as the first object in track 1. This suggests the first object contains two channels carried in both track 1 and track 2. The ADM metadata carried in the <axml\> would be used to clarify the allocation of channels and tracks.

### Multi-content example

The BW64 file could contain multiple content in a single file, such as a main 5.1 mix on the first 6 tracks, with a foreign language stereo mix on the next 2 tracks. [Recommendation ITU-R BS.1738]((https://www.itu.int/rec/R-REC-BS.1738/en)) contains several configurations, and the example will show how Production Scenario 5 from that Recommendation can be dealt with in the <chna\> chunk. This scenario contains 8 tracks, the first 6 contain a 5.1 complete mix, and the second 2 tracks contain a stereo international mix. The resulting <chna\> is shown below:

```c
ckID = {‘c’,’h’,’n’,’a’};
ckSize = 324;
numTracks = 8;
numUIDs = 8;
ID[0]={ trackIndex=1; UID=“ATU_00000001”; trackRef=“AT_00010001_01”; packRef=“AP_00010003”; pad=‘\0`; };
ID[1]={ trackIndex=2; UID=“ATU_00000002”; trackRef=“AT_00010002_01”; packRef=“AP_00010003”; pad=‘\0`; };
ID[2]={ trackIndex=3; UID=“ATU_00000003”; trackRef=“AT_00010003_01”; packRef=“AP_00010003”; pad=‘\0`; };
ID[3]={ trackIndex=4; UID=“ATU_00000004”; trackRef=“AT_00010004_01”; packRef=“AP_00010003”; pad=‘\0`; };
ID[4]={ trackIndex=5; UID=“ATU_00000005”; trackRef=“AT_00010005_01”; packRef=“AP_00010003”; pad=‘\0`; };
ID[5]={ trackIndex=6; UID=“ATU_00000006”; trackRef=“AT_00010006_01”; packRef=“AP_00010003”; pad=‘\0`; };
ID[6]={ trackIndex=7; UID=“ATU_00000007”; trackRef=“AT_00010001_01”; packRef=“AP_00010002”; pad=‘\0`; };
ID[7]={ trackIndex=8; UID=“ATU_00000008”; trackRef=“AT_00010002_01”; packRef=“AP_00010002”; pad=‘\0`; };
```

The ADM metadata in the <axml\> chunk will contain information on how the two mixes are split.
