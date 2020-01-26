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

#### Rolling perception (in gm mode) for selected tokens or active players if no token is selected
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