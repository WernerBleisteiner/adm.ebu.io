# loudnessMetadata

These elements describe the measured loudness of the programme or content.

## Example

```xml
<loudnessMetadata loudnessMethod="ITU-R BS.1770" loudnessRecType="EBU R128" loudnessCorrectionType="file">
  <integratedLoudness>-24.0</integratedLoudness>
  <loudnessRange>12.5</loudnessRange>
  <maxTruePeak>-5.2</maxTruePeak>
  <maxMomentary>-9.9</maxMomentary>
  <maxShortTerm>-18.3</maxShortTerm>
</loudnessMetadata>
```

## Elements

The `loudnessMetata` element contains these sub-elements and attributes:

| Sub-element | Description | Type | Quantity |
| ----------- | ----------- | ---- | -------- |
| integratedLoudness | Integrated loudness value | float | 0 or 1 |
| loudnessRange | Loudness range | float | 0 or 1 |
| maxTruePeak | Maximum true-peak | float | 0 or 1 |
| maxMomentary | Maximum momentary loudness | float | 0 or 1 |
| maxShortTerm | Maximum short-term loudness | float | 0 or 1 |
| dialogLoudness | Loudness of the average dialogue | float | 0 or 1 |

| Attribute | Description | Type | Required |
| --------- | ----------- | ---- | -------- |
| loudnessMethod | The method or algorithm used to calculate the loudness. | string | No |  |
| loudnessRecType | The RecType indicates which regional recommended practice was followed in the loudness correction of the audio. | string | No |
| loudnessCorrectionType | The correction type is used to indicate what correction the audio, for example, file-based or real-time. | string | No |
