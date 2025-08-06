# Screen-related content

The `screenRef` parameter appears in
[`audioBlockFormat`](../adm_elements/audio_channel_format_objects.md#audioblockformat) with
typeDefinition 'Objects' and
[`audioBlockFormat`](../adm_elements/audio_channel_format_objects.md#audioblockformat) with
the typeDefinition 'HOA' and the
[`audioPackFormat`](../adm_elements/audio_pack_format_hoa.md) with the typeDefinition 'HOA'.
It indicates whether the content is screen-related or not. The
`audioProgrammeReferenceScreen` parameter appears in
[`audioProgramme`](../adm_elements/audio_programme.md) and describes the screen which was
used during production.

The `screenRef` flag can be used by a renderer for special processing of all
screen-related objects taking into account the size of a local reproduction
screen compared to the production screen-size.

If a renderer uses the `screenRef` flag to enable a special processing, it
should use the reference/monitoring/production screen-size of the currently
rendered `audioProgramme` as the reference screen.

If the flag is set and no `audioProgrammeReferenceScreen` element is included in
the corresponding currently rendered `audioProgramme`, the default reference
production/monitoring screen is implicitly defined on the basis of
[Recommendation ITU-R BT.1845](https://www.itu.int/rec/R-REC-BT.1845/en) –
Guidelines on metrics to be used when tailoring television programmes to
broadcasting applications at various image quality levels, display sizes and
aspect ratio.

| Property                                      | Value                                        |
|-----------------------------------------------|----------------------------------------------|
| Azimuth of left bottom corner of screen	      | 29.0°                                        |
| Elevation of the left bottom corner of screen	| −17.3°                                       |
| Aspect ratio                                  | 1.78 (16:9)                                  |
| Width of the screen                           | 58° (as defined by image system 3840 x 2160) |

These spherical values can be transferred to Cartesian coordinates assuming a
reference distance of 1.0 by first transferring the values above to the
“standard” azimuth/elevation convention (0° azimuth is in front of the right
ear, positive values are counted counter-clockwise; 0° elevation is directly
above the head, positive values are counted downwards to the front) and then
using the trigonometric functions to gain the Cartesian coordinates. The screen
is assumed to have its corners touching the unit sphere. This results in the
following values (orientation of the [Cartesian
coordinate](coordinate_system.md) axes):

| Property                                 | Value  |
|------------------------------------------|--------|
| X-coordinate of the centre of the screen | 0.0    |
| Y-coordinate of the centre of the screen | 0.8438 |
| Z-coordinate of the centre of the screen | 0.0    |
| Aspect ratio                             | 1.78   |
| Width of the screen                      | 0.9354 |

## Coordinate conversion

The maths to convert from the polar coordinate screen to Cartesian coordinates is

$$d = \frac{1}{\sqrt{\frac{1}{a^2}\tan^2\left(\frac{w}{2}\right) + 1}},$$

where \(d\) is the Y-coordinate of the centre of the screen, \(a\) is the aspect ratio, and \(w\) is the polar angle of the screen width.

\(x = 2d \tan⁡\left(\frac{w}{2}\right)\), where \(x\) is the Cartesian screen width, and \(w\) is the polar angle of the screen width.
