# Content part

The ADM can be divided in the content and the format part. The [format part](format_part.md) can
exist without the content part, but not the other way around. Here we'll go through the content part with some simple examples.

## Single Programme

In many situations the ADM file you'll be generating will be for a single programme. A programme is the top level of the ADM, and the [`audioProgramme`](../reference/adm_elements/audio_programme.md) element is used to describe it. As with the other ADM main elements, we can give the `audioProgramme` a name, an ID, some time-related information and some other useful parameters. But lets start with the most basic settings, with name and ID set (both are mandatory):

```
<audioProgramme audioProgrammeName="Documentary"
                audioProgrammeID="APR_1001">
</audioProgramme>
```

This doesn't really tell us much, but it provides an entry point into the ADM, from which further things can be referenced. What we can add at this stage is the `start` and `duration` of the programme, so let's make it 30 minutes long:

```
<audioProgramme audioProgrammeName="Documentary"
                audioProgrammeID="APR_1001"
                start="00:00:00.00000" duration="00:30:00.00000">
</audioProgramme>
```
## Describing the Content

So, what have we got in our programme? In this example, we've got some narration, sound effects and background music. These are not described in the `audioProgramme`, but in the next element: [`audioContent`](../reference/adm_elements/audio_content.md).

For example, we can generate three `audioContent` elements, and give them some suitable names and IDs. Another thing we can add to each of these three elements is some information about whether the audio is dialogue or not:

```
<audioContent audioContentName="Narration"
              audioContentID="ACO_1001">
  <dialogue dialogueContentKind="1">1</dialogue>
</audioContent>
<audioContent audioContentName="SoundFX"
              audioContentID="ACO_1002">
  <dialogue nonDialogueContentKind="2">0</dialogue>
</audioContent>
<audioContent audioContentName="BgMusic"
              audioContentID="ACO_1003">
  <dialogue nonDialogueContentKind="1">0</dialogue>
</audioContent>
```

Now that we've defined these three `audioContent` elements, we need the `audioProgramme` element to be able to see them. This is done by adding some ID references to the `audioProgramme` element:

```
<audioProgramme audioProgrammeName="Documentary"
                audioProgrammeID="APR_1001"
                start="00:00:00.00000" duration="00:30:00.00000">
  <audioContentIDRef>ACO_1001</audioContentIDRef>
  <audioContentIDRef>ACO_1002</audioContentIDRef>
  <audioContentIDRef>ACO_1003</audioContentIDRef>
</audioProgramme>
```

So our elements are now structured like this:

![Programme and Contents](img/prog_cont.png)

## Connecting the Content Description to the Audio

We've now got three `audioContent` elements that each describe part of our programme, but these content descriptions need some actual audio connected to them. This is where the ['audioObject'](../reference/adm_elements/audio_object.md) element comes in. This element references audio tracks and the format description for those tracks, and can be referenced from the `audioContent` element.

Let's make some `audioObject` element for our example, we'll generate three of them, one for each `audioContent` element:

```
<audioObject audioObjectName="Narration"
             audioObjectID="AO_1001">
  <audioPackFormatIDRef>AP_00031001</audioPackFormatIDRef>
  <audioTrackUIDRef>ATU_00000001</audioTrackUIDRef>
</audioObject>
<audioObject audioObjectName="SoundFX"
             audioObjectID="AO_1002">
  <audioPackFormatIDRef>AP_00010003</audioPackFormatIDRef>
  <audioTrackUIDRef>ATU_00000002</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000003</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000004</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000005</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000006</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000007</audioTrackUIDRef>
</audioObject>
<audioObject audioObjectName="BgMusic"
             audioObjectID="AO_1003">
  <audioPackFormatIDRef>AP_00010002</audioPackFormatIDRef>
  <audioTrackUIDRef>ATU_00000008</audioTrackUIDRef>
  <audioTrackUIDRef>ATU_00000009</audioTrackUIDRef>
</audioObject>
```

