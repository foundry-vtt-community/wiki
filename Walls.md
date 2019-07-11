**# Walls**
Walls are a means for defining virtual boundaries in FoundryVTT. There are several types of walls that a GM can create as defined below.  Walls are typically not actually visible to players (with the exception of doors) or their tokens however can block visibility, movement and "local only" sound depending on the type of walls predefined by the GM. The GM draws walls segments, one at a time between two points. 

Players controlling tokens in a scene cannot move their token passed a wall that blocks it movement, however the GM (or players granted special permission) can move tokens passed movement blocking walls or doors. The exception to this are single direction walls which block movement only in one direction. TIP: Fun for insidious traps. 

**## Regular Walls**
These walls block movement, vision and sounds. They are rendered on the Walls Layer using an off-white color.

**## Terrain Walls**
Terrain walls are used for blocking movement of a token only.  They can be defined to block both directions of movement or just a single direction using the toggle left/right wall direction.  If a single direction is selected, an arrow appears in the wall segment indicating the direction of movement blocking and are drawn as a light green color.

**## Invisible Walls**
These walls block movement, but not vision or sound. They are rendered on the Walls Layer using a light blue color.

**## Ethereal Walls**
Ethereal walls block token vision and sound but do not hinder the movement of tokens and are drawn as a purple color.

**## Doors**
These walls are able to be toggled between multiple states. Doors may be closed, open, or locked. Closed (or locked) doors block movement, vision and sound, while open doors do not block vision, movement or sound. Doors will be rendered as a small icon for player views which, if clicked, will open or close the door provided it is not locked. Only Game-Master players have the ability to unlock doors. Open doors are rendered in green while with closed doors in orange and locked doors in red.

**## Secret Doors**
These walls work as doors, able to be toggled between closed, open, or locked states, however unlike regular doors the icon for secret doors is not shown to players and these can only be toggled by the Game Master. Secret doors are rendered in purple.

**## IMPORTANT TIPS**
Chaining wall segments: This can be done by holding down CTRL (on a PC) while creating a wall segment. The GM can continue clicking to chain together more wall segments.  Releasing CTRL completes a wall segment.

**Wall snapping:** The two points used to define a wall segment are snapped to a micro grid to ensure they are relatively drawn evenly and can easily be joined to other wall segments. Walls can be moved after creation by clicking on a wall segment point and holding the mouse button while dragging to a new location. Once released, the wall point will be moved and the wall adjusted accordingly.

**Deleting a wall segment**: Simply click on one of its points and press the DEL key (PC).

**Edit a wall segment:** By double-clicking a wall segment point shows the wall segment properties.  You can change the properties of an existing wall in that popup screen.  The color of the wall segment will adjust to the appropriate color.

**The Grid Layer:** is positioned 2nd from bottom in the layers of the Canvas. The Grid Layer is responsible for orienting and segmenting the game space into grid spaces. Currently only a square grid is supported but hex grid support is flagged as a feature for work during Beta development.

The Grid provides convenience tools for measuring distance, restricting token movement, and providing guide lines for anchoring wall segments or other canvas features.