Code snippets seen on the discord channel, make sure to backup before trying these:

## Bulk Update Tokens
```
for ( let a of game.actors.entities ) {
    let token = duplicate(a.data.token);
    token.name = a.data.name;
    token.img = a.data.img;
    token.bar1 = {attribute: "attributes.hp"};
    token.displayBars = CONST.TOKEN_DISPLAY_MODES.OWNER;
    token.displayName = CONST.TOKEN_DISPLAY_MODES.OWNER_HOVER;
    await a.update({token: token});
}
```

## Update Journal Entries Permissions

Step 1 - get the folder you want to target
```
const folder = game.folders.entities.find(f => (f.data.type === "JournalEntry") && (f.name === "TARGET FOLDER NAME"));
```
Step 2 - get all the Journal Entries which exist within that folder ID
```
const entries = game.journal.entities.filter(j => j.data.folder === folder._id);
```
Step 3 - modify all those entries to update their default permission
```
for ( let e of entries ) {
  await e.update({"permission.default": ENTITY_PERMISSIONS.OBSERVER});
}
```

## Update Wall Movement Type
```
 const scene = canvas.scene;
 let updatedWalls = duplicate(scene.data.walls).map(w => {
   w.move = WALL_MOVEMENT_TYPES.NORMAL;
   return w;
 }
 scene.update({walls: updatedWalls});
```

## Move Walls by 26px
```
 let walls = canvas.scene.data.walls.map(w => {
   w = duplicate(w);
   w.c[0] += 26;
   w.c[2] += 26;
   return w;
 });
 canvas.scene.update({walls: walls});
```

## Move NPCs Into a Folder

Step 1 - get the set of Actors you want to move to a folder
```
const actors = game.actors.entities.filter(a => a.type === "npc");
```
Step 2 - get the destination folder you want to put them in
```
const folder = game.folders.entities.find(f => f.name === "My Target Folder");
```
Step 3 - move all the actors to that folder programmatically
```
for ( let a of actors ) {
  await a.update({folder: folder._id});
}
```

## (Untested) Map and Wall Scaling
```js
 let scale = 2;
 canvas.scene.update({
   walls: canvas.scene.data.walls.map(w => {
     w.c = w.c.map(x => x * scale);
     return w;
   });
 });
```

## Copy Items from a Folder into a Compendium
```js
(async () => {
    const spells = game.items.entities.find(i => i.folder.name === "Bard Spells");
    const pack = game.packs.find(p => p.metadata.label === "Bard Spells");

    for (let s of spells){
            console.log("Adding spell:" + s.name);
            await pack.importEntity(s);
            }
        }    
})();
```
