Code snippets seen on the discord channel, make sure to backup before trying these:

**Update Journal Entries Permissions**
```
 // Step 1 - get the folder you want to target
 const folder = game.folders.entities.find(f => (f.data.type === "JournalEntry") && (f.name === "TARGET FOLDER NAME"));
 
 // Step 2 - get all the Journal Entries which exist within that folder ID
 const entries = game.journal.entities.filter(j => j.data.folder === folder._id); 
 
 // Step 3 - modify all those entries to update their default permission
 for ( let e of entries ) {
   await e.update({"permission.default": ENTITY_PERMISSIONS.OBSERVER});
 }
```

**Update wall movement type**
```
 const scene = canvas.scene;
 let updatedWalls = duplicate(scene.data.walls).map(w => {
   w.move = WALL_MOVEMENT_TYPES.NORMAL;
   return w;
 }
 scene.update({walls: updatedWalls});
```

**Move walls by 26px**
```
 let walls = canvas.scene.data.walls.map(w => {
   w = duplicate(w);
   w.c[0] += 26;
   w.c[2] += 26;
   return w;
 });
 canvas.scene.update({walls: walls});
```

**Move NPCs into a folder**
```
 // Step 1 - get the set of Actors you want to move to a folder
 const actors = game.actors.entities.filter(a => a.type === "npc");
 
 // Step 2 - get the destination folder you want to put them in
 const folder = game.folders.entities.find(f => f.name === "My Target Folder");
 
 // Step 3 - move all the actors to that folder programmatically
 for ( let a of actors ) {
   await a.update({folder: folder._id});
 }
```

**(Untested) Map and Wall Scaling**
```
 let scale = 2;
 canvas.scene.update({
   walls: canvas.scene.data.walls.map(w => {
     w.c = w.c.map(x => x * scale);
     return w;
   });
 });
```
