# Common Definitions

In the [format part](format_part.md) of the ADM, you saw how `audioPackFormat` and `audioChannelFormat` elements are used to describe a stereo pair of channels. If we had to define the elements for stereo every time we needed it the audio metadata, not only would it be pretty inefficient, it could be done in a variety of conflicting ways (e.g. different spelling of the element names). It therefore makes sense to have a set of definitions for commonly used formats. Thus, instead of including these explicitly in your file, they exist externally and your file only has to refer to them.

These common definitions are defined in [ITU-R Recommendation BS.2094](https://www.itu.int/rec/R-REC-BS.2094/en), which also includes an XML file with the common definitions within it. A wide range of the formats appear in the common definitions, both channel-based and HOA-based. The channel-based formats range from mono and stereo, all the way up to 22.2. The HOA-based formats include SN3D, N3D and FuMa up to high orders.

The elements covered by the common definitions are `audioPackFormat`, `audioChannelFormat`, `audioStreamFormat` and `audioTrackFormat`. The common definitions XML file is quite large, but here is an excerpt from it for 'stereo':

```
<audioPackFormat audioPackFormatID="AP_00010002"
                 audioPackFormatName="urn:itu:bs:2051:0:pack:stereo_(0+2+0)"
                 typeLabel="0001" typeDefinition="DirectSpeakers">
  <audioChannelFormatIDRef>AC_00010001</audioChannelFormatIDRef>
  <audioChannelFormatIDRef>AC_00010002</audioChannelFormatIDRef>
</audioPackFormat>

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
<audioChannelFormat audioChannelFormatID="AC_00010002"
                    audioChannelFormatName="FrontRight"
                    typeLabel="0001" typeDefinition="DirectSpeakers">
  <audioBlockFormat audioBlockFormatID="AB_00010002_00000001">
    <speakerLabel>urn:itu:bs:2051:0:speaker:M-030</speakerLabel>
    <position coordinate="azimuth">-30.0</position>
    <position coordinate="elevation">0.0</position>
    <position coordinate="distance">1.0</position>
  </audioBlockFormat>
</audioChannelFormat>

<audioStreamFormat audioStreamFormatID="AS_00010001"
                   audioStreamFormatName="PCM_FrontLeft"
                   formatLabel="0001" formatDefinition="PCM">
  <audioChannelFormatIDRef>AC_00010001</audioChannelFormatIDRef>
  <audioTrackFormatIDRef>AT_00010001_01</audioTrackFormatIDRef>
</audioStreamFormat>
<audioStreamFormat audioStreamFormatID="AS_00010002"
                   audioStreamFormatName="PCM_FrontRight"
                   formatLabel="0001" formatDefinition="PCM">
  <audioChannelFormatIDRef>AC_00010002</audioChannelFormatIDRef>
  <audioTrackFormatIDRef>AT_00010002_01</audioTrackFormatIDRef>
</audioStreamFormat>

<audioTrackFormat audioTrackFormatID="AT_00010001_01"
                  audioTrackFormatName="PCM_FrontLeft"
                  formatLabel="0001" formatDefinition="PCM">
  <audioStreamFormatIDRef>AS_00010001</audioStreamFormatIDRef>
</audioTrackFormat>
<audioTrackFormat audioTrackFormatID="AT_00010002_01"
                  audioTrackFormatName="PCM_FrontRight"
                  formatLabel="0001" formatDefinition="PCM">
  <audioStreamFormatIDRef>AS_00010002</audioStreamFormatIDRef>
</audioTrackFormat>
```

So, even for just stereo that's quite a lump of XML. By having this in a separate common definitions file, we don't need to include it in the XML in our audio file if we have stereo channels in it. This means a simple programme just containing a stereo pair of channels can be represented by the XML in this example:

```
<audioProgramme audioProgrammeName="SimpleProg"
                audioProgrammeID="APR_1001">
</audioProgramme>

<audioContent audioContentName="Music"
              audioContentID="ACO_1001">
  <audioObjectIDRef>AO_1001</audioObjectIDRef>
</audioContent>

<audioObject audioObjectName="Music"
             audioObjectID="AO_1001">
  <audioPackFormatIDRef>AP_00010002</audioPackFormatIDRef>
  <audioTrackUIDRef>ATU_00000001</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000002</audioTrackUIDRef>
</audioObject>
```

Here, the `audioObject` references `audioPackFormat` with the ID `AP_00010002`. As we know this is a common definition, then we don't need to include the `audioPackFormat`, `audioChannelFormat`, `audioStreamFormat` and `audioTrackFormat` elements for 'stereo' in our audio file.

Based on what has already been covered, we explore how timing parameters can be used to tailor duration of audio objects in the [next step](timing.md).
