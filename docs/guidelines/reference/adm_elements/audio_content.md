# audioContent

## Description

An `audioContent` element describes the content of one component of a programme (e.g. background music), and references one or more [`audioObject`](audio_object.md) elements to tie the content to its format. This element includes loudness metadata.

## Example

```xml
<audioContent audioContentID="ACO_1001"
              audioContentName="Music"
              audioContentLanguage="en">
  <audioObjectIDRef>AO_1001</audioObjectIDRef>
  <audioObjectIDRef>AO_1002</audioObjectIDRef>
  <loudnessMetadata loudnessMethod="ITU-R BS.1770" loudnessRecType="EBU R128">
    <integratedLoudness>-23.0</integratedLoudness>
  </loudnessMetadata>
  <dialogue nonDialogueContentKind="2">0</dialogue>
</audioContent>
```

## Attributes

| Attribute            | Description                 | Example  | Required |
|----------------------|-----------------------------|----------|----------|
| audioContentId       | ID of the content           | ACO_1001 | Yes      |
| audioContentName     | Name of the content         | Music    | Yes      |
| audioContentLanguage | Language of the content     | en       | Optional |

## Sub-elements

| Sub-element      | Description                                                       | Example | Quantity |
|------------------|-------------------------------------------------------------------|---------|----------|
| audioObjectIDRef | Reference(s) to audioObject(s)                                    | AO_1001 | 1...*    |
| [loudnessMetadata](loudness_metadata.md) | Measured loudness of the content       |         | 0 or 1   |
| [dialogue](#dialogue) | Specifies the type of the content (non dialogue, dialogue, mixed) |    | 0 or 1   |

### dialogue

This optional sub-element specifies the kind of content that is included in the parent audioContent. The `dialogue` sub-element can take the values 0 (no dialogue), 1 (pure dialogue) or 2 (mixed). It has an attribute that specifies the type of content using defined lists (enumerators) of content kinds.
The attribute is dependent on the value of the `dialogue` sub-element.

| Value of dialogue	| Attribute |	Description	|
|---------------------|-----------|-------------|
| 0	| nonDialogueContentKind | ID of the contained content kind (enumerator, see specification below) |
| 1	| dialogueContentKind	| ID of the contained content kind (enumerator, see specification below) |
| 2	| mixedContentKind |ID of the contained content kind (enumerator, see specification below) |

#### Dialogue types
| nonDialogueContentKind | Description |
|------------------------|-------------|
| 0	                     | undefined   |
| 1	                     | music  |
| 2	                     | effect  |

| dialogueContentKind	   | Description  |
|------------------------|-------------|
| 0	                     | undefined  |
| 1	                     | (storyline) dialogue  |
| 2	                     | voiceover  |
| 3	                     | spoken subtitle  |
| 4	                     | audio description/visually impaired  |
| 5	                     | commentary  |
| 6	                     | emergency  |

| mixedContentKind 	     | Description  |
|------------------------|-------------|
| 0	                     | undefined  |
| 1	                     | complete main  |
| 2	                     | mixed  |
| 3	                     | hearing impaired  |
