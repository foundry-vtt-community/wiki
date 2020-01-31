# What is a Macro?
A macro is a set of commands (such as a roll, a message, or a Javascript scriptlet) that Foundry can execute when the associated macro button is pressed.

Macros were added in Foundry VTT version `0.4.4`

# Macro Types
## Chat Macros

### Examples

## Script Macros

### Examples
#### Random Table Roll 

```js
const table = game.tables.entities.find(t => t.name === "MY TABLE NAME");
table.draw();
```

Replace the table name with the one you want to use.

#### Rolling perception (in gm mode) for selected tokens or active players if no token is selected. For dnd5e
```js
let actors = [];
// getting all actors of selected tokens
for(let id in canvas.tokens._controlled){
  actors.push(canvas.tokens._controlled[id].actor);
}
// if there are no selected tokens, get the actors the actors that represent active players
if(actors.length<1) {
  for(let id in game.users.entities) {
    if(game.users.entities[id].active){
	  if(game.users.entities[id].character !== null) {
	    actors.push(game.users.entities[id].character)
  	  }			
	}
  }
}

// roll for every actor
let messageContent = '';
for(let actor of actors) {
  let modifier = actor.data.data.skills.per.mod; // this is total bonus for perception (abilitie mod + proficiency)
  let result = new Roll(`1d20+${modifier}`).roll().total; // rolling the formula
  messageContent += `${actor.name} rolled <b>${result}</b> for perception<br>`; // creating the output string
}

// create the message
if(messageContent !== '') {
  let chatData = {
    user: game.user._id,
    speaker: ChatMessage.getSpeaker(),
    content: messageContent,
    whisper: game.users.entities.filter(u => u.isGM).map(u => u._id)
  };
  ChatMessage.create(chatData, {});
}
```
You can edit `${actor.name} rolled <b>${result}</b> for perception<br>` to change the displayed text.

### Consume various resources. 

This was actually written as a module that provides the dailyGrind function to be called from a macro with
```js
MacroModule.dailyGrind(actor, [["ration1", 1], ["ration2", 2]])
```

As a standalone macro it looks like:

```js
// Consume items from inventory
let consumption = [["ration1", 1], ["ration2", 2]];
let updates = [];
let consumed = "";
for (let [name, quantity] of consumption) {
  let item = actor.items.find(i=> i.name===name);
  if (item.data.data.quantity < quantity) {
    ui.notifications.warn(`${game.user.name} not enough ${name} remaining`);
    consumed += `Only had ${item.data.data.quantity} ${name} but needed ${quantity} - death ensues<br>`;
  } else {
    updates.push({"_id": item._id, "data.quantity": item.data.data.quantity - quantity});
    consumed += `Consumed ${quantity} ${item.data.name} and has ${item.data.data.quantity - quantity} left<br>`;
  }
}

if (updates.length > 0) {
  actor.updateManyEmbeddedEntities("OwnedItem", updates);
}
ChatMessage.create({
  user: game.user._id,
speaker: { actor: actor, alias: actor.name },
  content: consumed,
  type: CONST.CHAT_MESSAGE_TYPES.OTHER
});
```