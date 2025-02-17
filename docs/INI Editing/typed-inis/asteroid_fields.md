---
title: asteroid_fields
---

:::caution

This page is a work in progress!

There may be missing, incomplete or incorrect information on this page as it's still being built! Take information here with a pinch of salt, and feel free to contribute and correct things!

:::

## Overview

These files govern the properties of asteroid field zones as defined in [system](system.md) files.

### Vanilla Examples

* `DATA\SOLAR\ASTEROIDS\br01_cornwall_rock_asteroid_field.ini`
* `DATA\SOLAR\ASTEROIDS\ku03_ohka_dust_field.ini`
* `DATA\SOLAR\ASTEROIDS\li01_badlands_asteroids.ini`

## Syntax

Not all blocks are required.

### TexturePanels

This is only required when a band or billboard is used within this file.

```ini
[TexturePanels]
file = PATH
```

| Parameter | Information                                                                                    |
| --------- | ---------------------------------------------------------------------------------------------- |
| file      | This path points to a set of 2d textures used for the band and billboard elements of the field. |

### Field

Asteroid fields are made out of repeating cubes in which static asteroids are set. This block can be omitted to spawn no static asteroids.

```ini
[Field]
cube_size = INT
fill_dist = INT
diffuse_color = INT, INT, INT
ambient_color = INT, INT, INT0
ambient_increase = INT, INT, INT
tint_field = INT, INT, INT
empty_cube_frequency = FLOAT
max_alpha = FLOAT
```

| Parameter            | Information                                                                        |
| -------------------- | ---------------------------------------------------------------------------------- |
| cube_size            | The size of a cube of asteroids in meters. |
| fill_dist            | The distance from which asteroids are being drawn in the game. |
| diffuse_color        |  |
| ambient_color        |  |
| ambient_increase     | RBG light value added to the existing ambient light when a player is in the field. |
| tint_field           |  | 
| empty_cube_frequency | A chance percentage between 0 and 1 by which cubes are spawned without asteroids inside. |
| max_alpha            | A value between 0 and 1. Seemingly used only for gas "asteroids". |

### Exclusion Zones

:::caution

Please note that defining an exclusion here without a corresponding zone in a system file will cause crashes. 

:::

Exclusion zones cause cubes of this asteroid file to not be created. Note: The exclusion zone must have a minium size related to the defined cube size, or it may have no effect.

```ini
[Exclusion Zones]
exclusion = STRING
exclude_billboards = INT
exclude_dynamic_asteroids = INT
```

| Parameter          | Information                                                                                                                        |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| exclusion          | References the nickname of a zone defined in a system file. This zone will have no randomly generated asteroids spawned within it. Multiple `exclusion` parameters are allowed.|
| exclude_billboards | `1` for `true`. Relates directly to the previous `exclusion` defined. Determines whether or not the exclusion zone uses 'billboards', 2d asteroids that fade as the player approaches them.|
| exclude_dynamic_asteroids | `1` for `true`. Relates directly to the previous `exclusion` defined.  Disables spawning dynamic asteroids within this exclusion.|

### Properties

```ini
[properties]
flag = STRING
```

| Parameter | Information |
| --------- | ----------- |
| flag      | This can be determined multiple times. Appears to apply a tag to the field, uncertain what this is used for. Possibly related to NPC pilots `field_targeting` |

### Cube

The cube defines asteroids which are being spawned as static objects within this field in repeating patterns. This block can be omitted.

```ini
[Cube]
xaxis_rotation = INT, INT, INT, INT
yaxis_rotation = INT, INT, INT, INT
zaxis_rotation = INT, INT, INT, INT
asteroid = STRING, FLOAT, FLOAT, FLOAT, INT, INT, INT, mine
```

| Parameter       | Information |
| --------------- | ----------- |
| xaxis_rotation  |             |
| yaxis_rotation  |             |
| zaxis_rotation  |             |
| asteroid        | The STRING refers to an `[Asteroid]` or `[AsteroidMine]` entry. The following 3 FLOATS are the relative positioning within the cube - usually between 0 and 1, but also negative numbers and probably any numbers work. The last 3 INTs are the rotation of the asteroids in degrees. The ending `mine` is only required for `[AsteroidMine]`, possibly marking them as explosive.|

### Band

The band displays a visual polygon band around the zone from afar to give the impression of a big closed field. Can be omitted.

