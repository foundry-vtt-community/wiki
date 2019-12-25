Walls are a means for defining virtual boundaries in FoundryVTT. There are several types of walls that a GM can create as defined below.  Walls are typically not actually visible to players (with the exception of doors) or their tokens however can block visibility, movement and sounds depending on the type of walls predefined by the GM. The GM draws walls segments, one at a time between two points. 

Players controlling tokens in a scene cannot move their token passed a wall that blocks it movement, however the GM (or players granted special permission) can move tokens passed movement blocking walls or doors. The exception to this are single direction walls which block movement only in one direction. TIP: Fun for insidious traps. 

A specific tokens ability to see and hear sounds beyond a wall depends on the wall type. Some walls block token visibility, light, and/or sounds some do not. Vision blocking walls effects how light exposes a particular area of the scene that token might be able to see and also effects how Fog of War is exposed in a scene.  Sounds too can be blocked by certain walls.  The exception to these rules are "global" lights and sounds which are seen and heard through all wall types.

# Wall Types

## Regular Walls
These walls block movement, vision and sounds. They are rendered on the Walls Layer using an off-white color.

## Terrain Walls
Terrain walls are used for blocking movement of a token and vision beyond the terrain wall boundary.  These are typically used to hide what is behind an object, but allows the token can see the object itself such as a building.  Draw a series of terrain wall segments to define the outside of the object and the token can still see the object however the terrain wall now blocks vision and sound behind it. Terrain walls are drawn as a light green color.

## Invisible Walls
These walls block movement, but not vision or sound. They are rendered on the Walls Layer using a light blue color.

## Ethereal Walls
Ethereal walls block token vision and sound but do not hinder the movement of tokens and are drawn as a purple color.

## Doors
These walls are able to be toggled between multiple states. Doors may be closed, open, or locked. Closed (or locked) doors block movement, vision and sound, while open doors do not block vision, movement or sound. Doors will be rendered as a small icon for player views which, if clicked, will open or close the door provided it is not locked. Only Game-Master players have the ability to unlock doors. Open doors are rendered in green while with closed doors in orange and locked doors in red.

## Secret Doors
These walls work as doors, able to be toggled between closed, open, or locked states, however unlike regular doors the icon for secret doors is not shown to players and these can only be toggled by the Game Master. Secret doors are rendered in purple.

# IMPORTANT TIPS
See Walls and Journals video available:

[![Walls and Journals YouTube Video](http://img.youtube.com/vi/zLTArUhSssU/0.jpg)](http://www.youtube.com/watch?v=zLTArUhSssU)

Global lights are not affected by walls or doors. Global lights will be visible to all tokens that have visibility, regardless of wall between the token and the light source. This will also effect Fog of War.

Global sounds are heard by all tokens through all wall types.

**Chaining Wall Segments**: This can be done by holding down `CTRL` (on a PC) while creating a wall segment. The GM can continue clicking to chain together more wall segments.  Releasing `CTRL` completes a wall segment.

**Wall Snapping**: The two points used to define a wall segment are snapped to a micro grid to ensure they are relatively drawn evenly and can easily be joined to other wall segments. Walls can be moved after creation by clicking on a wall segment point and holding the mouse button while dragging to a new location. Once released, the wall point will be moved and the wall adjusted accordingly.

**Deleting a Wall Segment**: Simply click on one of its points and press the `DEL` key (PC).

**Edit a Wall Segment**: By double-clicking a wall segment point shows the wall segment properties.  You can change the properties of an existing wall in that popup screen.  The color of the wall segment will adjust to the appropriate color.

**Edit multiple Wall Segments**: Hold down the `SHIFT` key while clicking on multiple wall segments' points. Double-click
any wall segment point to bring up the properties which you can change for all of the selected wall segments.

**Rescaling your walls along with your scene**: Note that before using such a command, a backup is always advised. If you rescaled your scene and want to rescale your walls along with it, you can do so using the following code in the console (F12 to open, console tab at the top) with the appropriate scaling factor (here the scene has been assumed to double in size):
```js
let scale = 2;
canvas.scene.update({
  walls: canvas.scene.data.walls.map(w => {
    w.c = w.c.map(x => x * scale);
    return w;
  })
});```

**Directional Wall Segments**: Wall segments can be directional (left/right/both) to block is various ways.  Edit the wall segment to modify this option.

**The Grid Layer**: Is positioned 2nd from bottom in the layers of the Canvas. The Grid Layer is responsible for orienting and segmenting the game space into grid spaces. Currently only a square grid is supported but hex grid support is flagged as a feature for work during Beta development.

The Grid provides convenience tools for measuring distance, restricting token movement, and providing guide lines for anchoring wall segments or other canvas features.