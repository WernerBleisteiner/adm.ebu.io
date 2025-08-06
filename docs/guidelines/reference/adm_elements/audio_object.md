# audioObject

## Description

An `audioObject` element establishes the relationship between the content, the format via audio packs, and the assets using the [`audioTrackUID`](audio_track_uid.md) elements. `audioObject`s can be nested to group together other `audioObjects`.

## Example

```xml
<audioObject audioObjectID="AO_1002"
             audioObjectName="Object2"
             start="00:00:00.00000"
             dialogue="0" importance="5" interact="1" disableDucking="0">
  <audioPackFormatIDRef>AP_00010001</audioPackFormatIDRef>
  <audioComplementaryObjectIDRef>AO_1001</audioComplementaryObjectIDRef>
  <audioTrackUIDRef>ATU_00000003</audioTrackUIDRef>
  <audioObjectInteraction onOffInteract="1" gainInteract="1">
    <gainInteractionRange bound="min">-20.0</gainInteractionRange>
    <gainInteractionRange bound="max">3.0</gainInteractionRange>
  </audioObjectInteraction>
</audioObject>
```

## Attributes

| Attribute            | Description                 | Example  | Required | Default |
|----------------------|-----------------------------|----------|----------|---------|
| audioObjectID        | ID of the object            | AO_1001  | Yes      |         |
| audioObjectName      | Name of the object          | dialogue_stereo    | Yes      | |
| start                | Start time for the object, relative to the start of the programme.      | 00:00:00.00000 | Optional | 00:00:00.00000 |
| duration             | Duration of object.         | 00:02:00.00000 | Optional | unbounded |
| importance           | Importance of an object. Allows a renderer to discard an object below a certain level of importance. 10 is most important, 0 least. | 10 | Optional | 10 |
| interact             | Set to 1 if a user can interact with the object, 0 if not. | 1 | Optional | 0 |
| disableDucking       | Set to 1 to disallow automatic ducking of object, 0 to allow ducking |	0	| Optional | 0 |

The time is shown in the format of ‘hh:mm:ss.zzzzz’. ‘hh:mm:ss.zzzzz’ indicates hours, minutes, seconds and fractional seconds.

## Sub-elements

