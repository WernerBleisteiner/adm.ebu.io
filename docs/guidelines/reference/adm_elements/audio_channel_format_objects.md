# audioChannelFormat - Objects

## Description

An `audioChannelFormat` represents a single sequence of audio samples on which some action may be performed, such as movement of an object, which is rendered in a scene. It is sub-divided in the time domain into one or more [`audioBlockFormat`](#audioblockformat)s.

The [`typeDefinition`](type_definitions.md) described here is for the 'Objects' type, which is used for object-based audio where the position of the audio object may change dynamically. As well as the coordinates of the object, there are parameters for the object’s size, and whether it is a diffuse or coherent sound.

The other types of `audioChannelFormat`s are:

* [DirectSpeakers](audio_channel_format_direct_speakers.md)
* [Matrix](audio_channel_format_matrix.md)
* [HOA](audio_channel_format_hoa.md)
* [Binaural](audio_channel_format_binaural.md)

The `channelLock` parameter will inform a renderer to send the object’s audio to the nearest speaker or channel, rather than the usual panning, interpolation, etc. The `jumpPosition` parameter will ensure the renderer does not perform any temporal interpolation of the position values, so the object will jump in space rather than move smoothly to the next position.

The `position` elements use the `coordinate` attribute to specify which axis is used. The primary coordinate system is the Polar coordinate system, which uses azimuth, elevation and distance axes. However, it is possible to specify other axes for other coordinates such as X, Y and Z for the Cartesian coordinate system. This is described in more detail [here](../excursions/coordinate_system.md).


## Example

```xml
<audioChannelFormat audioChannelFormatID="AC_00031003"
                    audioChannelFormatName="Effect1"
                    typeLabel="0003" typeDefinition="Objects">
  <audioBlockFormat audioBlockFormatID="AB_00031003_00000001" rtime="00:00:00.00000" duration="00:00:02.00000">
    <position coordinate="X">0.8</position>
    <position coordinate="Y">-0.7</position>
    <position coordinate="Z">0.8</position>
    <cartesian>1</cartesian>
    <channelLock maxDistance="0.4">1</channelLock>
    <objectDivergence azimuthRange="20">0.4</objectDivergence>
    <jumpPosition interpolationLength="0.03">1</jumpPosition>
    <importance>3</importance>
    <zoneExclusion>
      <zone minX="-1.0" maxX="-0.7" minY="-1.0" maxY="1.0" minZ="-1.0" maxZ="1.0">LeftSide</zone>
      <zone minX="0.7" maxX="1.0" minY="-1.0" maxY="1.0" minZ="-1.0" maxZ="1.0">RightSide</zone>
    </zoneExclusion>
  </audioBlockFormat>
</audioChannelFormat>
```

## Attributes

The common [`audioChannelFormat` attributes](audio_channel_format.md#common-attributes) are used for the [`typeDefinition`](type_definitions.md) 'Objects'.

## Sub-elements

The common [`audioChannelFormat` sub-elements](audio_channel_format.md#common-sub-elements) are used for the [`typeDefinition`](type_definitions.md) 'Objects'.

## audioBlockFormat

In addition to the common [`audioBlockFormat` attributes](audio_channel_format.md#audioblockformat) the following sub-elements are defined for the `audioBlockFormat` with [`typeDefinition`](type_definitions.md) 'Objects'.

### Sub-elements

Some of the sub-elements depend upon whether polar or Cartesian coordinates are used, while some are common to both systems.

#### For polar coordinates

| Sub-element | Attribute              | Description                       | Units                        | Example | Quantity | Default |
|-------------|------------------------|-----------------------------------|------------------------------|---------|----------|---------|
| position    | coordinate=“azimuth”   | azimuth “theta” of sound location | Degrees (−180 ≤ theta ≤ 180) | −22.5   | 1        | –       |
| position    | coordinate=“elevation” | elevation “phi” of sound location | Degrees (−90 ≤ phi ≤ 90)     | 5.0     | 1        | –       |
| position    | coordinate=“distance”  | distance “r” from origin          | abs(r)                       | 0.9     | 0 or 1   | 1.0     |
| width       | –                      | horizontal extent                 | Degrees                      | 45      | 0 or 1   | 0.0     |
| height      | –                      | vertical extent                   | Degrees                      | 20      | 0 or 1   | 0.0     |
| depth       | –                      | distance extent                   | Ratio                        | 0.2     | 0 or 1   | 0.0     |

| Sub-element | objectDivergence                                                     |
|-------------|----------------------------------------------------------------------|
| Attribute   | azimuthRange                                                         |
| Description | Adjusts the balance between the object’s specified position and two other positions specified by the azimuthRange value (symmetrical on both sides of the object at the object’s position +/– azimuthRange). A value of 0 for the objectDivergence means no divergence. |
| Units       | 0 to 1.0 for objectDivergence, 0.0 to 180.0 (angle) for azimuthRange |
| Example     | 0.5 (objectDivergence), 60.0 (azimuthRange)                          |
| Quantity    | 0 or 1                                                               |
| Default     | 0.0 (objectDivergence), 45.0 (azimuthRange)                          |

| Sub-element | zoneExclusion                                                                 |
|-------------|-------------------------------------------------------------------------------|
| Description | Indicates which speaker/room zones the object should not be rendered through. |
| Sub-element | zone                                                                          |

| Sub-sub-element | zone _(Polar)_                                                                                                                                                     |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Attributes      | minElevation, maxElevation, minAzimuth, maxAzimuth                                                                                                                 |
| Description     | Specifies the circular projection onto the sphere for spherical coordinates. Multiple zone elements can be used to specify more complex exclusion shapes.          |
| Units           | -180 to 180 float for the spherical azimuth attribute and –90 to 90 float for the spherical elevation attribute. String for a label to describe the exclusion zone |
| Example         | maxElevation=30, minElevation=-30, minAzimuth=-30, maxAzimuth=30. “Centre front"                                                                                   |
| Quantity        | 1..*                                                                                                                                                               |

#### For Cartesian coordinates

| Sub-element | Attribute      | Description          | Units            | Example | Quantity | Default |
|-------------|----------------|----------------------|------------------|---------|----------|---------|
| position    | coordinate=“X” | left/right dimension | Normalized Units | −0.2    | 1        | -       |
| position    | coordinate=“Y” | back/front dimension | Normalized Units | 0.1     | 1        | -       |
| position    | coordinate=“Z” | bottom/top dimension | Normalized Units | −0.5    | 0 or 1   | 0.0     |
| width       | -              | X-width              | Normalized Units | 0.03    | 0 or 1   | 0.0     |
| depth       | -              | Y-width              | Normalized Units | 0.05    | 0 or 1   | 0.0     |
| height      | -              | Z-width              | Normalized Units | 0.07    | 0 or 1   | 0.0     |

| Sub-element | objectDivergence                                              |
|-------------|---------------------------------------------------------------|
| Attribute   | positionRange                                                 |
| Description | Adjusts the balance between the object’s specified position and two other positions specified by the positionRange value (symmetrical on both sides of the object at the object’s position +/– positionRange along the X-axis). A value of 0 for the objectDivergence means no divergence. |
| Units       | 0.0 to 1.0 for objectDivergence, 0.0 to 1.0 for positionRange |
| Example     | 0.5 (objectDivergence), 0.25 (positionRange)                  |
| Quantity    | 0 or 1                                                        |
| Default     | 0.0 (objectDivergence), 0.0 (positionRange)                   |

| Sub-element | zoneExclusion |
|-------------|-------------------------------------------------------------------------------|
| Description | Indicates which speaker/room zones the object should not be rendered through. |
| Sub-element | zone |

| Sub-sub-element | zone _(Cartesian)_                                                                                |
|-----------------|---------------------------------------------------------------------------------------------------|
| Attributes      | minX, maxX, minY, maxY, minZ, maxZ                                                                |
| Description     | Specifies the corner points of a cuboid in the 3D space that will be excluded from rendering for Cartesian coordinates. Multiple zone elements can be used to specify more complex exclusion shapes. |
| Units           | –1.0 to 1.0 float for each Cartesian attribute. String for a label to describe the exclusion zone |
| Example         | minX=–1.0, maxX=1.0, minY=–1.0, maxY=0.0, minZ=–1.0, maxZ=1.0, “Rear half”                        |
| Quantity        | 1..*                                                                                              |

#### For all coordinate systems

| Sub-element | cartesian                                                                                                                    |
|-------------|------------------------------------------------------------------------------------------------------------------------------|
| Description | Specifies coordinate system, if the flag is set to 1 the Cartesian coordinates and otherwise spherical coordinates are used. |
| Units       | 1/0 flag                                                                                                                     |
| Example     | 1                                                                                                                            |
| Quantity    | 0 or 1                                                                                                                       |
| Default     | 0                                                                                                                            |

| Sub-element | gain                                     |
|-------------|------------------------------------------|
| Description | Apply a gain to the audio in the object. |
| Units       | linear gain value                        |
| Example     | 0.5                                      |
| Quantity    | 0 or 1                                   |
| Default     | 1.0                                      |

| Sub-element | diffuse                                                                        |
|-------------|--------------------------------------------------------------------------------|
| Description | Describes the diffuseness of an audioObject (if it is diffuse or direct sound) |
| Units       | 1/0 flag                                                                       |
| Example     | 0.5                                                                            |
| Quantity    | 0 or 1                                                                         |
| Default     | 0                                                                              |

| Sub-element | channelLock                              |
|-------------|------------------------------------------|
| Attribute   | maxDistance                              |
| Description | If set to 1 a renderer can lock the object to the nearest channel or speaker, rather than normal rendering. The optional maxDistance attribute defines the radius of a sphere around the object’s position. If one or more speakers exist in the defined sphere or on its surface, the object snaps to the nearest speaker. If maxDistance is undefined, a default value of infinity is assumed, meaning that the object should snap to the nearest of all speakers (unconditioned channelLock). |
| Units       | 1/0 flag                                 |
| Example     | 1 (channel Lock), 0.1 (maxDistance)      |
| Quantity    | 0 or 1                                   |
| Default     | 0 (channel Lock), infinity (maxDistance) |


| Sub-element | jumpPosition                                                      |
|-------------|-------------------------------------------------------------------|
| Attribute   | interpolationLength                                               |
| Description | If jumpPosition is set to 1 the position will change instantly from the previous block’s position. If set to 0 then interpolation of the position will take the entire length of the block. If the interpolationLength attribute is used, and the jumpPosition value is 1, then the interpolation will take as long as the specified value. The interpolation length should be shorter or equal than the block’s duration. |
| Units       | 1/0 flag for jumpPosition, seconds (5d.p) for interpolationLength |
| Example     | 1 (jumpPosition), 0.05125 (interpolationLength)                   |
| Quantity    | 0 or 1                                                            |
| Default     | 0 for jumpPosition                                                |

| Sub-element | screenRef                                                                                       |
|-------------|-------------------------------------------------------------------------------------------------|
| Description | Indicates whether the object is screen-related (flag is equal to 1) or not (flag is equal to 0) |
| Units       | 1/0 flag                                                                                        |
| Example     | 0                                                                                               |
| Quantity    | 0 or 1                                                                                          |
| Default     | 0                                                                                               |

| Sub-element | importance               |
|-------------|--------------------------|
| Description | Importance of an object. |
| Units       | 0 to 10                  |
| Example     | 10                       |
| Quantity    | 0 or 1                   |
| Default     | 10                       |
