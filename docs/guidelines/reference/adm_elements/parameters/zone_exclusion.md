# zoneExclusion

The `zoneExclusion` parameter appears in [`audioBlockFormat`](../audio_channel_format_objects.md#audioblockformat) only for the 'Objects' typeDefinition.

The `zoneExclusion` parameter is used to dynamically reconfigure the object renderer to “mask out” certain speaker zones during playback. This guarantees that no loudspeaker belonging to the masked zones will be used for rendering the applicable object. Typical zone masks used in production today include sides and rear. Multiple `zone` sub-elements within `zoneExclusion` can be set simultaneously to mask out more than one zone. The default is that all zones are enabled and when `zoneExclusion` is set to one or more of the indicated zones, those are “masked out” during playback. The sub-element zone is used to define the coordinates of the zone in the unit-cuboid.

Zones are defined in the Cartesian coordinate system using the sub-element zone by specifying the corner points of a unit-cuboid in 3D space by: `minX`, `maxX`, `minY`, `maxY`, `minZ`, `maxZ`. In the spherical coordinate system the zone is defined by: `minAzimuth`, `maxAzimuth`, `minElevation`, `maxElevation`.

For example: `minX`=−1.0, `maxX`=1.0, `minY`=−1.0, `maxY`=–1.0, `minZ`=−1.0, `maxZ`=1.0 specifies the rear wall.

Varying this parameter over successive blocks should be avoided.
