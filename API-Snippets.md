Code snippets seen on the discord channel, make sure to backup before trying these:

## Bulk Update Tokens
This example updates all tokens in game so that:
* 
* they have `attributes.hp` as a first bar.
* Bars are displayed to owner only
* Names are displayed to owner only on hover.

```js
// Update all tokens in game:
for ( let a of game.actors.entities ) {
    let token = duplicate(a.data.token);

    // Update name and image of token to match name of actor
    token.name = a.data.name;
    token.img = a.data.img;

    // Set first bar to show HP (systems: dnd5, pf)
    token.bar1 = {attribute: "attributes.hp"};

    // Display bars and names to owner only (names on hover)
    token.displayBars = CONST.TOKEN_DISPLAY_MODES.OWNER;
    token.displayName = CONST.TOKEN_DISPLAY_MODES.OWNER_HOVER;
    
    // Actually update game database
    await a.update({token: token});
}
```

## Update Journal Entries Permissions

Step 1 - get the folder you want to target
```js
const folder = game.folders.entities.find(f => (f.data.type === "JournalEntry") && (f.name === "TARGET FOLDER NAME"));
```
Step 2 - get all the Journal Entries which exist within that folder ID
```js
const entries = game.journal.entities.filter(j => j.data.folder === folder._id);
```
Step 3 - modify all those entries to update their default permission
```js
for ( let e of entries ) {
  await e.update({"permission.default": ENTITY_PERMISSIONS.OBSERVER});
}
```

## Bulk update walls on scene

In both examples here approaches to modify walls data are equivalent:
* one duplicates all the walls in advance
* another duplicates each wall individually during iteration.

Second approach might be preferred when on some conditions update is not needed, but otherwise there should be no difference

### Change movement type of walls to "normal":
```js
 const scene = canvas.scene;
 let updatedWalls = duplicate(scene.data.walls).map(w => {
   w.move = WALL_MOVEMENT_TYPES.NORMAL;  // Another option is WALL_MOVEMENT_TYPES.NONE
   return w;
 }
 scene.update({walls: updatedWalls});
```

### Move Walls by 26px on X-axis
```js
 let walls = canvas.scene.data.walls.map(w => {
   w = duplicate(w);
   w.c[0] += 26;  // Move start point
   w.c[2] += 26;  // Move end point
   return w;
 });
 canvas.scene.update({walls: walls});
```

## Move NPCs Into a Folder

Step 1 - get the set of Actors you want to move to a folder
```js
const actors = game.actors.entities.filter(a => a.type === "npc");
```
Step 2 - get the destination folder you want to put them in
```js
const folder = game.folders.entities.find(f => f.name === "My Target Folder");
```
Step 3 - move all the actors to that folder programmatically
```js
for ( let a of actors ) {
  await a.update({folder: folder._id});
}
```

## Map and Wall Scaling
This example scales walls by a factor of 2. Origin of the scaling will be topmost left corner of a scene, so walls in the center of scene will move closer to bottom-right corner, and walls in that corner may be moved beyond the limits of the scene.
```js
 let scale = 2;
 canvas.scene.update({
   walls: canvas.scene.data.walls.map(w => {
     w.c = w.c.map(x => x * scale);
     return w;
   })
 });
 // Redraw canvas to see the changes:
 canvas.draw(); 
```

## Copy Items from a Folder into a Compendium
```js
(async () => {
    const spells = game.items.entities.filter(i => i.folder && i.folder.name === "Bard Spells");
    const pack = game.packs.find(p => p.metadata.label === "Bard Spells");

    for (let s of spells){
      console.log("Adding spell:" + s.name);
      await pack.importEntity(s);
    }    
})();
```

## Copy Items from a Folder with nested Folders into a Compendium
```js
( async () => {
    const folder = game.folders.entities.find(f => f.name === "Blah");
    const pack = game.packs.find(p => p.metadata.label === "Foo");
    let spells = [];

    for (let c of folder.children) {
        if (c.content.length) {
          for (let s of c.content) {
              spells.push(s);
          }
        }
        
    }
    
    for (let s of spells){
      console.log("Adding spell:" + s.name);
      await pack.importEntity(s);
    }    
})();
```