In each object there is an `audioPackFormatIDRef` sub-element, and this is a reference to an [`audioPackFormat`](../reference/adm_elements/audio_pack_format.md) element that describes the format of the group of channels the audio has. There are also some `audioTrackUIDRef` sub-elements, and these are references to the actual track of audio. So for each of the three objects we have these references:

  * Narration (`AO_1001`)
    - Pack: `AP_00031001` - 'Object' type containing a single channel
    - Track UID: `ATU_00000001` - Single track
  * SoundFX (`AO_1002`)
    - Pack: `AP_00010003` - 'DirectSpeakers' type containing a 5.1 set of channels
    - Track UIDs: `ATU_00000002` to `ATU_00000007` - Six tracks
  * BgMusic (`AO_1003`)
    - Pack: `AP_00010002` - 'DirectSpeakers' type containing a stereo pair of channels
    - Track UIDs: `ATU_00000008` and `ATU_00000009` - Two tracks

We can now go back and connect our `audioContent` elements to the `audioObject` elements:

```
<audioContent audioContentName="Narration"
              audioContentID="ACO_1001">
  <dialogue dialogueContentKind="1">1</dialogue>
  <audioObjectIDRef>AO_1001</audioObjectIDRef>
</audioContent>
<audioContent audioContentName="SoundFX"
              audioContentID="ACO_1002">
  <dialogue nonDialogueContentKind="2">0</dialogue>
  <audioObjectIDRef>AO_1002</audioObjectIDRef>
</audioContent>
<audioContent audioContentName="BgMusic"
              audioContentID="ACO_1003">
  <dialogue nonDialogueContentKind="1">0</dialogue>
  <audioObjectIDRef>AO_1003</audioObjectIDRef>
</audioContent>
```

So, we have now generated a description of our content and connected to the format description via the `audioPackFormatIDRef` sub-elements within `audioObject`. The `audioObject` element also contains other parameters to allow setting of time restrictions (more can be read on the [Timing](timing.md) page), interactivity and mutual exclusivity.

Our elements are now structured like this:

![Programme, Contents and Objects](img/prog_cont_obj_chna.png)

You should have already seen the `audioPackFormat` elements in the [format part page](format_part.md), so you can now see how the format part connects with the content part.

## Track UIDs and Actual Audio Tracks

In the `audioObject` element you'll see the `audioTrackUIDRef` sub-elements, which reference [`audioTrackUID`](../reference/adm_elements/audio_track_uid.md) elements. The `audioTrackUID` element represents part of, or a complete, audio track in the file. In its simplest form it doesn't have to carry any other information, but it can include the sample-rate and bit-depth used if wanted.

In a BW64 the ['chna' chunk](../reference/excursions/chna_chunk.md) carries the relationship between `audioTrackUID`s and the actual tracks in the file like this:

| TrackNum | audioTrackUID | audioTrackFormatID | audioPackFormatID |
|----------|---------------|--------------------|-------------------|
| 1        | ATU_00000001  | AT_00031001_01     | AP_00031001       |
| 2        | ATU_00000002  | AT_00010001_01     | AP_00010003       |
| 3        | ATU_00000003  | AT_00010002_01     | AP_00010003       |
| 4        | ATU_00000004  | AT_00010003_01     | AP_00010003       |
| 5        | ATU_00000005  | AT_00010004_01     | AP_00010003       |
| 6        | ATU_00000006  | AT_00010005_01     | AP_00010003       |
| 7        | ATU_00000007  | AT_00010006_01     | AP_00010003       |
| 8        | ATU_00000008  | AT_00010001_01     | AP_00010002       |
| 9        | ATU_00000009  | AT_00010002_01     | AP_00010002       |

So, you can see how the 9 audio tracks in the file are each given an `audioTrackUID` ID, as well as `audioTrackFormatID` and `audioPackFormatID`s which describe the format of each tracks.

If you haven't already, you can read about the format part of the ADM [here](format_part.md).

The common definitions ensures that frequently used formats don't need to be redefined with each use, you can read more about this in the [next step](common_definitions.md).
