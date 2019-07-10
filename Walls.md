# Walls
The Grid Layer is positioned 2nd from bottom in the layers of the Canvas. The Grid Layer is responsible for orienting and segmenting the game space into grid spaces. Currently only a square grid is supported but hex grid support is flagged as a feature for work during Beta development.

The Grid provides convenience tools for measuring distance, restricting token movement, and providing guide lines for anchoring wall segments or other canvas features.

## Regular Walls
These walls block both movement and vision. They are rendered on the Walls Layer using an off-white color.

## Terrain Walls

## Invisible Walls
These walls block movement, but not vision. They are rendered on the Walls Layer using a light blue color.

## Ethereal Walls

## Doors
These walls are able to be toggled between multiple states. Doors may be closed, open, or locked. Closed (or locked) doors block both movement and vision, while open doors do not block either vision or movement. Doors will be rendered as a small icon for player views which, if clicked, will open or close the door provided it is not locked. Only Game-Master players have the ability to unlock doors. Open doors are rendered in green while with closed doors in orange and locked doors in red.

## Secret Doors
These walls work as doors, able to be toggled between closed, open, or locked states, however unlike regular doors the icon for secret doors is not shown to players and these can only be toggled by the Game Master. Secret doors are rendered in purple.
