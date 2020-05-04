Code snippets seen on the discord channel, make sure to backup before trying these:

## Bulk Update Tokens
This example updates all tokens in game.

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

## Scaling ruler labels
When zoomed out ruler labels become almost not visible. They can be scaled by processing pan hook calls, but maybe you should just make a macro and put it on hotbar
```js
// This is not very good example because you need to zoom while ruler is visible (e.g. use ruller with Ctrl pressed)
Hooks.on("canvasPan", (canvas, options) => {
  let labelScale = 1;
  if (options.scale < 1) {
    labelScale = 1/options.scale;
  };
  canvas.controls.getRulerForUser(game.userId).labels.children.map(c=>c.transform.scale.set(labelScale));
  // if you are scaling from simple macro then you can set scale to (1/canvas.stage.scale._x)
});

```

## Play some audio-file
```js
AudioHelper.play({src: "audio/SFX/Some File.mp3", volume: 0.8, autoplay: true, loop: false}, true);
```

## Combat

### Starting combat

`token.toggleCombat()` or:
```js
// having `token` variable:
combat = await game.combats.object.create({scene: canvas.scene._id, active: true});
await combat.createEmbeddedEntity("Combatant", [{tokenId: token.id, hidden: token.data.hidden}]);
```
```js
// existing combat from sidebar:
combat = ui.combat.combat
```

### Do something based on rolled initiative for active combat

```js

async function processCombat(combat) {
  var combat = combat ? combat : game.combat;  // curren combat of current scene by default

  // Will change something based on difference between their initiative and best initiative:
  const topInit = parseFloat(combat.turns[0].initiative);

  // let's do this:
  await Promise.all(combat.turns.map(async (turn) => {
    const c = this.getCombatant(turn._id);
    if ( !c || ! c.actor ) return ;
    // Doing "something" (you probably should replace next part:
    const newValue = Math.max(
      0,
      c.actor.data.data.resources.time.max - Math.round((topInit-parseFloat(turn.initiative))/3)
    );
    if ( c.actor.data.data.resources.time.value != newValue ) {
      return c.actor.update({"data.resources.time.value": newValue});
    };
  }));
}
```

## Simple distance between 2 tokens

[`canvas.grid.measureDistance(fromToken, toToken, {gridSpaces: True})`](https://foundryvtt.com/api/GridLayer.html#measureDistance)

## Ask for some input using Dialog

[Dialog](https://foundryvtt.com/api/Dialog.html) example:

```js

// Return distance from 2 tokens or ask it with dialog. 
// For example you can call it like distance, somethingElse = promptDistanceNSomethingElse(canvas.tokens.controlled[0], game.user.targets[0])
export async function promptDistanceNSomethingElse(fromToken, toToken) {
  var distance = 0,
      somethingElse = 0;
  if (!fromToken) {
    ui.notifications.error('promptDistanceNSomethingElse needs at least fromActor arg');
    throw "bad thing happened";
  }
  if ( toToken ) {
    distance = canvas.grid.measureDistance(fromToken, toToken, {gridSpaces: false}) - 1; // -1 to have zero distance between tokens in neighbour grid cells.
    distance = Math.round(distance*100)/100;
    somethingElse = toToken.attributes.magicSecrets.somethingElse.value;
  } else {
    const content = '\n'+
    'This action needs to know distance and somethingElse.' +
    '\n<div class="form-group dialog distance-prompt">' +
    '\n  <label>distance:</label> <input type="number" name="distance" value="0"/>' +
    '\n</div>' +
    '\n<div class="form-group dialog distance-prompt">' +
    '\n  <label>somethingElse:</label> <input type="number" name="somethingElse" value="0"/>' +
    '\n</div>';
    [distance, somethingElse] = await new Promise((resolve, reject) => {
      new Dialog({
        title: "Distance",
        content: content,
        default: 'ok',
        buttons: {
          ok: {
            icon: '<i class="fas fa-check"></i>',
            label: 'ok',
            default: true,
            callback: html => {
              resolve([
                html.find('.distance-prompt.dialog [name="distance"]')[0].value,
                html.find('.distance-prompt.dialog [name="somethingElse"]')[0].value,
              ]);
            },
          }
        }
      }).render(true);
    });
    distance = parseInt(distance ? distance : 0);
    somethingElse = parseInt(somethingElse ? somethingElse : 0);
  }
  return [distance, somethingElse];
}
```