```ini
[Band]
render_parts = INT
shape = STRING
height = INT
offset_dist = INT
fade = INT, FLOAT, INT, INT
texture_aspect = INT
color_shift = INT, INT, INT
ambient_intensity = INT
vert_increase = INT
```

| Parameter         | Information |
| ----------------- | ----------- |
| render_parts      |             |
| shape             |             |
| height            |             |
| offset_dist       |             |
| fade              |             |
| texture_aspect    |             |
| color_shift       |             |
| ambient_intensity |             |
| vert_increase     |             |

### ExclusionBand

The exclusion band works as normal bands, but specific for exclusion zones. These bands are visible always, not only from within the exclusion zone. Can be omitted.

```ini
[Band]
zone = STRING
render_parts = INT
shape = STRING
height = INT
offset_dist = INT
fade = INT, FLOAT, INT, INT
texture_aspect = INT
color_shift = INT, INT, INT
ambient_intensity = INT
vert_increase = INT
cull_mode = INT
```

| Parameter         | Information |
| ----------------- | ----------- |
| zone              |             |
| render_parts      |             |
| shape             |             |
| height            |             |
| offset_dist       |             |
| fade              |             |
| texture_aspect    |             |
| color_shift       |             |
| ambient_intensity |             |
| vert_increase     |             |
| cull_mode         |             |

### AsteroidBillboards

Within a zone, cheap sprites with textures are shown to render asteroids further away. Can be omitted.

```ini
[AsteroidBillboards]
count = INT
start_dist = INT
fade_dist_percent = FLOAT
shape = mine_rock_tri
color_shift = FLOAT, FLOAT, FLOAT
ambient_intensity = INT
size = INT, INT
```

| Parameter         | Information |
| ----------------- | ----------- |
| count             |             |
| start_dist        |             |
| fade_dist_percent |             |
| shape             |             |
| color_shift       |             |
| ambient_intensity |             |
| size              |             |

### DynamicAsteroids

Dynamic asteroids fly randomly across the inside of a zone. They are client-side and always spawn around the camera position. They can be used to create lootable areas. Can be omitted. Can be defined multiple times?

```ini
[DynamicAsteroids]
asteroid = STRING
count = INT
placement_radius = INT
placement_offset = INT
max_velocity = INT
max_angular_velocity = INT
color_shift = INT, INT, INT
```

| Parameter            | Information |
| -------------------- | ----------- |
| asteroid             |             |
| count                |             |
| placement_radius     |             |
| placement_offset     |             |
| max_velocity         |             |
| max_angular_velocity |             |
| color_shift          |             |


### LootableZone

Within lootable zones, any dynamic asteroid can drop commodities on destruction. This block can be defined multiple times for multiple lootable zones. Can also be entirely omitted.

```ini
[LootableZone]
zone = zone_bw03_img_cobalt_mining_area ; optional
asteroid_loot_container = STRING
asteroid_loot_commodity = STRING
dynamic_loot_container = STRING
dynamic_loot_commodity = STRING
asteroid_loot_count = INT, INT
dynamic_loot_count = INT, INT
asteroid_loot_difficulty = INT
dynamic_loot_difficulty = INT
```

| Parameter                | Information |
| ------------------------ | ----------- |
| zone                     | Name of a zone within the asteroid field to which this lootable zone is limited. If omitted, the lootable zone applies to the entire asteroid field. |
| asteroid_loot_container  | Name of a `[LootCrate]` created when something dropped from an asteroid. Seems unused. |
| asteroid_loot_commodity  | Name of a `[Commodity]` dropped within the `asteroid_loot_container`. Seems unused. |
| asteroid_loot_count      | Random commodity unit count from INT to INT units within the dropped loot container. Seems unused. |
| asteroid_loot_difficulty | Difficulty required to drop loot from an asteroid? Seems unused. |
| dynamic_loot_container   | Name of a `[LootCrate]` created when something dropped from a dynamic asteroid. Seems unused. |
| dynamic_loot_commodity   | Name of a `[Commodity]` dropped within the `asteroid_loot_container`. Seems unused. |
| dynamic_loot_count       | Random commodity unit count from INT to INT units within the dropped loot container. Seems unused. |
| dynamic_loot_difficulty  | Difficulty required to drop loot from a dynamic asteroid? Seems unused. |