| Sub-element      | Description                                                       | Example | Quantity |
|------------------|-------------------------------------------------------------------|---------|----------|
| audioPackFormatIDRef | Reference to an audioPackFormat for format description	| AP_00010001	| 0..* |
| audioObjectIDRef | Reference to another audioObject | AO_1002 | 0..* |
| [audioComplementaryObjectIDRef](#audiocomplementaryobjectidref)	| Reference to another audioObject that is complementary to the object, e.g. to describe mutually exclusive languages. | AO_1003 | 0..* |
| audioTrackUIDRef | Reference to an audioTrackUID (when using a BW64 file, this is listed in the <chna> chunk)	| ATU_00000001 | 0..* |
| audioObjectInteraction | Specification of possible user interaction with the object. | | 0 or 1 |

If the value of `audioTrackUIDRef` is set to ATU_00000000 it does not refer to a track in the file, but refers to a virtual empty track. This can be useful for multichannel formats where some of the channels are not being used, so instead of storing zero value samples in the file, this silent track is used instead thus saving space in the file.

### audioComplementaryObjectIDRef

The `audioComplementaryObjectIDRef` element contains a reference to another `audioObject` that is complementary to the parent `audioObject`. A list of `audioComplementaryObjectIDRef`s can therefore be used to describe mutually exclusive objects, e.g. language tracks that contain the same dialogue in different dub versions (“XOR” relationship).
To avoid cross-references between `audioComplementaryObjectIDRef`s of several `audioObject`s, the `audioComplementaryObjectIDRef` sub-element should only be included in one corresponding parent `audioObject` for each set of mutually exclusive contents. The parent `audioObject` with the `audioComplementaryObjectIDRef`s should be the one that contains the default version of the set of mutually exclusive objects.

### audioObjectInteraction sub-element

An `audioObjectInteraction` element describes any possible user interaction with the corresponding parent `audioObject`. It should be present only if the `interact` attribute of the parent `audioObject` is set to 1. In case the “Interact” attribute of the parent `audioObject` is set to 0, any `audioObjectInteraction` element should be ignored. The `audioObjectInteraction` element has the following attributes and sub-elements.

| Attribute |	Description |	Example	| Required |
| ----------|-------------|---------|----------|
| onOffInteract	| Set to 1 if a user can switch the object on or off, 0 if not.	| 1	| Yes |
| gainInteract | Set to 1 if a user can change the gain of the object, 0 if not. | 1 | Optional |
| positionInteract | Set to 1 if a user can change the position of the object, 0 if not. | 0 | Optional |

If the `onOffInteract` attribute is set to 1, the `audioObject` can be swithced on or off by the user. If the `gainInteract` attribute is set to 1, the gain of the `audioObject` can be changed by the user according to the [`gainInteractionRange`](#gaininteractionrange) sub-element. If the `positionInteract` attribute is set to 1, the positions of the `audioBlockFormat`s in the parent `audioObject` can be changed by the user according to the [`positionInteractionRange`](#positioninteractionrange) sub-element.

If an `audioObject` allows interaction, the change to an attribute that can be set by the user should be within the limits of the interaction range of that `audioObject`. In this context, a “change” is the difference between a condition before and after the interaction.
The resultant position and gain of a sound source is the combination of the attributes of the position and gain sub-elements of the `audioBlockFormat` and all the changes caused by interaction in the hierarchy of `audioObject`s that refer to the `audioBlockFormat`.

#### gainInteractionRange

| Bound attribute	| Description	| Units |	Example |
|-----------------|-------------|-------|---------|
| min	            | Minimum gain factor of possible user gain interaction (gainMin = gain (or 1.0 if not defined) * gainInteractionRangeMin) | linear gain value | 0.5 |
| max	            | Maximum gain factor of possible user gain interaction (gainMax = gain (or 1.0 if not defined) * gainInteractionRangeMax) | linear gain value | 1.5 |

##### Example

```xml
<audioObjectInteraction onOffInteract="1" gainInteract="1">
  <gainInteractionRange bound="min">-20.0</gainInteractionRange>
  <gainInteractionRange bound="max">3.0</gainInteractionRange>
</audioObjectInteraction>
```

#### positionInteractionRange

For polar coordinates:

| coordinate attribute | bound attribute | Description | Units | Example |
|----------------------|-----------------|-------------|-------|---------|
| azimuth | min	| Minimum azimuth offset value of possible user position interaction | Degrees | –30.0 |
| azimuth | max | Maximum azimuth offset value of possible user position interaction | Degrees | +30.0 |
| elevation | min | Minimum elevation offset value of possible user position interaction | Degrees | –15.0 |
| elevation | max | Maximum elevation offset value of possible user position interaction | Degrees | +15.0 |
| distance | min | Minimum normalised distance of possible user position interaction | 0 to 1 | 0.5 |
| distance | max | Maximum normalised distance of possible user position interaction | 0 to 1 | 0.5 |

##### Example

```xml
<audioObjectInteraction onOffInteract="1" positionInteract="1">
  <positionInteractionRange bound="min" coordinate="azimuth">-50.0</positionInteractionRange>
  <positionInteractionRange bound="max" coordinate="azimuth">50.0</positionInteractionRange>
  <positionInteractionRange bound="min" coordinate="elevation">-20.0</positionInteractionRange>
  <positionInteractionRange bound="max" coordinate="elevation">20.0</positionInteractionRange>
  <positionInteractionRange bound="min" coordinate="distance">0.6</positionInteractionRange>
  <positionInteractionRange bound="max" coordinate="distance">1.0</positionInteractionRange>
</audioObjectInteraction>
```

For Cartesian coordinates:

| coordinate attribute | bound attribute | Description | Units | Example |
|----------------------|-----------------|-------------|-------|---------|
| X | min | Minimum X-axis offset value of possible user position interaction | Normalized Units | –0.5 |
| X | max | Maximum X-axis offset value of possible user position interaction | Normalized Units | +0.5 |
| Y | min | Minimum Y-axis offset value of possible user position interaction | Normalized Units | –0.2 |
| Y | max | Maximum Y-axis offset value of possible user position interaction | Normalized Units | 0.0 |
| Z | min | Minimum Z-axis offset value of possible user position interaction | Normalized Units | 0.1 |
| Z | max | Maximum Z-axis offset value of possible user position interaction | Normalized Units | 0.4 |

##### Example

```xml
<audioObjectInteraction onOffInteract="1" positionInteract="1">
  <positionInteractionRange bound="min" coordinate="X">-0.5</positionInteractionRange>
  <positionInteractionRange bound="max" coordinate="X">0.5</positionInteractionRange>
  <positionInteractionRange bound="min" coordinate="Y">-0.2</positionInteractionRange>
  <positionInteractionRange bound="max" coordinate="Y">0.2</positionInteractionRange>
  <positionInteractionRange bound="min" coordinate="Z">0.0</positionInteractionRange>
  <positionInteractionRange bound="max" coordinate="Z">1.0</positionInteractionRange>
</audioObjectInteraction>
```

## Nested audioObjects and timing parameters

When audioObject elements are nested the start time of the `audioObject` is still relative to the start of the programme, not the relative to the `audioObject` that refers to it. It is required to ensure that any `audioObject` that is referred from another audioObject does not have a start time earlier than the referent, nor does it have an end time (i.e. start + duration) after the referent.
