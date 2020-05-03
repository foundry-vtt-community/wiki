# Learning API

Foundry VTT API can be used to write [[script macros|Script-Macros]] (that can be used from hotbar or from chat) or to write your own [[extension modules|Community-Modules]] or even your own [[system implementations|System-Development-for-Beginners)]].

There are many objects available in [Foundry API](https://foundryvtt.com/api/) with a lot of attributes and methods. But in the simplest case you'll want to write some macro to do something of the following:
* manipulate tokens on map or manipulate data in Actor Sheets of those tokens.
* Send messages to chat or make rolls.

## Updating data

Many of the objects that you'll want to change are subclasses of [Entity](https://foundryvtt.com/api/Entity.html) and they all have a `data` attribute that usually holds all the things you may want to analyse or change. You must always keep in mind next things about data:

* It is also stored on server, so any changes to it must also be pushed to server. Usually you can just stick to `entity.update({"some.path.as.string": value})` to update both local and server data and everything will be good.
* For Actors structure of `actor.data` almost always looks like this: `{_id: "...", name: "...", permissions: {...}, type: "e.g.character", data: {}}`, where actual "details" are stored in the "nested" `data`. So if you want to get some attribute, then you should do something like this `getProperty(actor.data.data, 'attributes.str.mod')`
* While most of the actor's data is stored in `actor.data.data`, other things of "top-most" data are stored on server too, and so `actor.update(path, value)` method uses "paths" relative to top-most data attribute. That's why you are getting attribute values using "double data" (`actor.data.data.attributes.str.value`) but updating them with "single" data (`actor.update({'data.attributes.str.value': actor.data.data.attributes.str.value+1})`).
* Server accepts specific structure of data depending on the type of entity that you work with, and adding your own fields usually will be ignored by server, and so will not be "saved". Currently this structure is not really documented anywhere, so you'll have to inspect answers from server to actually see what's there.
* In some cases not everything that you have in `data` is really saved on server: some game systems populate `data` with dynamically computed values that are being built from "permanent data"
* Entities may have EmbeddedEntities "inside" of them, which often are "owned copies" of some object from collection, for example Actor may have "OwnedItem" embedded entity that is a copy of entity from Item tab of sidebar. In fact data of those entities is stored in `entity.data[something] = []`, so you may work with that data directly, but often actor will have attribute with a list of class instances that represent the same data, for example: `actor.data.items` is a list of plain `object`s, while `actor.items` is a list of [`Item`s](https://foundryvtt.com/api/Item.html) represented by that data. Calling `update` on objects retreived from those "helper" attributes will just call proper update from a parent object.
* Entities may have attributes returning other entities, that really are built from data of "parent" entity. Updating those usually will just call `parent.update` with proper paths. They are somewhat familiar to embedded entities but do not support `parent.updateEmbeddedEntities` method. For example `token.actor` is an [Actor](https://foundryvtt.com/api/Actor.html) entity that in some cases simply represents data from `token.data.actorData`.
* If you use the [d&d 5 system](https://gitlab.com/foundrynet/dnd5e/-/blob/38afcea18fe723f48ebcb305bc91dc5cc1ee419a/module/actor/entity.js#L302) as reference, then you may think that updating data like `data["token.height"]` works too. In that system that approach works because it's done in method that later sends that data to server. In other examples you may see that some data attributes are assigned as `actor.data.data.attributes.somethingDerived.value = X` -- usually this is done without `actor.update()` because it sets dynamic data that can be calculated and does not require saving. The same is true for `setProperty(actor, key, value)` — it may be used to build dynamic data but will not trigger updates on server.

Actual examples to update data of `token` or of `actor`:

* `token.update({"img": "shared/images/tokens/Foo-Bar.png"})` — to update image of a token.
* `actor.items[0].update({"name": actor.items[0].data.name+ " (rusty)"})` — to update name of first item in the inventory of actor. It's the same as `actor.updateEmbeddedEntity("OwnedItem", {_id: actor.items[0]._id, name: actor.items[0].data.name+ " (rusty)"})`. And `actor.items[0].data.name` here is the same as `actor.data.items[0].name`
* `Actor.update({_id: actor._id, name: actor.name+" test"})` -- update name of an actor. The same as `actor.update({name: actor.name+" test"})`.
* `Actor.update([{_id: actor1._id, name: actor1.name+" test"}, {_id: actor2._id, name: actor2.name+" test"}])` — update multiple actors simultaneously.

## Permissions

Only GM can change data of ANY token. Other users are usually very limited in what they can change. This can be configured on a per-token basis in the settings of token. Other objects have permissions too, so even a [[Measurement Template|Templates]] has permissions (currenlty non configurable), so somthing created by master often can't be changed by other users. This restrictions apply to Macros that players run.

How to "fix" this: either edit permissions for all the objects, or implement some "messaging" module that will handles specially formed whispers sent to GM and do some stuff in response to this. For example script-heavy map that uses [[TriggerHappy|Community-Modules#trigger-happy]] may use this approach to send whispers to GM when player steps on Trap. On the side of GM that "potentially useful module" will parse the message and determine what macro to call (potentially rechecking conditions). In practice: it's easier to configure permissions than bother implementing such a module.

## Actors and tokens

Actor represents Characters or NPCs that you create in the [[Actors directory|Actors]] of the [[Sidebar|Sidebar]], or to be more precise, they only represent "data" of these objects (details later) that generally is accessible through character sheet.

Tokens represent tokens placed on the map. In the settings of token you can see a "Link actors data" checkbox. Let's call tokenks where this checkbox is set as "linked tokens", and in opposite case — "unlinked tokens".

Each token object has an `actor` attribute that behaves differently for "linked" and unlinked tokens. For "linked" token data stored in that attribute represents the same character sheet that is openned when you open something from "Actrors" tab of sidebar, so changing `actor` of linked token will change actor in that tab too. For unlinked token `actor` attribute represents "synthetic actor" that starts as a copy of actor from Actors tab, and tracks changes independantly from original actor.

Linked tokens are usually used for "characters": each token on different scene will have the same character sheet. Multiple tokens of actor on same scene behave similarly.

Unlinked tokens are usually used for "monsters" and other "npcs": each token on map will have it's own character sheet. This may sometimes be used for characters too, for example if you want to have a character "in a dream" then you can create an unlinked token to use it in one scene: changes to character sheet on that scene will not affect "main character sheet"

`token.actor` attribute "properly" handles `update` for both cases, so updating `resources.hp.value` of a token is as simple as:
```js
token.actor.update({
  'data.resources.hp.value': token.actor.data.data.resources.hp.value - 5
}); // In reality you should also consider min/max values
```

Note: sometimes you can see different way to update a token's character sheet:
```js
if (token.data.actorLink) {  // if token is "linked"
  token.actor.update({[`data.${attribute}`]: newValue});
} else { // if token is "unlinked"
  token.update({[`actorData.data.${attribute}`]: newValue});
}
```
This is not really needed now (at least in Foundry v0.5.5) and `token.actor.update({'foo': 'bar'})` for unlinked token will do just the same thing as code in `else` branch of previous example: 

`if (token.data.actorLink) token.actor.update({'foo': 'bar'})`

is the same as

`token.update({'actorData.foo': 'bar'})`

So it's safe to simply do `token.actor.update` both for linked and for unlinked tokens.

### Expected data structure

Actor: 
```js
{
  _id: "...", 
  name: "...", 
  permissions: {default: Number, `${userIdString}`: Number}, 
  type: "e.g.character", 
  data: {
    // Actually this depends on a system (template.json) and in some 
    // cases some inner objects do not have restrictions on keys
    attributes: {...},
    resources: {...},
  },
  flags: {},  // Please don't update this directly, use `actor.setFlag`
}
```

Token:
```js
{
_id: "OUfGJUIjOlku2VRS",
actorData: {},
actorId: "g8RFI5YLBoPc3WcO",
actorLink: true,
bar1: {attribute: "resources.hp"},
bar2: {attribute: "resources.strangeness"},
brightLight: 0,
brightSight: 0,
dimLight: 0,
dimSight: 0,
displayBars: 50, // See https://foundryvtt.com/api/global.html#TOKEN_DISPLAY_MODES
displayName: 50, 
disposition: 1,  // See https://foundryvtt.com/api/global.html#TOKEN_DISPOSITIONS
effects: [],
elevation: 0,
flags: {}, // Please don't update this directly, use `token.setFlag`
height: 1,
hidden: false,
img: "shared/images/tokens/Foo-Bar.png",
lightAlpha: 1,
lightAngle: 360,
lightColor: "",
lockRotation: false,
mirrorX: false,
mirrorY: false,
name: "...",
rotation: 0,
scale: 1,
sightAngle: 360,
vision: false,
width: 1,
x: 1610,
y: 2380
}
```

### "Current" actor and token.

There are 2 special variables available for script macro: `token` and `actor`, that are set to a "earliest" selected token and to it's corresponding actor. If there is nothing selected but current user is a player and  character is configured for that player (in "Player configuration", not simply by setting ownership), then you can get actor from `game.user.character`, and having it you can get a token for that actor from current scene:
```js
actor = actor ? actor : game.user.character;
if (!token && game.user.character) token = actor.getActiveTokens()[0];
// Note: if character for some reason has more than 1 token on map, then
// only "first" of them will be used. Also: there may be NO token for that 
// player on current scene.
```

If you are writing your own system or module, then often there will be no `token` variable that holds current selected token. To get one in this situation, you can take first element of `canvas.tokens.controlled`.

"Too complex to use" way to get active token:
```js
export function getActingToken({actor, limitActorTokensToControlledIfHaveSome=true, warn=true, linked=false}={}) {
  const tokens = [];
  const character = game.user.character;
  if (actor) {
    if ( limitActorTokensToControlledIfHaveSome && canvas.tokens.controlled.length > 0 ) {
      tokens.push(...canvas.tokens.controlled.filter(t => {
        if (!(t instanceof Token)) return false;
        if (linked) return t.data.actorLink && t.data.actorId === this._id;
        return t.data.actorId === this._id
      }));
      tokens.push(...actor.getActiveTokens().filter(t => canvas.tokens.controlled.some(tc => tc._id == t._id)));
    } else {
      tokens.push(...actor.getActiveTokens());
    }
  } else {
    tokens.push(...canvas.tokens.controlled);
    if ( tokens.length === 0 && character ) {
      tokens.push(...character.getActiveTokens());
    }
  }
  if ( tokens.length > 1 ) {
    if ( warn ) ui.notifications.error("Too many tokens selected or too many tokens of actor in current scene.");
    return null;
  } else {
    return tokens[0] ? tokens[0] : null;
  }
}
```

### Other ways to get tokens

Sometimes you may want to get all tokens on current scene:
```js
// all tokens on current scene that are selected:
for (let token of canvas.tokens.controlled) console.log(token.name);

// all tokens on current scene:
for (let token of canvas.tokens.placeables) console.log(token.name);

// all tokens of player characters on current scene:
characterTokens = game.users.players.reduce((tokens, u) => {
    let token = u.character ? u.character.getActiveTokens()[0] : null;
    if (token) {
        tokens.push(token);
    };
    return tokens;
}, []);

// all tokens of current scene that are also in combat now:
canvas.tokens.placeables.filter(t => t.inCombat);
```

## Chat messages and rolls

Sometimes you want to have both flexibility of Scripted Macro and a roll results in chat (or other message). For this you can use [`Roll(...).roll().toMessage(...)`](https://foundryvtt.com/api/Roll.html#toMessage) or [`ChatMessage.create(...)`](https://foundryvtt.com/api/ChatMessage.html#.create)

### Expected data structure

```js
{
_id: "IumnLhgq16IYaU5d",
content: "1d20",
flags: {},  // Please don't update this directly, use `token.setFlag`
flavor: " Flavor text",
roll: '{"class":"Roll","formula":"1d20","dice":[{"class":"Die","faces":20,"rolls":[{"roll":16}],"formula":"1d20","options":{}}],"parts":["_d0"],"result":"16","total":16}',  // This is a string with JSON data about original roll
sound: "sounds/dice.wav",
speaker: {scene: "kRMKKOP6oZXX4QSp", actor: null, token: null, alias: "Gamemaster"},
timestamp: 1588121758652,
type: CHAT_MESSAGE_TYPES.ROLL,  // See https://foundryvtt.com/api/global.html#CHAT_MESSAGE_TYPES
user: "J8QI73ORKEvonlPQ",  // id of user sending a message
whisper: ["idOfUser"], // Usually if that list is not empty, then type will be CHAT_MESSAGE_TYPES.WHISPER
}
```

### ChatMessage

The simplest way to create a message is:
```js
ChatMessage.create({content: "Your text here"});
```

In some cases you may want to override "speaker" of a message:
```js
ChatMessage.create({content: "Your text here", speaker: ChatMessage.getSpeaker({token: token})});
ChatMessage.create({content: "Your text here", speaker: ChatMessage.getSpeaker({actor: actor})});
ChatMessage.create({content: "Your text here", speaker: ChatMessage.getSpeaker({user: otherUser})});
ChatMessage.create({
  content: "Spikes pierce you and you loose over 9000 hp",
  speaker: ChatMessage.getSpeaker({alias: "Deadly spiky trap"})
});
```

### Roll

You can roll like this:
```js
roll = new Roll("1d20 + @attributes.str.mod", token.actor.getRollData()).roll();
roll.toMessage({
  flavor: `${actor.name} tries to bend a bar.`,
  speaker: ChatMessage.getSpeaker({token: token}),
});
```

You can also add custom "@-attributes" to your formula if you wish:
```js
const rollData = token.actor.getRollData();
mergeObject(rollData, {strangeMacroishBonus: 42});
roll = new Roll("1d20 + @attributes.str.mod + @strangeMacroishBonus", rollData).roll();
// The same `roll.toMessage({...})` code here.
```

### Other things useful for writing macros

* `canvas.tokens.controlled` — selected tokens.
* `game.user.targets` — targets selected by current user. It's a [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set), so use appropriately or convert to array: `Array.from(game.user.targets)`
* `game.combat` -- instance of [Combat](https://foundryvtt.com/api/Combat.html) that is active on current scene.
  * `game.combat.combatant` -- "Combatant" object of current turn. Has attributes:
    * `actor` with Actor instance.
    * `token` with **data** of a token (not an instance of Token), so it's the same as `token.data` that you usually use in macro code.
    * `initiative`, `resource`, `active`.
  * `game.combat.combatants`: all "Combatant" objects of current combat.
* distance between 2 tokens: [`canvas.grid.measureDistance(fromToken, toToken, {gridSpaces: True})`](https://foundryvtt.com/api/GridLayer.html#measureDistance)
* Do something based on rolled initiative for active combat:
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
* [Dialog](https://foundryvtt.com/api/Dialog.html). Example:
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
    const content = `
This action needs to know distance and somethingElse.
<div class="form-group dialog distance-prompt">
  <label>distance:</label> <input type="number" name="distance" value="0"/>
</div>
<div class="form-group dialog distance-prompt">
  <label>somethingElse:</label> <input type="number" name="somethingElse" value="0"/>
</div>
    `;
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
